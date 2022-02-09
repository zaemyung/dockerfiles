FROM zaemyung/ml:latest

LABEL maintainer="zaemyung@gmail.com" \
      org.opencontainers.image.source="https://github.com/zaemyung/dockerfiles"

ARG UNAME=zaemyung
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID $UNAME
RUN useradd -m -u $UID -g $GID -s /bin/bash $UNAME
USER $UNAME
