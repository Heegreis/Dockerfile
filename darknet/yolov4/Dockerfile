FROM heegreis/cuda-python:3.6-cuda10.1-cudnn7-devel-ubuntu18.04

# set UTF-8 that can support other language
ENV LANG C.UTF-8

RUN apt-get update && apt-get install -y --no-install-recommends \
        git \
        wget \
        # opencv dependencies
        cmake \
        build-essential pkg-config libgtk-3-dev \
        libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
        libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev \
        gfortran openexr libatlas-base-dev \
        libtbb2 libtbb-dev libdc1394-22-dev \
        && \
     rm -rf /var/lib/apt/lists/*

WORKDIR /

# use commit 14b196d4f2f73fb2f6f8c4019de9a0de00c5a27e
RUN git clone https://github.com/AlexeyAB/darknet.git && \
    cd /darknet && \
    git checkout 8297b1be3108f47d82b97d322d5f1aef5150018f && \
    wget https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.weights && \
    sed -i 's/OPENCV=0/OPENCV=1/' Makefile && \
    sed -i 's/GPU=0/GPU=1/' Makefile && \
    sed -i 's/CUDNN=0/CUDNN=1/' Makefile && \
    sed -i 's/CUDNN_HALF=0/CUDNN_HALF=1/' Makefile && \
    sed -i 's/LIBSO=0/LIBSO=1/' Makefile

# opencv build
RUN mkdir /opencv_build && cd /opencv_build && \
    git clone https://github.com/opencv/opencv.git && \
    cd opencv && git checkout 4.5.0 && cd .. && \
    git clone https://github.com/opencv/opencv_contrib.git && \
    cd opencv_contrib && git checkout 4.5.0
    
RUN cd /opencv_build/opencv && \
    mkdir build && cd build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
        -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D OPENCV_GENERATE_PKGCONFIG=ON \
        -D OPENCV_EXTRA_MODULES_PATH=/opencv_build/opencv_contrib/modules \
        -D BUILD_EXAMPLES=OFF \
        -D WITH_FFMPEG=ON \
        -D WITH_CUBLAS=ON .. && \
    make -j$(nproc) && \
    make install && \
    ldconfig

RUN cd /darknet && make

RUN pip install opencv-python

WORKDIR /darknet