# Dockerfiles

Some Docker files I find handy. Where possible, all are built using the [http://phusion.github.io/baseimage-docker/](Phusion baseimage-docker) pattern.

## Minecraft server with overviewer

Build images (if local)

    docker build -t minecraft ./minecraft
    docker build -t mapserver ./mapserver
    docker build -t mapgenerator ./mapgenerator

Run the server!  

    MINECRAFT=$(docker run -d -p 25565:25565 minecraft)
    MAPSERVER=$(docker run -d -p 8000:8000 mapserver)
    docker run -volumes-from $MINECRAFT -volumes-from $MAPSERVER mapgenerator

Schedule overview builds every hour

    @hourly docker run -volumes-from $MINECRAFT -volumes-from $MAPSERVER mapgenerator

## Redis server

Build image (if local)

    docker build -t redis ./redis

Run the server!  

    REDIS=$(docker run -d -p 6379:6379 --name=redis redis)

Run the same server as a client!

    docker run -it --name=redis_client --link redis:redis --rm redis /bin/bash -c 'exec redis-cli -h "$REDIS_PORT_6379_TCP_ADDR" -p "$REDIS_PORT_6379_TCP_PORT"'

## Utility commands

Nuke all images ran or running:

    docker stop $(docker ps -a -q) ; docker rm $(docker ps -a -q)

Run a container with a bash shell

    docker run -i -t redis:latest /bin/bash
