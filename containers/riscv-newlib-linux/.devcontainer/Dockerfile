FROM ubuntu:21.04

ENV RISCV="/usr/local/riscv"
ENV PATH="${RISCV}/bin:${PATH}"

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install sudo lsb-release wget git software-properties-common  device-tree-compiler \
    autoconf automake autotools-dev curl python3 python3-distutils libmpc-dev libmpfr-dev libgmp-dev  \
    gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev

RUN git clone https://github.com/riscv/riscv-gnu-toolchain \
    && cd ./riscv-gnu-toolchain \
    && ./configure --prefix=${RISCV} && make && make linux

RUN git clone https://github.com/riscv/riscv-isa-sim \
    && cd ./riscv-isa-sim && mkdir build && cd build \
    && ../configure --prefix=${RISCV} \
    && make && make install

RUN git clone https://github.com/riscv/riscv-pk \
    && cd ./riscv-pk && mkdir build && cd build \
    && ../configure --prefix=${RISCV} --host=riscv64-unknown-elf \
    && make && make install