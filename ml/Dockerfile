FROM zaemyung/cuda:10.2-python3

LABEL maintainer="zaemyung@gmail.com"

ENV LANG=C.UTF-8
ENV SHELL=/bin/bash

ENV LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH

RUN sed -i "s/archive\.ubuntu\.com/mirror\.kakao\.com/g" /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
        libblas-dev \
        liblapack-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir --upgrade \
        pip \
        setuptools \
        wheel

RUN pip3 install --no-cache-dir \
        Cython \
        ipython \
        kaleido \
        matplotlib \
        numpy \
        pandas \
        plotly \
        pyaml \
        requests \
        scikit-learn \
        scipy \
        seaborn \
        torch \
        torchvision \
        tqdm

RUN pip3 install --no-cache-dir --no-index torch-scatter -f https://pytorch-geometric.com/whl/torch-1.7.0+cu102.html
RUN pip3 install --no-cache-dir --no-index torch-sparse -f https://pytorch-geometric.com/whl/torch-1.7.0+cu102.html
RUN pip3 install --no-cache-dir --no-index torch-cluster -f https://pytorch-geometric.com/whl/torch-1.7.0+cu102.html
RUN pip3 install --no-cache-dir --no-index torch-spline-conv -f https://pytorch-geometric.com/whl/torch-1.7.0+cu102.html
RUN pip3 install --no-cache-dir torch-geometric

RUN pip3 install --no-cache-dir pytorch-lightning
