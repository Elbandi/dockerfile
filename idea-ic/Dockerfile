#
# IntelliJ IDEA Community Edition Dockerfile
#
# https://github.com/elbandi/dockerfile
# https://github.com/elbandi/dockerfile/tree/master/idea-ic
#

# Pull base image.
FROM java:openjdk-7-jdk

# Add IntelliJ IDEA, downloaded from https://www.jetbrains.com/idea/
ADD ideaIC-14.1.2.tar.gz /tmp/

# Install IntelliJ IDEA and fix paths
RUN \
    mv /tmp/idea-IC* /opt/idea-IC && \
    sed 's%..user.home.%/data%;s%# idea.config.path%idea.config.path%;s%# idea.system.path%idea.system.path%' -i /opt/idea-IC/bin/idea.properties

# My X11 desktop
ENV DISPLAY 192.168.200.26:51

# Define user
USER nobody

# Define commonly used HOME variable
ENV HOME /data

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["/opt/idea-IC/bin/idea.sh"]
