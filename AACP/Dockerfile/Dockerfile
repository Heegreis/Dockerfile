FROM heegreis/opencv-ffmpeg-keras:t1.13

RUN apt-get update
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

WORKDIR /AACP