#
# WebStorm Dockerfile
#
# https://github.com/elbandi/dockerfile
# https://github.com/elbandi/dockerfile/tree/master/webstorm
#

# Pull base image.
FROM dockerfile/java

# Add WebStorm, downloaded from https://www.jetbrains.com/webstorm/
ADD WebStorm-9.0.3.tar.gz /tmp/

# Install webstorm and fix paths
RUN \
    mv /tmp/WebStorm* /opt/webstorm && \
    sed 's%..user.home.%/data%;s%# idea.config.path%idea.config.path%;s%# idea.system.path%idea.system.path%' -i /opt/webstorm/bin/idea.properties

# My X11 desktop
ENV DISPLAY 192.168.200.26:51

# Define user
USER www-data

# Define commonly used HOME variable
ENV HOME /data

# Define default command.
CMD ["/opt/webstorm/bin/webstorm.sh"]