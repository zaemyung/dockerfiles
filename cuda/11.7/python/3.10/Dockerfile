FROM nvidia/cuda:11.7.1-cudnn8-devel-ubuntu22.04

LABEL maintainer="zaemyung@gmail.com" \
      org.opencontainers.image.source="https://github.com/zaemyung/dockerfiles"

ENV PYTHON_VERSION 3.10.11
ENV CMAKE_VERSION 3.26.4
ENV TMUX_VERSION 3.3a
ENV LANG=C.UTF-8

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        curl \
        dpkg-dev \
        gcc \
        git \
        htop \
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
        openssh-client \
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

RUN wget -O /tmp/python.tar.xz "https://www.python.org/ftp/python/${PYTHON_VERSION%%[a-z]*}/Python-$PYTHON_VERSION.tar.xz" \
    && mkdir -p /usr/src/python \
    && tar -xJC /usr/src/python --strip-components=1 -f /tmp/python.tar.xz \
    && rm /tmp/python.tar.xz

RUN cd /usr/src/python \
    && ./configure \
        --build="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
        --enable-loadable-sqlite-extensions \
        --enable-optimizations \
        --enable-option-checking=fatal \
        --enable-shared \
        --with-lto \
        --with-system-expat \
        --with-system-ffi \
        --without-ensurepip \
    && make -j "$(nproc)" \
    && make install \
    && ldconfig \
    && rm -rf /usr/src/python

RUN cd /usr/local/bin \
    && ln -s idle3 idle \
    && ln -s pydoc3 pydoc \
    && ln -s python3 python \
    && ln -s python3-config python-config

RUN wget -O /tmp/get-pip.py "https://bootstrap.pypa.io/get-pip.py" \
    && python /tmp/get-pip.py --no-cache-dir \
    && rm /tmp/get-pip.py
