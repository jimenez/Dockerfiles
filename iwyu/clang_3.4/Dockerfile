#llvm clang 3.4 + IWYU image

FROM ubuntu:14.04
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

#Checkout IWYU and switch the banch clang_3.4
RUN mkdir include-what-you-use && cd include-what-you-use && svn co http://include-what-you-use.googlecode.com/svn/trunk/ source && cd source && svn switch ^/branches/clang_3.4

ENV CC clang
ENV CXX clang++
ENV CMAKE_C_COMPILER clang
ENV CMAKE_CXX_COMPILER clang++

#Configure IWYU
RUN cd include-what-you-use && mkdir build && cd build && cmake -G "Unix Makefiles" -DLLVM_PATH=/usr/lib/llvm-3.4 ../source

#Compile and install IWYU
RUN cd include-what-you-use/build && make && make install
