#
# CLion Dockerfile
#
# https://github.com/elbandi/dockerfile
# https://github.com/elbandi/dockerfile/tree/master/clion
#

# Pull base image.
FROM dockerfile/java

# Add CLion, downloaded from https://www.jetbrains.com/clion/
ADD clion-140.2310.6.tar.gz /tmp/

# Install clion and fix paths
RUN \
    mv /tmp/clion* /opt/clion && \
    sed 's%..user.home.%/data%;s%# idea.config.path%idea.config.path%;s%# idea.system.path%idea.system.path%' -i /opt/clion/bin/idea.properties

# My X11 desktop
ENV DISPLAY 192.168.200.26:51

# Define user
USER www-data

# Define commonly used HOME variable
ENV HOME /data

# Define default command.
CMD ["/opt/clion/bin/clion.sh"]