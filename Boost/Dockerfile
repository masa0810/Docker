FROM nvidia/cuda:9.1-cudnn7-devel

# Install dependencies
RUN set -x && \
    apt-get -qq update && \
    apt-get -qq upgrade && \
    apt-get -qq -y install git && \
    apt-get -qq -y install libicu-dev libbz2-dev zlib1g-dev liblzma-dev

# Boost Build
RUN set -x && \
    cd /tmp/ && \
    git clone --recursive https://github.com/boostorg/boost.git -b boost-1.66.0 && \
    cd boost/ && \
    ./bootstrap.sh && \
    ./b2 -j`grep processor /proc/cpuinfo | wc -l` cxxflags="-std=c++14" linkflags="-std=c++14" install

# Clearn up
RUN set -x && \
    cd ~/ && \
    apt-get -qq -y purge git && \
    apt-get -qq -y autoclean && \
    apt-get -qq -y clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*