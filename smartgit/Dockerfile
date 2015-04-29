#
# SmartGit Dockerfile
#
# https://github.com/elbandi/dockerfile
# https://github.com/elbandi/dockerfile/tree/master/smartgit
#

# Pull base image.
FROM java:openjdk-7-jre

ENV DEBIAN_FRONTEND noninteractive

# Add SmartGit, downloaded from http://www.syntevo.com/smartgit/download/
ADD smartgit-6_5_7.deb /tmp/

# Install depends and smartgit
RUN \
    apt-get update && \
    apt-get install -y git git-gui gitk libgtk2.0-0 libxtst6 libjna-java && \
    dpkg -i /tmp/smartgit-6_5_7.deb && \
    echo "-Dsmartgit.settings=/data/.smartgit/6.5" >/usr/share/smartgit/bin/smartgit.vmoptions && \
    rm /tmp/smartgit-6_5_7.deb && \
    rm -rf /var/lib/apt/lists/*

# My X11 desktop
ENV DISPLAY 192.168.200.26:51

# Define user
USER www-data

# Define commonly used HOME variable
ENV HOME /data

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["/usr/share/smartgit/bin/smartgit.sh"]
