FROM hub.islab.secom.corp/arg/docker/devel:base

# 更新
RUN set -x && \
    apt-get -qq update && \
    apt-get -qq -y upgrade

# FMT インストール
RUN set -x && \
    cd /tmp/ && \
    git clone -b build https://git.islab.secom.corp/LibraryMirror/fmt.git && \
    mkdir fmt/build && cd fmt/build && \
    cmake .. -G Ninja -DCMAKE_BUILD_TYPE=Release -DFMT_DOC=OFF -DFMT_TEST=OFF && \
    ninja -j`nproc` && ninja install

# Clearn up
RUN set -x && \
    cd ~/ && \
    apt-get -qq -y autoremove && \
    apt-get -qq -y autoclean && \
    apt-get -qq -y clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
