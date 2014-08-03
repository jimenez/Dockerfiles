#Mesos image from clang 3.4

FROM jimenez/iwyu:clang_3.4
MAINTAINER Isabel Jimenez <contact@isabeljimenez.com>

RUN apt-get update -q

#Install Dependencies
RUN apt-get -qy install         \
    autoconf                    \
    automake                    \
    ca-certificates             \
    git-core                    \
    libcurl4-nss-dev            \
    libsasl2-dev                \
    libtool                     \
    --no-install-recommends

#Clone mesos repository
RUN git clone http://git-wip-us.apache.org/repos/asf/mesos.git

#Bootstrap
RUN cd mesos && ./bootstrap

#Configure
RUN mkdir /mesos/build && cd mesos/build && ../configure --disable-java --disable-python --disable-optimize --without-included-zookeeper

#Make
RUN cd /mesos/build && make -j 4

WORKDIR /mesos