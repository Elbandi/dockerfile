#
# SmartGit Dockerfile
#
# https://github.com/elbandi/dockerfile
# https://github.com/elbandi/dockerfile/tree/master/smartgit
#

# Pull base image.
FROM java:openjdk-8-jre

ENV DEBIAN_FRONTEND noninteractive

ENV SMARTGIT_VERSION 7_0_2

# Add SmartGit, downloaded from http://www.syntevo.com/smartgit/download/
ADD smartgit-${SMARTGIT_VERSION}.deb /tmp/

# Install depends and smartgit
RUN \
    apt-get update && \
    apt-get install -y git git-gui gitk libgtk2.0-0 libxtst6 libjna-java && \
    dpkg -i /tmp/smartgit-${SMARTGIT_VERSION}.deb && \
    echo "-Dsmartgit.settings=/data/.smartgit/6.5" >/usr/share/smartgit/bin/smartgit.vmoptions && \
    rm /tmp/smartgit-${SMARTGIT_VERSION}.deb && \
    rm -rf /var/lib/apt/lists/*

# My X11 desktop
ENV DISPLAY 192.168.200.26:51

# Define user
USER www-data

# Define commonly used HOME variable
ENV HOME /data

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["/usr/share/smartgit/bin/smartgit.sh"]
