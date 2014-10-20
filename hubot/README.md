# Substantia Hubot

Build Container

    docker build -t hubot .

Run hubot container

    docker run -d hubot:latest

Run a shell to checkout container

    docker run --rm=true -i -t hubot:latest /bin/bash

Nuke all containers stopped or running

    docker stop $(docker ps -a -q) ; docker rm $(docker ps -a -q)
