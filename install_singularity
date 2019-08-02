#!/bin/bash

export PATH=/usr/local/go/bin:$PATH

go version

export VERSION=3.2.1 && \
    wget --quiet https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-${VERSION}.tar.gz && \
    tar -xzf singularity-${VERSION}.tar.gz && \
    cd singularity

./mconfig && \
    make --silent -C builddir && \
    sudo make -C builddir install
