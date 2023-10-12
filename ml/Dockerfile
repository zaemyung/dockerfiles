FROM zaemyung/cuda:12.1-python3.11

LABEL maintainer="zaemyung@gmail.com" \
      org.opencontainers.image.source="https://github.com/zaemyung/dockerfiles"

ENV LANG=C.UTF-8
ENV SHELL=/bin/bash

ENV LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH

RUN apt-get update && apt-get install -y \
        libblas-dev \
        liblapack-dev \
        graphviz \
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

RUN pip3 install --index-url https://download.pytorch.org/whl/cu121 --no-cache-dir \
        torch \
        torchvision \
        torchaudio

RUN pip3 install --no-cache-dir \
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

RUN pip3 install --no-cache-dir \
        torch_geometric

RUN pip3 install --no-cache-dir \
        pyg_lib \
        torch_scatter \
        torch_sparse \
        torch_cluster \
        torch_spline_conv \
        --find-links https://data.pyg.org/whl/torch-2.1.0+cu121.html

