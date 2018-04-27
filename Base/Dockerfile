FROM hub.islab.secom.corp/arg/docker/ubuntu

# 開発ツールインストール
RUN set -x && \
    apt-get -qq update && \
    apt-get -qq -y upgrade && \
    apt-get -qq -y install build-essential

# Git インストール
RUN set -x && \
    apt-get -qq -y install git && \
    git config --global http.sslVerify false

# CCache インストール
RUN set -x && \
    apt-get -qq -y install ccache && \
    echo export USE_CCACHE=1 >> ~/.bashrc && \
    echo export CCACHE_DIR=/tmp/ccache >> ~/.bashrc

# Ninja インストール
RUN set -x && \
    apt-get -qq -y install re2c python3 && \
    ln -s `which python3` /usr/local/bin/python && \
    cd /tmp/ && \
    git clone -b build https://git.islab.secom.corp/LibraryMirror/ninja.git && \
    cd ninja/ && \
    ./configure.py --bootstrap && \
    cp ninja /usr/local/bin/ && \
    rm /usr/local/bin/python && \
    apt-get -qq -y purge re2c python3

# Cmake インストール
RUN set -x && \
    apt-get -qq -y install libncurses5-dev && \
    cd /tmp/ && \
    git clone -b build https://git.islab.secom.corp/LibraryMirror/cmake.git && \
    cd cmake/ && \
    ./bootstrap --parallel=`nproc` --enable-ccache && \
    make -j`nproc` && make install && \
    apt-get -qq -y purge libncurses5-dev

# Clearn up
RUN set -x && \
    cd ~/ && \
    apt-get -qq -y autoremove && \
    apt-get -qq -y autoclean && \
    apt-get -qq -y clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
