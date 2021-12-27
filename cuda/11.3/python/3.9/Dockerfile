FROM nvidia/cuda:11.3-cudnn8-devel-ubuntu20.04

LABEL maintainer="zaemyung@gmail.com"

ENV PYTHON_VERSION 3.9.9
ENV CMAKE_VERSION 3.22.1
ENV TMUX_VERSION 3.2a
ENV LANG=C.UTF-8

RUN sed -i "s/archive\.ubuntu\.com/mirror\.kakao\.com/g" /etc/apt/sources.list

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        curl \
        dpkg-dev \
        gcc \
        git \
        libbluetooth-dev \
        libbz2-dev \
        libc6-dev \
        libevent-dev \
        libexpat1-dev \
        libffi-dev \
        libgdbm-compat-dev \
        libgdbm-dev \
        liblzma-dev \
        libncurses5-dev \
        libncursesw5-dev \
        libreadline-dev \
        libsqlite3-dev \
        libssl-dev \
        make \
        tk-dev \
        uuid-dev \
        vim \
        wget \
        xz-utils \
        zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}.tar.gz \
    && tar xzf cmake-${CMAKE_VERSION}.tar.gz \
    && cd cmake-${CMAKE_VERSION} \
    && ./bootstrap \
    && make -j "$(nproc)" \
    && make install \
    && cd .. \
    && rm -rf cmake-${CMAKE_VERSION} \
    && rm -f cmake-${CMAKE_VERSION}.tar.gz

RUN wget https://github.com/tmux/tmux/releases/download/${TMUX_VERSION}/tmux-${TMUX_VERSION}.tar.gz \
    && tar xzf tmux-${TMUX_VERSION}.tar.gz \
    && cd tmux-${TMUX_VERSION} \
    && ./configure \
    && make -j "$(nproc)" \
    && make install \
    && cd .. \
    && rm -rf tmux-${TMUX_VERSION} \
    && rm -f tmux-${TMUX_VERSION}.tar.gz

RUN wget https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-${PYTHON_VERSION}.tgz -O python.tgz \
    && tar -xvf python.tgz \
    && mv Python-* python \
    && cd python \
    && ./configure \
        --build="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
        --enable-loadable-sqlite-extensions \
        --enable-optimizations \
        --enable-option-checking=fatal \
        --enable-shared \
        --with-system-expat \
        --with-system-ffi \
        --without-ensurepip \
    && make -j "$(nproc)" \
    && make install \
    && cd .. \
    && ldconfig \
    && rm -rf python*

RUN python3 -m venv venv

ENV PATH=/venv/bin:$PATH

RUN curl https://bootstrap.pypa.io/get-pip.py | python
