#
# IntelliJ IDEA Community Edition Dockerfile
#
# https://github.com/elbandi/dockerfile
# https://github.com/elbandi/dockerfile/tree/master/idea-ic
#

# Pull base image.
FROM java:openjdk-8-jdk

# Add IntelliJ IDEA, downloaded from https://www.jetbrains.com/idea/
ADD ideaIC-2021.3.tar.gz /tmp/

# Install IntelliJ IDEA and fix paths
RUN \
    usermod -d /data nobody && \
    mv /tmp/idea-IC* /opt/idea-IC && \
    sed -e 's%..user.home.%/data%;s%# idea.config.path%idea.config.path%;s%# idea.system.path%idea.system.path%' \
        -e '/idea.system.path/a \\nidea.library.source.dir=/data/.IdeaIC/libSources' -i /opt/idea-IC/bin/idea.properties

# My X11 desktop
ENV DISPLAY 192.168.200.26:51

# Define user
USER nobody

# Define commonly used HOME variable
ENV HOME /data

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["/opt/idea-IC/bin/idea.sh"]
