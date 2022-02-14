FROM zaemyung/ml:latest

LABEL maintainer="zaemyung@gmail.com" \
    org.opencontainers.image.source="https://github.com/zaemyung/dockerfiles"

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --yes --no-install-recommends \
    sudo && rm -rf /var/lib/apt/lists/*

ARG UNAME=zaemyung
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID $UNAME
RUN useradd -m -u $UID -g $GID -s /bin/bash $UNAME
RUN echo $UNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$UNAME && chmod u=r,g=r,o= /etc/sudoers.d/$UNAME
USER $UNAME
