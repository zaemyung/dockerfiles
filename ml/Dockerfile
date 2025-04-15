FROM zaemyung/cuda:12.6-python3.12

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

RUN pip3 install --index-url https://download.pytorch.org/whl/cu126 --no-cache-dir \
        torch \
        torchvision \
        torchaudio

RUN pip3 install --no-cache-dir \
        torchmetrics \
        transformers

RUN pip3 install --no-cache-dir \
        torch_geometric

RUN pip3 install --no-cache-dir \
        pyg_lib \
        torch_scatter \
        torch_sparse \
        torch_cluster \
        torch_spline_conv \
        --find-links https://data.pyg.org/whl/torch-2.6.0+cu126.html

RUN pip3 install --no-cache-dir \
        accelerate \
        altair \
        autoawq \
        beautifulsoup4 \
        boto3 \
        chromadb \
        Cython \
        datasets \
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
        spacy \
        streamlit \
        tqdm \
        trl \
        tyro \
        wandb \
        zss
