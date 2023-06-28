FROM zaemyung/cuda:11.7.1-python3.10

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
        beautifulsoup4 \
        boto3 \
        Cython \
        htbuilder \
        ipython \
        kaleido \
        matplotlib \
        networkx \
        numpy \
        pandas \
        plotly \
        pyaml \
        python-dotenv \
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
        torchmetrics

RUN pip3 install --no-cache-dir \
        transformers

RUN pip3 install --no-cache-dir \
        datasets \
        nltk \
        rouge_score \
        sacrebleu \
        sentencepiece \
        sentsplit \
        spacy

# Deep Graph Library (DGL)
RUN pip3 install --no-cache-dir --find-links https://data.dgl.ai/wheels/cu117/repo.html \
        dgl

RUN pip3 install --no-cache-dir --find-links https://data.dgl.ai/wheels-test/repo.html \
        dglgo