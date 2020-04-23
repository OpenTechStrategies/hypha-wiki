# Setup a local development environment with Docker for Hypha


## Requirements

Recent version of [Docker](https://www.docker.com/get-started).


## Domains for local development

You will need two domain to run this app. One for the public site and one for the apply site.

Add this to your `/etc/hosts` file.

~~~~
127.0.0.1 hypha.test
127.0.0.1 apply.hypha.test
~~~~

The "[test](https://en.wikipedia.org/wiki/.test)" TLD is safe to use, it's reserved for testing purposes.

OBS! All examples from now on will use the `hypha.test` domains.


## Get the code

~~~~
$ git clone git@github.com:OpenTechFund/hypha.git hypha

$ cd hypha
~~~~

OBS! Everything from now on will happen inside the hypha directory.


## Docker

### Build the Docker images

Move to the "docker" directory.

~~~~
$ cd docker
~~~~

Run the docker compose command to build the images. This will take some time.

If you need to rebuild the images to get a later version just run the "build" again.

~~~~
$ docker-compose build
~~~~


### Start the docker environment

To start the docker containers you use the "up" command. This command you will use each time you want to start up and use this docker environment.

~~~~
$ docker-compose up
~~~~


### Access the docker environment

Go to [http://hypha.test:8090/](http://hypha.test:8090/)


### Run commands in  the docker environment

To get bash shell on the container that runs the Django app, use this command.

~~~~
docker-compose exec py bash
~~~~

Here you can issue django commands as normal.


### Stop the docker environment.

Press `ctrl+c` in the terminal window.