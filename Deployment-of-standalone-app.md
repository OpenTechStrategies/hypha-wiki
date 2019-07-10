# OTF Application Installation Process

## Server Specs

- AWS T2-micro
- Ubuntu 18.04
- (Also tested on WSL Ubuntu 16.04)

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

- `sudo apt-get install postgresql postgresql-contrib`
- `sudo service postgresql start`
- `sudo su - postgres`
- `psql`
- `CREATE DATABASE opentech;`
- `CREATE USER root WITH SUPERUSER LOGIN` (temporary until we get this going, then we'll restrict.)
- Also, make sure that the root user has trust access in pg_hba.conf (also will restrict later.)

## Running app

- `export DJANGO_ADMIN_SETTINGS=opentech.settings.production`
- `export SECRET_KEY='SOME SECRET KEY HERE'`
- `python manage.py collectstatic --noinput`
- `python manage.py createcachetable`
- `python manage.py migrate --noinput && python manage.py clear_cache --cache=default --cache=wagtailcache`
  
   
   