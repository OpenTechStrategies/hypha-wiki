# Setup a local development environment with Docker for Hypha


## Requirements

Recent version of [Docker](https://www.docker.com/get-started).


## Domains for local development

You will need two domain to run this app. One for the public site and one for the apply site.

Add this to your `/etc/hosts` file. (Feel free to use another name but then remember to use it in all the commands below.)

~~~~
127.0.0.1 hypha.test
127.0.0.1 apply.hypha.test
~~~~

The "[test](https://en.wikipedia.org/wiki/.test)" TLD is safe to use, it's reserved testing purposes.

OBS! All examples from now on will use the `hypha.test` domains.


## Get the code

~~~~
$ git clone git@github.com:OpenTechFund/hypha.git hypha

$ cd hypha
~~~~

OBS! Everything from now on will happen inside the hypha directory.


## Build the Docker images

Move to the "docker" directory.

~~~~
$ cd docker
~~~~

Run the docker compose command to build the images.

~~~~
$ docker-compose build
~~~~

This will take some time.

Then it's time to start the docker containers.

~~~~
$ docker-compose up
~~~~

