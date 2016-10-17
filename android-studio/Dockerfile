#
# Android Studio Dockerfile
#
# https://github.com/elbandi/dockerfile
# https://github.com/elbandi/dockerfile/tree/master/android-studio
#

# Pull base image.
FROM java:openjdk-8-jdk

ENV ANDROID_SDK_FILENAME android-sdk_r24.4.1-linux.tgz
ENV ANDROID_STUDIO_FILENAME android-studio-ide-145.3330264-linux.zip
ENV ANDROID_API_LEVELS android-15,android-16,android-17,android-18,android-19,android-22
ENV ANDROID_EXTRA extra-android-support,extra-android-m2repository,extra-google-m2repository
# Possible more extra packages:
# - extra-google-gcm
# - extra-google-google_play_services
# - extra-google-play_billing
# - extra-google-play_licensing
# - extra-google-webdriver
ENV ANDROID_BUILD_TOOLS_VERSION 24.0.3
ENV ANDROID_HOME /opt/android-sdk-linux
ENV ANDROID_SDK_HOME /data/.AndroidStudio2.0
ENV GRADLE_USER_HOME /data/.AndroidStudio2.0/.gradle
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools

# Add Android Studio, downloaded from http://developer.android.com/sdk/index.html
ADD ${ANDROID_STUDIO_FILENAME} /tmp/
# Add Android SDK, downloaded from http://developer.android.com/sdk/index.html
ADD ${ANDROID_SDK_FILENAME} /opt/

# Installs i386 architecture required for running 32 bit Android tools
RUN dpkg --add-architecture i386 && \
    apt-get update -y && \
    apt-get install -y libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoremove -y && \
    apt-get clean

# Installs Android SDK
RUN echo y | android update sdk --no-ui -a --filter tools,platform-tools,${ANDROID_API_LEVELS},build-tools-${ANDROID_BUILD_TOOLS_VERSION},${ANDROID_EXTRA}

# Install Android Studio and fix paths
RUN \
    usermod -d /data nobody && \
    unzip -q /tmp/android-studio*.zip -d /opt && \
    rm /tmp/android-studio*.zip && \
    sed -e 's%..user.home.%/data%;s%# idea.config.path%idea.config.path%;s%# idea.system.path%idea.system.path%' \
        -e 's%.AndroidStudio.0%.AndroidStudio2.0%' \
        -e '/idea.system.path/a \\nidea.library.source.dir=/data/.AndroidStudio2.0/libSources' -i /opt/android-studio/bin/idea.properties

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
CMD ["/opt/android-studio/bin/studio.sh"]
