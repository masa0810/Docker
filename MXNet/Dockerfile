FROM hub.islab.secom.corp/arg/docker/devel:opencv

# 更新
RUN set -x && \
    apt-get -qq update && \
    apt-get -qq -y upgrade

# MXNet インストール
RUN set -x && \
    apt-get -qq -y install nvidia-cuda-toolkit \
        pkg-config \
        libjemalloc-dev \
        libopenblas-dev \
        python3 \
        wget \
        libgdal20 \
        libgdcm2.8 \
        libtbb2 \
        libva2 && \
    sed -i -e "s/__GNUC__ > 6/__GNUC__ > 7/g" /usr/include/crt/host_config.h && \
    cd /tmp/ && \
    wget http://islmirror.islab.secom.corp/repo/software/windows/NVIDIA/cudnn-9.1-linux-x64-v7.1.tgz && \
    tar xvf cudnn-9.1-linux-x64-v7.1.tgz && \
    cp cuda/include/* /usr/local/include/ && \
    cp -R cuda/lib64/* /usr/local/lib/ && \
    git clone -b build https://git.islab.secom.corp/LibraryMirror/incubator-mxnet.git mxnet && \
    mkdir mxnet/build && cd mxnet/build && \
    cmake .. -G Ninja \
        -DBUILD_SHARED_LIBS=ON \
        -DBUILD_TESTING=OFF \
        -DBUILD_TESTING=OFF \
        -DCMAKE_BUILD_TYPE=Release \
        -DCUDA_ARCH_BIN="52 61" \
        -DCUDA_ARCH_NAME="Manual" \
        -DCUDA_ARCH_PTX="30" \
        -DENABLE_CUDA_RTC=OFF \
        -DUSE_GPERFTOOLS=OFF \
        -DUSE_OLDCMAKECUDA=ON \
        -DUSE_OPENMP=OFF && \
    ninja -j`nproc` && ninja install && \
    sed -i -e "s/__GNUC__ > 7/__GNUC__ > 6/g" /usr/include/crt/host_config.h && \
    apt-get -qq -y purge nvidia-cuda-toolkit \
        pkg-config \
        libjemalloc-dev \
        libopenblas-dev \
        python3 \
        wget \
        libgdal20 \
        libgdcm2.8 \
        libtbb2 \
        libva2

# Clearn up
RUN set -x && \
    cd ~/ && \
    apt-get -qq -y autoremove && \
    apt-get -qq -y autoclean && \
    apt-get -qq -y clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
