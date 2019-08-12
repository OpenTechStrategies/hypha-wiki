# OTF Application Installation Process

## Server Specs

- AWS T2-micro
- Ubuntu 18.04
- (Also tested on WSL Ubuntu 18.04)

## Packages Installed before requirements.txt

- python3-pip
- postgresql (version 10.9): `sudo apt-get install postgresql postgresql-contrib`
- nodejs (version v12.5.0): 
  - `curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -`
  - `sudo apt-get install nodejs`
- gulp (version 4.0.2 CLI version 2.2.0):
  - `sudo npm install -g gulp`

## Setting up virtual environment

- `virtualenv --python=/usr/bin/python3 venv/opentech`
- `source venv/opentech/bin/activate`

## Installing packages 

- `pip install -r requirements.txt`
- `pip install 'stellar==0.4.5'` (not needed in production)
- `pip install 'Werkzeug==0.14.1'` (not needed in production)

## Post-install setup

- `npm install`
- `gulp deploy`

## Database setup

- `sudo service postgresql start`
- `sudo su - postgres`
- `psql`
- `CREATE DATABASE opentech;`
- `CREATE USER [linux username] WITH SUPERUSER LOGIN` (temporary until we get this going, then we'll restrict.)
- Also, make sure that this user has trust access in pg_hba.conf (also will restrict later.)

## Running app

- `export DJANGO_ADMIN_SETTINGS=opentech.settings.production`
- `export SECRET_KEY='SOME SECRET KEY HERE'`
- `export SECURE_SSL_REDIRECT=false` (to prevent SSL redirect)
- `python manage.py collectstatic --noinput`
- `python manage.py createcachetable`
- `python manage.py migrate --noinput && python manage.py clear_cache --cache=default --cache=wagtailcache`
- `python manage.py runserver` (runs development server at http://127.0.0.1:8000)

## Deploy with nginx/gunicorn

- make sure gunicorn is installed (should be)
- test run with gunicorn: `gunicorn --bind 0.0.0.0:<some port> opentech.wsgi:application`
- add /etc/systemd/system/gunicorn.socket
```
[Unit]
Description=gunicorn service
Requires=gunicorn.socket
After=network.target


[Service]
User=ubuntu
Group=www-data
WorkingDirectory=/home/ubuntu/opentech.fund/
ExecStart=/home/ubuntu/opentech.fund/venv/opentech/bin/gunicorn --access-logfile - --workers 3 --bind unix:/home/opentech.fund/gunicorn.sock opentech.wsgi:application -e DJANGO_ADMIN_SETTINGS=opentech.production -e SECRET_KEY='SOME SECRET KEY HERE'

[Install]
WantedBy=multi-user.target
```
- start and enable the socket: `sudo systemctl start gunicorn.socket`, `sudo systemctl enable gunicorn.socket`
- check status of socket: `sudo systemctl status gunicorn.socket`
- test status of gunicorn: `sudo systemctl status gunicorn`
- Add new config file for nginx in /etc/nginx/sites-available:
```
server {
    listen 80;
    server_name ec2-3-84-236-234.compute-1.amazonaws.com;

    location /static/ {
        root /home/ubuntu/opentech.fund/opentech;
    }

    location / {
        include proxy_params;
        proxy_pass http://unix:/run/gunicorn.sock;
    }

}
```
- symlink to sites-enabled: `sudo ln -s /etc/nginx/sites-available/newfile /etc/nginx/sites-enabled`
- restart nginx: `sudo systemctl restart nginx`
  
   
   