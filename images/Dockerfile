FROM amd64/ubuntu:latest

### Base

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Stockholm

RUN apt-get update -y && apt-get install -y --no-install-recommends \
        bison \
        gcc \
        g++ \
        gnupg \
        curl \
        ninja-build \
        build-essential \
        xz-utils \
        git \
        unzip \
        tar \
        wget \
        ca-certificates

### LLVM

RUN wget -nv -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add -
RUN echo "deb http://apt.llvm.org/focal/ llvm-toolchain-focal main" \
        > /etc/apt/sources.list.d/llvm.list; \
    apt-get -qq update && \
    apt-get install -qqy -t llvm-toolchain-focal \
        clang clang-tidy clang-format lld llvm

### CMake

ARG CMAKE_VERSION=3.21.1

RUN wget https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-Linux-x86_64.sh \
      -q -O /tmp/cmake-install.sh \
      && chmod u+x /tmp/cmake-install.sh \
      && mkdir /usr/bin/cmake \
      && /tmp/cmake-install.sh --skip-license --prefix=/usr/bin/cmake \
      && rm /tmp/cmake-install.sh

ENV PATH="/usr/bin/cmake/bin:${PATH}"

### Cleanup

RUN apt-get autoclean && \
    apt-get autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* \
