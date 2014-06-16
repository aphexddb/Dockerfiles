FROM ubuntu

RUN sed -i 's/universe/universe multiverse/' /etc/apt/sources.list
RUN apt-get update
RUN apt-get dist-upgrade -y

RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee /etc/apt/sources.list.d/webupd8team-java.list
RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
RUN apt-get update
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
RUN apt-get install -y oracle-java7-installer

ENV VERSION 1.7.5
RUN mkdir /minecraft
RUN wget -O /minecraft/minecraft.jar --no-check-certificate https://s3.amazonaws.com/Minecraft.Download/versions/${VERSION}/minecraft_server.${VERSION}.jar
RUN chmod +x /minecraft/minecraft.jar

EXPOSE 25565
WORKDIR /minecraft
VOLUME ["/minecraft"]
ENTRYPOINT ["java", "-jar", "minecraft.jar", "nogui"]
CMD ["-Xmx1024M", "-Xms768M"]
