FROM heegreis/opencv-ffmpeg:cuda10.0-cudnn7
# set UTF-8 that can support other language
ENV LANG C.UTF-8

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
RUN git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose && \
    cd openpose && \
    git checkout v1.5.0
RUN cd openpose && \
    sed -i 's/78287B57CF85FA89C03F1393D368E5B7) # Body (BODY_25)/d41d8cd98f00b204e9800998ecf8427e) # Body (BODY_25)/' CMakeLists.txt && \
    sed -i 's/e747180d728fa4e4418c465828384333) # Face/d41d8cd98f00b204e9800998ecf8427e) # Face/' CMakeLists.txt && \
    sed -i 's/a82cfc3fea7c62f159e11bd3674c1531) # Hand/d41d8cd98f00b204e9800998ecf8427e) # Hand/' CMakeLists.txt
RUN cd openpose && mkdir build && cd build && \
    cmake -DOpenCV_INCLUDE_DIRS=/usr/local/include/opencv2 \
    -DOpenCV_LIBS_DIR=/usr/local/lib .. && \
    cmake -DOpenCV_CONFIG_FILE=/usr/local/share/OpenCV/OpenCVConfig.cmake .. && \
    cmake -DBUILD_PYTHON=ON ..
RUN cd openpose/build && make -j`nproc`