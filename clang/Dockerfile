# -*- mode: dockerfile -*-
FROM ubuntu:16.04
MAINTAINER Shogo Sawai
ENV DEBIAN_FRONTEND noninteractive
ENV EMSCRIPTEN_ROOT /opt/emsdk_portable
ENV LLVM_HASH d49f798558cc172a2a868d8098f0116135534946
ENV CLANG_HASH 04d0827ce598578a3cd298f2834352198b5c3285
ENV COMPILER_RT_HASH 054a09b3998670d99074bae79cf8b9d71711c1da
ENV LIBCXX_HASH f47536798d2a69901035e3a9fd23f7240e25ff27
ENV LIBCXXABI_HASH 08bf03cf8ca8a4f55644956aec77677b3f0cf232
ENV CLANG_TOOLS_EXTRA_HASH 3f32ce33f870300972e84ef4390f27f9ed40094c
# apt-get build-dep -y llvm clang
RUN apt-get update && \
    apt-get install -y git gcc g++ cmake python && \
    apt-get upgrade -y && \
    apt-get clean && \
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/* 
RUN set -x && \
    cd ~ && \
    git clone -n http://llvm.org/git/llvm.git && \
    cd llvm && \
    git checkout ${LLVM_HASH} && \
    cd tools/ && \
    git clone -n http://llvm.org/git/clang.git && \
    cd clang/ && \
    git checkout ${CLANG_HASH} && \
    cd ../../projects/ && \
    git clone -n http://llvm.org/git/compiler-rt.git && \
    cd compiler-rt && \
    git checkout ${COMPILER_RT_HASH} && \
    cd .. && \
    git clone -n http://llvm.org/git/libcxx.git && \
    cd libcxx && \
    git checkout ${LIBCXX_HASH} && \
    cd .. && \
    git clone -n http://llvm.org/git/libcxxabi.git && \
    cd libcxxabi && \
    git checkout ${LIBCXXABI_HASH} && \
    cd ../../tools/clang/tools/ && \
    git clone -n http://llvm.org/git/clang-tools-extra.git && \
    cd clang-tools-extra && \
    git checkout ${CLANG_TOOLS_EXTRA_HASH} && \
    cd ~ && \
    mkdir build && \
    cd build/ && \
    cmake -G "Unix Makefiles" -DBUILD_SHARED_LIBS=true -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr ../llvm/ && \
    make && \
    make install && \
    cd ~ && \
    rm -rf llvm && \
    rm -rf build
