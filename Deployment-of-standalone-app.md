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
- `pip install 'stellar==0.4.5'`
- `pip install 'Werkzeug==0.14.1'`

## Post-install setup

- `npm install`
- `gulp deploy`

## Running app

- `export DJANGO_ADMIN_SETTINGS=opentech.settings.production`
- `export SECRET_KEY='SOME SECRET KEY HERE'`
- `python manage.py collectstatic --noinput`
- `python manage.py migrate --noinput && python manage.py clear_cache --cache=default --cache=wagtailcache`
  
   
   
