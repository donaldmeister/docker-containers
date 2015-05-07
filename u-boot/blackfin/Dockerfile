# dongle_lite bootloader build environment
# April 2, 2015
#
# VERSION 0.0.1

FROM debian:wheezy

MAINTAINER Mentor Graphics(c) 2015

# install git in order to download the build tools and u-boot code
RUN apt-get update && apt-get install -y git

# install packages needed to execute the build tools
RUN apt-get install -y zlib1g-dev \
                       libglib2.0-dev \
                       libpixman-1-dev \
                       libftdi1 \
                       urjtag \
                       ncurses-dev \
                       pkg-config \
                       autoconf \
                       automake \
                       bison \
                       flex \
                       gettext \
                       m4 \
                       make \
                       texinfo \
                       g++ \
                       gawk \
                       python \
                       bc \
                       bzip2 \
                       ack-grep \
                       vim

# create a non-root user in order for executing build-tools
RUN useradd -d /home/developer -m -s /bin/bash developer
RUN echo "developer:developer" | chpasswd
RUN echo "developer ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# mkdir build directory and volume mount point
RUN mkdir /opt/blackfin-sources
RUN chown developer:developer /opt/blackfin-sources

# switch to the non-root user to generate the build-tools and build u-boot
USER developer

# clone the adi-toolchin-blackfin repository
RUN git clone git://git.code.sf.net/p/adi-toolchain/blackfin /opt/blackfin-sources/toolchain
RUN git clone git://git.code.sf.net/p/adi-u-boot/code /opt/blackfin-sources/u-boot
RUN git clone git://git.code.sf.net/p/adi-buildroot/code /opt/blackfin-sources/buildroot
RUN git clone git://git.code.sf.net/p/adi-linux/code /opt/blackfin-sources/buildroot/linux/linux-kernel

RUN mkdir /opt/blackfin-sources/build
WORKDIR /opt/blackfin-sources

# run the build tools
#RUN /opt/blackfin-sources/toolchain/buildscript/BuildToolChain \
#        -b /opt/blackfin-sources/build \
#        -k /opt/blackfin-sources/buildroot/linux/linux-kernel \
#        -s /opt/blackfin-sources/toolchain \
#        -u /opt/blackfin-sources/u-boot



USER root

#VOLUME /opt


