FROM zaemyung/cuda:11.3.1-python3.9

LABEL maintainer="zaemyung@gmail.com" \
      org.opencontainers.image.source="https://github.com/zaemyung/dockerfiles"

ENV LANG=C.UTF-8
ENV SHELL=/bin/bash

ENV LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH

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
        htbuilder \
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
        tqdm \
        wandb

RUN pip3 install --no-cache-dir \
        torch \
        torchvision \
        torchaudio \
        -f https://download.pytorch.org/whl/cu113

RUN pip3 install --no-cache-dir \
        torch-scatter \
        torch-sparse \
        torch-cluster \
        torch-spline-conv \
        torch-geometric \
        -f https://data.pyg.org/whl/torch-1.11.0+cu113.html

RUN pip3 install --no-cache-dir \
        pytorch-lightning \
        torchmetrics \
        transformers

RUN pip3 install --no-cache-dir \
        datasets \
        nltk \
        rouge_score \
        sacrebleu \
        sentencepiece \
        sentsplit \
        spacy
