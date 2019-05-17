FROM ubuntu:18.04

ARG DEBIAN_FRONTEND="noninteractive"

RUN echo "nameserver 8.8.8.8 # Google dns" >> /etc/resolv.conf && more /etc/resolv.conf

RUN BUILD_DEPENDENCIES="\
  software-properties-common \
  wget sudo" \
  && dpkg --add-architecture i386 \
  && apt-get update \
  && apt-get install -y \
    winbind \
    $BUILD_DEPENDENCIES

RUN sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com --recv 0xF987672F
RUN wget https://dl.winehq.org/wine-builds/Release.key -O - | apt-key add -

RUN wget https://dl.winehq.org/wine-builds/Release.key -O - | apt-key add - \
    && apt-add-repository https://dl.winehq.org/wine-builds/ubuntu \
    && apt-get update && apt install -y --no-install-recommends winehq-devel \
    && apt-get remove --purge -y $BUILD_DEPENDENCIES \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*
