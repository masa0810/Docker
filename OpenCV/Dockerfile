FROM hub.islab.secom.corp/arg/docker/devel:base

# 更新
RUN set -x && \
    apt-get -qq update && \
    apt-get -qq -y upgrade

# OpenCV インストール
RUN set -x && \
    apt-get -qq -y install nvidia-cuda-toolkit \
        pkg-config \
        liblapacke-dev \
        libopenblas-dev \
        libeigen3-dev \
        libtbb-dev \
        libhdf5-serial-dev \
        libgflags-dev libgoogle-glog-dev libceres-dev \
        libfreetype6-dev libharfbuzz-dev \
        protobuf-compiler libprotobuf-dev \
        libavcodec-dev libavformat-dev libavutil-dev libswscale-dev libavresample-dev \
        libdc1394-22-dev \
        libgphoto2-dev \
        libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev \
        libv4l-dev v4l-utils qv4l2 v4l2ucp \
        libva-dev \
        libxine2-dev \
        libgdal-dev libgdcm2-dev && \
    sed -i -e "s/__GNUC__ > 6/__GNUC__ > 7/g" /usr/include/crt/host_config.h && \
    cd /tmp/ && \
    git clone -b build https://git.islab.secom.corp/LibraryMirror/opencv.git && \
    git clone -b build https://git.islab.secom.corp/LibraryMirror/opencv_contrib.git && \
    git clone -b build https://git.islab.secom.corp/LibraryMirror/opencv_3rdparty.git && \
    mkdir opencv/build && cd opencv/build && \
    cmake .. -G Ninja \
        -DBUILD_JASPER=ON \
        -DBUILD_JAVA=OFF \
        -DBUILD_JPEG=ON \
        -DBUILD_OPENEXR=ON \
        -DBUILD_PACKAGE=OFF \
        -DBUILD_PERF_TESTS=OFF \
        -DBUILD_PNG=ON \
        -DBUILD_PROTOBUF=ON \
        -DBUILD_TESTS=OFF \
        -DBUILD_TIFF=ON \
        -DBUILD_WEBP=ON \
        -DBUILD_ZLIB=ON \
        -DBUILD_opencv_apps=OFF \
        -DBUILD_opencv_java_bindings_generator=OFF \
        -DBUILD_opencv_js=OFF \
        -DBUILD_opencv_text=OFF \
        -DBUILD_opencv_ts=OFF \
        -DCMAKE_BUILD_TYPE=Release \
        -DCPU_BASELINE=AVX512_SKX \
        -DCUDA_ARCH_BIN="5.2 6.1" \
        -DCUDA_ARCH_PTX="3.0" \
        -DCUDA_FAST_MATH=ON \
        -DENABLE_CXX11=ON \
        -DENABLE_FAST_MATH=ON \
        -DENABLE_LTO=OFF \
        -DOPENCV_DOWNLOAD_PATH=/tmp/opencv_3rdparty \
        -DOPENCV_ENABLE_NONFREE=ON \
        -DOPENCV_EXTRA_MODULES_PATH=/tmp/opencv_contrib/modules \
        -DPROTOBUF_PROTOC_EXECUTABLE=/usr/bin/protoc \
        -DTINYDNN_USE_TBB=ON \
        -DWITH_GDAL=ON \
        -DWITH_GDCM=ON \
        -DWITH_GPHOTO2=ON \
        -DWITH_LIBV4L=ON \
        -DWITH_MATLAB=OFF \
        -DWITH_OPENCL=ON \
        -DWITH_OPENCLAMDBLAS=OFF \
        -DWITH_OPENCLAMDFFT=OFF \
        -DWITH_PTHREADS_PF=OFF \
        -DWITH_TBB=ON \
        -DWITH_VA=ON \
        -DWITH_XINE=ON && \
    ninja -j`nproc` && ninja install && \
    sed -i -e "s/__GNUC__ > 7/__GNUC__ > 6/g" /usr/include/crt/host_config.h && \
    apt-get -qq -y purge nvidia-cuda-toolkit \
        pkg-config \
        liblapacke-dev \
        libopenblas-dev \
        libeigen3-dev \
        libtbb-dev \
        libhdf5-serial-dev \
        libgflags-dev libgoogle-glog-dev libceres-dev \
        libfreetype6-dev libharfbuzz-dev \
        protobuf-compiler libprotobuf-dev \
        libavcodec-dev libavformat-dev libavutil-dev libswscale-dev libavresample-dev \
        libdc1394-22-dev \
        libgphoto2-dev \
        libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev \
        libv4l-dev v4l-utils qv4l2 v4l2ucp \
        libva-dev \
        libxine2-dev \
        libgdal-dev libgdcm2-dev

# Clearn up
RUN set -x && \
    cd ~/ && \
    apt-get -qq -y autoremove && \
    apt-get -qq -y autoclean && \
    apt-get -qq -y clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
