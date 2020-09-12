FROM nvidia/cuda:10.2-cudnn7-devel-ubuntu18.04

LABEL maintainer="zaemyung@gmail.com"

ENV PYTHON_VERSION 3.8.5

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

RUN wget https://github.com/Kitware/CMake/releases/download/v3.18.2/cmake-3.18.2.tar.gz \
    && tar xzf cmake-3.18.2.tar.gz \
    && cd cmake-3.18.2 \
    && ./bootstrap \
    && make -j "$(nproc)" \
    && make install \
    && cd .. \
    && rm -rf cmake-3.18.2 \
    && rm -f cmake-3.18.2.tar.gz

RUN wget https://github.com/tmux/tmux/releases/download/3.1b/tmux-3.1b.tar.gz \
    && tar xzf tmux-3.1b.tar.gz \
    && cd tmux-3.1b \
    && ./configure \
    && make -j "$(nproc)" \
    && make install \
    && cd .. \
    && rm -rf tmux-3.1b \
    && rm -f tmux-3.1b.tar.gz

RUN wget -O /tmp/python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f /tmp/python.tar.xz \
    && rm /tmp/python.tar.xz

RUN wget https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tgz -O python.tgz \
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