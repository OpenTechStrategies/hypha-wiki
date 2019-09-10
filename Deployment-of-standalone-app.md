# OTF Application Installation Process

## Standalone Server/VPS

This process was tested on Ubuntu 18.04LTS. It should work on any Debian-based system.

### Basic installation steps.

These are the basic packages needed before you can start the installation process.

- python3-pip - install using  `sudo apt-get install python3-pip`
- postgresql (version 10.9) use `sudo apt-get install postgresql postgresql-contrib`
- to install nodejs (version v12.5.0), use nodesource. Add the PPA to your sources list by running this script: `curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - then `sudo apt-get install nodejs`
- gulp (version 4.0.2 CLI version 2.2.0) installed using `sudo npm install -g gulp`

Then, you'll want to set up a virtual environment: `virtualenv --python=/usr/bin/python3 venv/opentech` and `source venv/opentech/bin/activate`

Next, install the required packages using `pip install -r requirements.txt`. You can also install stellar and Werkzeug, but they are not required in production.

- `pip install 'stellar==0.4.5'` (not needed in production)
- `pip install 'Werkzeug==0.14.1'` (not needed in production)

### Post-install setup
You'll want to install npm, `npm install`, and then deploy gulp using `gulp deploy`.

Postgresql is the database used. Start the server you installed above using `sudo service postgresql start`, then log into the postgres superuser, `sudo su - postgres` and enter the postgresql cli with `psql`. In the CLI, use these commands:

- `CREATE DATABASE opentech;`
- `CREATE USER [linux username] WITH SUPERUSER LOGIN`
- Also, make sure that this user has trust access in pg_hba.conf.

These settings can be restricted later as required.

### Running the app

First, choose the correct settings - the possibilities are 'dev', 'test', and 'production'. If you're going to set this up in a production setting, then 'production' is the one to use: `export DJANGO_ADMIN_SETTINGS=opentech.settings.production`. The application needs a secret key: `export SECRET_KEY='SOME SECRET KEY HERE'`.

To begin with, set the `export SECURE_SSL_REDIRECT=false` to prevent SSL redirect. When you've set up SSL for your server, you can change that setting later.

Then use the following commands to test run the server:

- `python manage.py collectstatic --noinput`
- `python manage.py createcachetable`
- `python manage.py migrate --noinput && python manage.py clear_cache --cache=default --cache=wagtailcache`
- `python manage.py runserver` (runs development server at http://127.0.0.1:8000)

You should see the home page of the server. That's great. We can then take the next steps.

### Deploy with nginx/gunicorn

Make sure gunicorn is installed (it should be). Do a test run with gunicorn: `gunicorn --bind 0.0.0.0:<some port> opentech.wsgi:application` This might not work. It's OK if it doesn't work - you can go on anyway.

You need to add a file: /etc/systemd/system/gunicorn.socket. It should have this content:

```
[Unit]
Description=gunicorn service
Requires=gunicorn.socket
After=network.target

[Service]
User=ubuntu
Group=www-data
WorkingDirectory=/path/to/application/
ExecStart=/path/to/virtual/environment/bin/gunicorn --access-logfile - --workers 3 --bind unix:/path/to/application/gunicorn.sock opentech.wsgi:application -e DJANGO_ADMIN_SETTINGS=opentech.production -e SECRET_KEY='SOME SECRET KEY HERE'

[Install]
WantedBy=multi-user.target
```
You can start and enable the socket by using `sudo systemctl start gunicorn.socket`, `sudo systemctl enable gunicorn.socket`. You can check status of socket using `sudo systemctl status gunicorn.socket`.
You can test the status of gunicorn: `sudo systemctl status gunicorn`.

Set up DNS so that server.domain and apply.server.domain point to the server you've installed the application. Install nginx if you haven't already (`sudo apt-get install nginx`). You'll need to add two new config files for nginx in /etc/nginx/sites-available:

main
```
server {
    listen 80;
    server_name server.domain;

     location ^~/static/(.*)$ {
        alias /path/to/application/opentech/staticfiles/;
    }

    location / {
        include proxy_params;
        proxy_pass http://unix:/run/gunicorn.sock;
    }

}
```

apply
```
server {
   listen 80;
   server_name apply.server.domain;
   location ^~/static/(.*)$ {
      root /path/to/application/opentech/staticfiles/;
   }
   location / {
      include proxy_params;
      proxy_pass http://unix:/run/gunicorn.sock;
    }
}
```
Then, symlink these to sites-enabled: `sudo ln -s /etc/nginx/sites-available/main /etc/nginx/sites-enabled && sudo ln -s /etc/nginx/sites-available/apply /etc/nginx/sites-enabled`. Then restart nginx using `sudo systemctl restart nginx`.

**You should then be able to access your application at http://server.domain and http://apply.server.domain.** 
  
   
   