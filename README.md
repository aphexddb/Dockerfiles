# Dockerfiles

## Utility commands

Nuke all images ran or running:

    docker stop $(docker ps -a -q) ; docker rm $(docker ps -a -q)

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
