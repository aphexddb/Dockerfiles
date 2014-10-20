# Use phusion/baseimage as base image. To make your builds
# reproducible, make sure you lock down to a specific version, not
# to `latest`! See
# https://github.com/phusion/baseimage-docker/blob/master/Changelog.md
# for a list of version numbers.
FROM phusion/baseimage:0.9.15

# Set correct environment variables.
ENV HOME /root

# Regenerate SSH host keys. baseimage-docker does not contain any, so you
# have to do that yourself. You may also comment out this instruction; the
# init system will auto-generate one during boot.
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

############## START APPLICATION ##############

# Install linux build tools
RUN apt-get update
RUN apt-get install -y gcc make g++ build-essential libc6-dev tcl wget git

# Hubot reqs (hipchat needs libxpat, etc: https://github.com/hipchat/hubot-hipchat)
RUN apt-get install -y libexpat1-dev libicu-dev

# install node
RUN apt-get -y install nodejs nodejs-legacy npm

# install Hubot
RUN npm install -g coffee-script hubot@v2.7.5

# Create a Hubot
RUN mkdir -p /hubot
WORKDIR /hubot
RUN hubot --create .
RUN npm install
RUN npm install hubot-hipchat --save
RUN npm install hubot-redis-brain --save
RUN chmod 755 bin/hubot

VOLUME ["/hubot"]

ENV HUBOT_HIPCHAT_JID <todo>
ENV HUBOT_HIPCHAT_PASSWORD <todo>
ENV REDIS_URL <todo>

ADD hubot.init /etc/service/hubot/run

############## END APPLICATION ##############

# Clean up APT when done.
#RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
