FROM zaemyung/ml:latest

LABEL maintainer="zaemyung@gmail.com" \
      org.opencontainers.image.source="https://github.com/zaemyung/dockerfiles"

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --yes --no-install-recommends \
    sudo && rm -rf /var/lib/apt/lists/*

ARG UNAME
ARG UID
ARG GID
RUN groupadd -g $GID $UNAME
RUN useradd -m -u $UID -g $GID -s /bin/bash $UNAME
RUN echo $UNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$UNAME && chmod u=r,g=r,o= /etc/sudoers.d/$UNAME
USER $UNAME

# fetch dotfiles
RUN wget "https://raw.githubusercontent.com/zaemyung/dots_public/main/.bash_aliases" -P /home/${UNAME}/
RUN wget "https://raw.githubusercontent.com/zaemyung/dots_public/main/.vimrc" -P /home/${UNAME}/
RUN wget "https://raw.githubusercontent.com/zaemyung/dots_public/main/.tmux.conf" -P /home/${UNAME}/

# install utils
RUN git clone --depth 1 "https://github.com/rupa/z.git" /home/${UNAME}/z

RUN git clone --depth 1 "https://github.com/tmux-plugins/tpm" /home/${UNAME}/.tmux/plugins/tpm
RUN /home/${UNAME}/.tmux/plugins/tpm/scripts/install_plugins.sh

RUN curl -fLo /home/${UNAME}/.vim/autoload/plug.vim --create-dirs "https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim"
RUN yes '' | vim +'PlugInstall --sync' +qa
