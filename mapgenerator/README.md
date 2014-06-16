# Minecraft overviewer mapgenerator

The worker has a few more dependencies but this container does it's one thing. Get world files from /minecraft/world, create the map, and write the output to /www. This worker knows nothing about where or how it gets the files to process, it just processes world files into maps from it's local filesystem.

via [http://crosbymichael.com/advanced-docker-volumes.html](http://crosbymichael.com/advanced-docker-volumes.html)
