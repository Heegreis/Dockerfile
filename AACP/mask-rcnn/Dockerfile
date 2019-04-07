FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04
ENV OPENCV_VERSION 3.4.2

# set UTF-8 that can support other language
ENV LANG C.UTF-8

# Install all dependencies for OpenCV
RUN apt-get -y update && \
    apt-get -y install \
        python3 \
        python3-dev \
        git \
        wget \
        unzip \
        cmake \
        build-essential \
        pkg-config \
        libatlas-base-dev \
        gfortran \
        libjasper-dev \
        libgtk2.0-dev \
        libavcodec-dev \
        libavformat-dev \
        libswscale-dev \
        libjpeg-dev \
        libpng-dev \
        libtiff-dev \
        libjasper-dev \
        libv4l-dev \
    && \
# install python dependencies
    wget https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py && \
    rm get-pip.py && \
    # imgaug have to install before opencv and ffmpeg
    pip3 install imgaug && \
    pip3 install numpy \
    && \
# Install OpenCV
    wget https://github.com/opencv/opencv/archive/$OPENCV_VERSION.zip -O opencv3.zip && \
    unzip -q opencv3.zip && \
    mv /opencv-$OPENCV_VERSION /opencv && \
    rm opencv3.zip && \
    wget https://github.com/opencv/opencv_contrib/archive/$OPENCV_VERSION.zip -O opencv_contrib3.zip && \
    unzip -q opencv_contrib3.zip && \
    mv /opencv_contrib-$OPENCV_VERSION /opencv_contrib && \
    rm opencv_contrib3.zip \
    && \
# Prepare build
    mkdir /opencv/build && cd /opencv/build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE \
      -D BUILD_PYTHON_SUPPORT=ON \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D OPENCV_EXTRA_MODULES_PATH=/opencv_contrib/modules \
      -D BUILD_EXAMPLES=OFF \
      -D PYTHON_DEFAULT_EXECUTABLE=/usr/bin/python3 \
      -D BUILD_opencv_python3=ON \
      -D BUILD_opencv_python2=OFF \
      -D WITH_IPP=OFF \
      -D WITH_FFMPEG=ON \
      -D WITH_CUDA=ON \
      -D CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-10.0 \
      -D WITH_CUBLAS=ON \
      -D WITH_V4L=ON .. \
    && \
# Install
    cd /opencv/build && \
    make -j$(nproc) && \
    make install && \
    ldconfig \
    && \
# Clean
   apt-get -y remove \
        python3-dev \
        libatlas-base-dev \
        gfortran \
        libjasper-dev \
        libgtk2.0-dev \
        libavcodec-dev \
        libavformat-dev \
        libswscale-dev \
        libjpeg-dev \
        libpng-dev \
        libtiff-dev \
        libjasper-dev \
        libv4l-dev \
    && \
    apt-get clean && \
    rm -rf /opencv /opencv_contrib /var/lib/apt/lists/*
# install keras and AACP
RUN apt-get -y update && \
    # ==================================================================
    # tensorflow
    # ------------------------------------------------------------------
    pip3 install tensorflow-gpu==1.13.1 && \
    # ==================================================================
    # keras
    # ------------------------------------------------------------------
    pip3 install h5py && \
    pip3 install keras==2.2.4 && \
    # ==================================================================
    # python
    # ------------------------------------------------------------------
    pip3 install Pillow && \
    pip3 install scikit-learn && \
    pip3 install openpyxl

# Openpose Prerequisites
RUN apt-get -y install build-essential
RUN apt-get -y install libatlas-base-dev libprotobuf-dev libleveldb-dev libsnappy-dev libhdf5-serial-dev protobuf-compiler
RUN apt-get -y install --no-install-recommends libboost-all-dev
RUN apt-get -y install libgflags-dev libgoogle-glog-dev liblmdb-dev
RUN apt-get -y install python3-setuptools python3-dev build-essential
RUN pip3 install --upgrade numpy protobuf
RUN apt-get -y install opencl-headers ocl-icd-opencl-dev
RUN apt-get -y install python3-pip
RUN apt-get -y install libviennacl-dev
# Openpose Build
WORKDIR /
RUN git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
RUN cd openpose && mkdir build && cd build && \
    cmake -DOpenCV_INCLUDE_DIRS=/usr/local/include/opencv2 \
    -DOpenCV_LIBS_DIR=/usr/local/lib .. && \
    cmake -DOpenCV_CONFIG_FILE=/usr/local/share/OpenCV/OpenCVConfig.cmake .. && \
    cmake -DBUILD_PYTHON=ON ..
RUN cd openpose/build && make -j`nproc`
# install face dependence
RUN pip3 install face_recognition && \
    pip3 install imutils && \
    pip3 install dlib && \
    pip3 install pandas && \
    pip3 install matplotlib && \
    # ==================================================================
    # mask-rcnn dependence
    # ------------------------------------------------------------------
    pip3 install Shapely && \
    pip3 install scipy && \
    pip3 install cython && \
    pip3 install matplotlib && \
    pip3 install scikit-image && \
    pip3 install jupyter && \
    pip3 install --no-cache-dir git+https://github.com/waleedka/coco.git#subdirectory=PythonAPI

WORKDIR /AACP