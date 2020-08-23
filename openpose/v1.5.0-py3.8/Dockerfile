FROM cuda-python:3.8-cuda10.0-cudnn7-devel
# set UTF-8 that can support other language
ENV LANG C.UTF-8

RUN apt-get update
# Openpose Prerequisites
RUN apt-get -y install build-essential
RUN apt-get -y install libatlas-base-dev libprotobuf-dev libleveldb-dev libsnappy-dev libhdf5-serial-dev protobuf-compiler
RUN apt-get -y install --no-install-recommends libboost-all-dev
RUN apt-get -y install libgflags-dev libgoogle-glog-dev liblmdb-dev
RUN pip install --upgrade numpy protobuf
RUN apt-get -y install opencl-headers ocl-icd-opencl-dev
RUN apt-get -y install libviennacl-dev
RUN apt-get install -y libopencv-dev
RUN pip install opencv-python

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
    cmake -DBUILD_PYTHON=ON ..
RUN cd openpose/build && make -j`nproc`
RUN cd openpose && rm -rf models
COPY models /openpose/models/
# 成功