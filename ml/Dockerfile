FROM zaemyung/cuda:13.0-python3.13

LABEL maintainer="zaemyung@gmail.com" \
      org.opencontainers.image.source="https://github.com/zaemyung/dockerfiles"

ENV LANG=C.UTF-8
ENV SHELL=/bin/bash

ENV LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH

RUN apt-get update && apt-get install -y \
        ccache \
        graphviz \
        libaio1 \
        libblas-dev \
        liblapack-dev \
        numactl \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir --upgrade \
        pip \
        setuptools \
        wheel

RUN pip3 install --index-url https://download.pytorch.org/whl/cu130 --no-cache-dir \
        torch \
        torchvision \
        torchaudio

RUN pip3 install --no-cache-dir \
        accelerate \
        altair \
        autoawq \
        beautifulsoup4 \
        boto3 \
        chromadb \
        Cython \
        datasets \
        deepspeed \
        evaluate \
        guidance \
        htbuilder \
        ipython \
        kaleido \
        matplotlib \
        natsort \
        networkx \
        nltk \
        numpy \
        pandas \
        parsimonious \
        peft \
        plotly \
        pyaml \
        pygraphviz \
        python-dotenv \
        python-notification \
        PyYAML \
        regex \
        requests \
        rich \
        rouge_score \
        sacrebleu \
        scikit-learn \
        scipy \
        seaborn \
        sentence-transformers \
        sentencepiece \
        sentsplit \
        sglang \
        spacy \
        streamlit \
        torchmetrics \
        tqdm \
        transformers \
        tyro \
        wandb \
        zss
