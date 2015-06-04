#llvm clang 3.4

FROM ubuntu:15.04
MAINTAINER Isabel Jimenez <contact@isabeljimenez.com>

RUN apt-get update -q

#Install Dependencies
RUN apt-get -qy install         \
    build-essential             \
    clang                       \
    cmake                       \
    libclang-dev		\
    libncurses-dev              \
    linux-libc-dev		\
    llvm-dev			\
    make                        \
    subversion			\
    --no-install-recommends

ENV CC clang
ENV CXX clang++
ENV CMAKE_C_COMPILER clang
ENV CMAKE_CXX_COMPILER clang++
