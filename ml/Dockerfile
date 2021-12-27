FROM zaemyung/cuda:11.3-python3.9

LABEL maintainer="zaemyung@gmail.com" \
      org.opencontainers.image.source="https://github.com/zaemyung/dockerfiles"

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
        altair \
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
        streamlit \
        tensorflow \
        tqdm

RUN pip3 install --no-cache-dir --no-index \
        torch==1.10.1+cu113 \
        torchvision==0.11.2+cu113 \
        torchaudio==0.10.1+cu113 \
        -f https://download.pytorch.org/whl/cu113/torch_stable.html

RUN pip3 install --no-cache-dir --no-index \
        torch-scatter \
        torch-sparse \
        torch-cluster \
        torch-spline-conv \
        torch-geometric \
        -f https://data.pyg.org/whl/torch-1.10.1+cu113.html

RUN pip3 install --no-cache-dir \
        pytorch-lightning \
        torchmetrics \
        transformers