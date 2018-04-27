FROM hub.islab.secom.corp/arg/docker/devel:base

# 更新
RUN set -x && \
    apt-get -qq update && \
    apt-get -qq -y upgrade

# Boost インストール
RUN set -x && \
    apt-get -qq -y install \
        libbz2-dev \
        liblzma-dev \
        zlib1g-dev \
        libicu-dev && \
    cd /tmp/ && \
    git clone -b build https://git.islab.secom.corp/LibraryMirror/boost.git && \
    cd boost/ && \
    ./bootstrap.sh --with-icu && \
    ./b2 -j`nproc` link=shared runtime-link=shared threading=multi variant=release --without-python install && \
    apt-get -qq -y purge \
        libbz2-dev \
        liblzma-dev \
        zlib1g-dev \
        libicu-dev

# Clearn up
RUN set -x && \
    cd ~/ && \
    apt-get -qq -y autoremove && \
    apt-get -qq -y autoclean && \
    apt-get -qq -y clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
