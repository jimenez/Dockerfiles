#Mesos image from gcc 4.7

FROM ubuntu:14.04
MAINTAINER Isabel Jimenez <contact@isabeljimenez.com>

RUN apt-get update -q

#Install Dependencies
RUN apt-get -qy install         \
    build-essential             \
    autoconf                    \
    automake                    \
    ca-certificates             \
    gdb                         \
    git-core                    \
    libcurl4-nss-dev            \
    libsasl2-dev                \
    libtool                     \
    make                        \
    --no-install-recommends

#Creating a Mesos repository
RUN mkdir /mesos && chown daemon /mesos

WORKDIR /mesos

USER daemon

#Clone mesos repository
RUN git clone http://git-wip-us.apache.org/repos/asf/mesos.git .

#Bootstrap
RUN ./bootstrap

#Configure
RUN mkdir build && cd build && ../configure --disable-java --disable-python --disable-optimize --without-included-zookeeper

#Make
RUN cd build && make -j 4