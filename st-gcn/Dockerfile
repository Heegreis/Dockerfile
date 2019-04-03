FROM heegreis/opencv-ffmpeg:cuda8.0-cudnn7
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
    git checkout v1.4.0
RUN cd openpose && mkdir build && cd build && \
    cmake -DOpenCV_INCLUDE_DIRS=/usr/local/include/opencv2 \
    -DOpenCV_LIBS_DIR=/usr/local/lib .. && \
    cmake -DOpenCV_CONFIG_FILE=/usr/local/share/OpenCV/OpenCVConfig.cmake .. && \
    cmake -DBUILD_PYTHON=ON ..
RUN cd openpose/build && make -j`nproc`

# install st-gcn
RUN pip3 install https://download.pytorch.org/whl/cu80/torch-0.4.0-cp35-cp35m-linux_x86_64.whl && \
    pip3 install pyyaml && \
    pip3 install argparse && \
    pip3 install h5py && \
    pip3 install imageio && \
    pip3 install scikit-video

# install other python liberary
RUN pip3 install Pillow

WORKDIR /AACP