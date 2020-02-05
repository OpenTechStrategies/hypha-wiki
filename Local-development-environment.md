# OTF Application Installation Process

## Local development environment


### Requirements

Make sure you have these things installed on your system:

- Git
- Python 3.6.x or 3.7.x
- Pip (to install python packages)
- PostgreSQL 10.x (later might work as well)
    - libpq-dev (on Linux at least)
- Apache or Nginx
- Node 10.x (later might work as well)

On Linux install them with your normal package manager. On macOS [Homebrew](https://brew.sh/) is an excellent option.

For Windows [Chocolatey](https://chocolatey.org/) seems popular but we have no experience with Windows.


### Domains for local development

You will need two domain to run this app. One for the public site and one for the apply site.

Add this to your `/etc/hosts` file. Replace "hypha" with your site name.

~~~~
127.0.0.1 hypha.test
127.0.0.1 apply.hypha.test
~~~~

The "[test](https://en.wikipedia.org/wiki/.test)" TLD is safe to use, it's reserved testing purposes.

OBS! All examples from now on will use the `hypha.test` domains.


### Get the code

~~~~
$ git clone https://github.com/OpenTechFund/hypha.git hypha

$ cd hypha
~~~~

OBS! Everything from now on will happen inside the hypha directory.


### Python virtual environment

Create the virtual environment, specify the python binary to use and the directory. Then source the activate script to activate the virtual environment. The last line tells Django what settings to use.

~~~~
$ python3 -m venv venv/hypha
$ source venv/hypha/bin/activate
$ export DJANGO_SETTINGS_MODULE=opentech.settings.dev
~~~~

Inside your activated virtual environment you will use plain `python` and `pip` commands. Everything inside the virtual environment is python 3 since we specified that when we created it.

Each time you open up a new shell to work with the app you will need to activate the virtual environment.

~~~~
$ cd /path/to/application/hypha
$ source venv/hypha/bin/activate
$ export DJANGO_SETTINGS_MODULE=opentech.settings.dev
~~~~


### Install Python packages

All the needed python packages for production are listed in the `requirements.txt` file. Additional packages for development are listed in `requirements-dev.txt`, it also includes everything from the `requirements.txt` file.

For a development environment you then run:

~~~~
$ pip install -r requirements-dev.txt
~~~~

If any `requirements*.txt` file have been updated you will need to rerun this command to get the updated/added packages.

Some additional development tools that might come in handy are django-debug-toolbar and stellar. Stellar makes it quick and easy to create database snapshots and restore from them.

~~~~
$ pip install --upgrade django-debug-toolbar
$ pip install --upgrade stellar
~~~~


### Install Node packages

All the needed Node packages are listed in `package.json`. Install them with this command.

~~~~
$ npm install
~~~~

You will also need the gulp task manager. On some systems you might need to run this command with `sudo`.

~~~~
$ npm install -g gulp-cli
~~~~


### The Postgres database

If the `createdb`and `dropdb` is not available you will need to add the Postgres bin directory to you path or call the commands with complete path.

Create a database for the app.

~~~~
$ createdb hypha
~~~~

To drop a database use.

~~~~
$ dropdb hypha
~~~~

#### Linux installs might require setting up a user

On Linux you might need to run as the "postgres" user first when setting upp Postgres. Use it to create the database and set up a database user. For local development I suggest creating a user with the same name as you account, then you will not need to specify it on every command.

~~~~
$ su - postgres
$ createdb hypha
$ createuser [your-account-name]
~~~~

#### macOS users might need this fix

To make the app find the Postgres socket you might need to update the "unix_socket_directories" setting in the  `postgresql.conf` file.

~~~~
unix_socket_directories = '/tmp, /var/pgsql_socket'
~~~~

#### Use stellar for db snapshots

If you installed "stellar" you can use it to take snapshots and restore them.

~~~~
$ stellar snapshot hypha_2019-10-01
~~~~

~~~~
$ stellar restore hypha_2019-10-01
~~~~


### Local settings

On production it's recommend to use environment variables for all settings. For local development putting them in a file is however convenient.

When you use the "dev" settings it will included all the setting you put in `local.py`.

Copy the local settings example file.

~~~~
$ cp -p opentech/settings/local.py.example opentech/settings/local.py
~~~~

You most likely want to set these:

* `ALLOWED_HOSTS`
* `BASE_URL`
* `SECRET_KEY`


If you have a problem with "CSRF cookie not set".

~~~~
CSRF_COOKIE_SAMESITE = None
SESSION_COOKIE_SAMESITE = None
~~~~

If you do not use the app name for the database.

~~~~
import dj_database_url

DATABASES = {
    'default': dj_database_url.config(
        conn_max_age=600,
        default='postgres:///hypha'
    )
}
~~~~
### Create log directory

`mkdir -p var/log/`

### Set up Gunicorn

Gunicorn is installed inside the virtual enviroment since it's listed in `requirements.txt`.

At the bottom of this file you find a handy script for Gunicorn. For a quick test you can run this command from your site directory.

~~~~
$ gunicorn opentech.wsgi:application --env DJANGO_SETTINGS_MODULE=opentech.settings.dev --bind 127.0.0.1:9001
~~~~

Quit the server with `ctrl-c` when you done testing.

* `opentech.wsgi:application` links it up to the app via the `opentech/wsgi.py` file.
* `--env …` tells it what settings to use, for development your want "dev" settings.
* `--bind …` makes it listen on localhost port 90001. Socket works as well but on macOS they have given me issues, while tcp connections always seems to just work.



### Set up Apache or Nginx

Set up new vhost for Apache or Nginx. WE let the web server handle static files and proxy everything else over to Gunicorn.


#### Apache

~~~~
<VirtualHost 127.0.0.1:80>
  ServerName hypha.test
  ServerAlias apply.hypha.test
  DocumentRoot "/path/to/application/hypha/opentech"


  Alias /media/ /path/to/application/hypha/media/
  Alias /static/ /path/to/application/hypha/static/
  Alias /static_src/ /path/to/application/hypha/opentech/static_src/

  <Directory "/path/to/application/hypha/static">
    Require all granted
  </Directory>

  <Directory "/path/to/application/hypha/media">
    Require all granted
  </Directory>

  <Directory "/path/to/application/hypha/opentech/static_src">
    Require all granted
  </Directory>

  <IfModule mod_proxy_http.c>
    <Location "/">
      ProxyPreserveHost On
      ProxyPass http://127.0.0.1:9001/
      ProxyPassReverse http://127.0.0.1:9001/
    </Location>

    <LocationMatch "^/(static|media|static_src)/">
      ProxyPass !
    </LocationMatch>

    <LocationMatch "^/[\w-]+\.(ico|json|png|txt)$">
      ProxyPass !
    </LocationMatch>
  </IfModule>
</VirtualHost>
~~~~


#### Nginx

```
server {
    listen 80;
    server_name hypha.test apply.hypha.test;

    location /media/ {
        alias /path/to/application/hypha/media/;
    }

    location /static/ {
        alias /path/to/application/hypha/static/;
    }

    location / {
        include proxy_params;
        proxy_pass http://127.0.0.1:9001/;
    }

}
```



### Finally, the app itself

Start by specifying what settings file is to be used (if you have not already done this, see above).

~~~~
$ export DJANGO_SETTINGS_MODULE=opentech.settings.dev
~~~~

Then use the following commands to set up the app:

Create the cache tables.

~~~~
$ python manage.py createcachetable
~~~~

Run all migrations to set up the database tables.

~~~~
$ python manage.py migrate --noinput
~~~~

Create the first super user.

~~~~
$ python manage.py createsuperuser
~~~~

Collect all the static files.

~~~~
$ python manage.py collectstatic --noinput
~~~~

Set the addresses and ports of the two wagtail sites.

~~~~
$ python manage.py wagtailsiteupdate hypha.test apply.hypha.test 80
~~~~


Now you should be able to access the sites on <https://hypha.test/> and <https://apply.hypha.test/>

#### Administration

* The Django Administration panel: <http://apply.hypha.test/django-admin/>
* The Apply dashboard: <http://apply.hypha.test/dashboard/>
* The Apply Wagtail admin: <http://apply.hypha.test/admin/>

Use the email address and password you set in the `createsuperuser` step above to login.


### Front end development

See the `gulpfile.js` file for a complete list of commands. Here are the most common in development.

This will watch all sass and js files for changes and build them with css maps. It will also run the "collecstatic" command, useful when running the site with a production server and not the built in dev server.

~~~~
$ gulp watch
~~~~

If you are working on the React components then it may be worth just using one of the two following commands. They should do the same thing, but the npm command calls Webpack direct.

~~~~
$ gulp watch:app
# OR
$ npm run webpack-watch
~~~~

To build the assets which get deployed, use the following. The deployment scripts will handle this, and the files should not be committed.

~~~~
$ gulp build
~~~~


### Useful things

Script to start/stop/restart gunicorn:

~~~~ bash
#!/usr/bin/env bash

set -euo pipefail

WORKERS=3
PORT=${2:-9001}
PROJECT=$(cat "${VIRTUAL_ENV}/.project")
WSGI=$(find "${PROJECT}" -name wsgi.py)
WSGI=${WSGI%/*}
NAME=${WSGI##*/}
SETTINGS="${NAME}.settings.${3:-dev}"
RUNDIR="${PROJECT}/var/run"
LOGDIR="${PROJECT}/var/log"
SOCK="${RUNDIR}/${NAME}-gunicorn.sock"
PID="${RUNDIR}/${NAME}-gunicorn.pid"
LOGFILE="${LOGDIR}/${NAME}-gunicorn.log"

function start_gunicorn {
  if [[ ! -d "${RUNDIR}" ]]; then
    mkdir -p "${RUNDIR}"
  else
    rm -rf "${RUNDIR}/${NAME}*"
  fi

  if [[ ! -d "${LOGDIR}" ]]; then
    mkdir -p "${LOGDIR}"
  fi

  gunicorn \
      ${NAME}.wsgi:application \
      --env DJANGO_SETTINGS_MODULE=${SETTINGS} \
      --pid ${PID} \
      --bind 127.0.0.1:${PORT} \
      --workers ${WORKERS} \
      --name ${NAME} \
      --daemon \
      --reload \
      --log-file=${LOGFILE} \
      --log-level error
  echo "Gunicorn started."
}

function stop_gunicorn {
    kill `cat $PID`
    echo "Gunicorn stopped."
}

case $1 in
  start)
    start_gunicorn
  ;;
  stop)
    stop_gunicorn
  ;;
  restart)
    stop_gunicorn
    start_gunicorn
  ;;
  *)
    echo "Not a recognised command, use start/stop/restart."
  ;;
esac
~~~~
