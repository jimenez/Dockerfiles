#llvm clang trunk + IWYU image

FROM ubuntu:14.04
MAINTAINER Isabel Jimenez <contact@isabeljimenez.com>

RUN apt-get update -q

#Install Dependencies
RUN apt-get -qy install         \
    build-essential             \
    cmake                       \
    groff                       \
    lib32z1-dev                 \
    libncurses-dev              \
    python-dev                  \
    subversion                  \
    --no-install-recommends

#Checkout llvm and clang
RUN svn co http://llvm.org/svn/llvm-project/llvm/trunk llvm && cd llvm/tools &&                                 \
    svn co http://llvm.org/svn/llvm-project/cfe/trunk clang && cd ../.. && cd llvm/tools/clang/tools            \
    svn co http://llvm.org/svn/llvm-project/clang-tools-extra/trunk extra && cd ../../../.. && cd llvm/projects \
    svn co http://llvm.org/svn/llvm-project/compiler-rt/trunk compiler-rt

#Compile and install clang
RUN mkdir build && cd build ; ../llvm/configure && make -j16 && make install

#Checkout IWYU
RUN cd llvm/tools/clang/tools &&                                                                                \
    svn co http://include-what-you-use.googlecode.com/svn/trunk/ include-what-you-use &&                        \
    echo "add_subdirectory(include-what-you-use)" >> CMakeLists.txt ;                                           \
    sed -i 's/^DIRS.*:=/DIRS := include-what-you-use/' Makefile

#Configure, compile and install IWYU
RUN cd /llvm ; mkdir build && cd build && cmake .. && make -j16 && make install

ENV CC clang
ENV CXX clang++
ENV CMAKE_C_COMPILER clang
ENV CMAKE_CXX_COMPILER clang++