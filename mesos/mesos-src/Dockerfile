#Mesos image from clang 3.4 for development

FROM jimenez/mesos-dev:clang
MAINTAINER Isabel Jimenez <contact@isabeljimenez.com>

RUN apt-get update -q

#Install Dependencies
RUN apt-get -qy install         \
    emacs-nox                   \
    --no-install-recommends

#Bootstrap
RUN ./bootstrap

#Configure
RUN cd build && CC=clang CXX=clang++ CFLAGS='-fsanitize=thread -g' CXXFLAGS='-fsanitize=thread -g' ../configure --disable-python --disable-java --disable-optimize --without-included-zookeeper

#Make
RUN cd build && make -j 4
