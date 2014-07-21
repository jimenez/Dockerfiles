#llvm clang + IWYU image

FROM ubuntu:14.04
MAINTAINER Isabel Jimenez <contact@isabeljimenez.com>

RUN apt-get update -q

#Install Dependencies
RUN apt-get -qy install         \
    build-essential             \
    cmake                       \
    lib32z1-dev                 \
    libncurses-dev              \
    python-dev                  \
    subversion                  \
    --no-install-recommends

#Install llvm
RUN svn co http://llvm.org/svn/llvm-project/llvm/trunk llvm && cd llvm/tools &&                                 \
    svn co http://llvm.org/svn/llvm-project/cfe/trunk clang && cd ../.. && cd llvm/tools/clang/tools            \
    svn co http://llvm.org/svn/llvm-project/clang-tools-extra/trunk extra && cd ../../../.. && cd llvm/projects \
    svn co http://llvm.org/svn/llvm-project/compiler-rt/trunk compiler-rt
RUN mkdir build && cd build ; ../llvm/configure && make

#Install IWYU
RUN cd llvm/tools/clang/tools &&                                                                                \
    svn co http://include-what-you-use.googlecode.com/svn/trunk/ include-what-you-use &&                        \
    echo "add_subdirectory(include-what-you-use)" >> CMakeLists.txt ;                                           \
    sed -i 's/^DIRS.*:=/DIRS := include-what-you-use/' Makefile
RUN cd /llvm ; mkdir build && cd build && cmake .. && make  && make install
