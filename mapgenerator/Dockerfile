FROM ubuntu

RUN sed -i 's/universe/universe multiverse/' /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y

RUN echo "deb http://overviewer.org/debian ./" >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y --force-yes minecraft-overviewer wget

ENV VERSION 1.7.5

RUN wget --no-check-certificate https://s3.amazonaws.com/Minecraft.Download/versions/${VERSION}/${VERSION}.jar -P ~/.minecraft/versions/${VERSION}/

ENTRYPOINT ["overviewer.py"]
CMD ["/minecraft/world", "/www"]
