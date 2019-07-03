# OTF Application Installation Process

## Server Specs

- AWS T2-micro
- Ubuntu 18.04
- (Also tested on WSL Ubuntu 16.04)

## Packages Installed before requirements.txt

- python3-pip
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

- Tried two options:
  - From Heroku deployment: `python manage.py collectstatic --noinput`
  - Got: 
    ```
    No Django settings specified.
    Unknown command: 'collectstatic'
    Type 'manage.py help' for usage.
    ```
  - From Vagrant deployment: 
     - `export PYTHONPATH=/home/ubuntu/opentech.fund/`
     - `export DJANGO_ADMIN_SETTINGS=opentech.settings.production`
  - Got:
   `ModuleNotFoundError: No module named 'opentech'`
  - Then tried to set DJANGO_ADMIN_SETTINGS and use `python manage.py collectstatic --noinput`
  - Got: `django.core.exceptions.ImproperlyConfigured: The SECRET_KEY setting must not be empty.`
  - so: `export SECRET_KEY='THIS IS NOT A SECRET'`
  - then: 
   ```
   manage.py collectstatic: error: unrecognized arguments: --noinputpython manage.py collectstatic
   ```
   
