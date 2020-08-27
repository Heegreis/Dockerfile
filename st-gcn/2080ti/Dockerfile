# stage 1
FROM heegreis/openpose:v1.5.0-py3.6-2080ti as openpose

# stage 2
FROM heegreis/cuda-python:3.6-cuda10.0-cudnn7-runtime as base
## set UTF-8 that can support other language
ENV LANG C.UTF-8

## copy openpose and install dependency
WORKDIR /

COPY --from=openpose /openpose/build /openpose/build

COPY --from=openpose /openpose/models /openpose/models

COPY --from=openpose /openpose/examples/media /openpose/examples/media

RUN apt-get update && apt-get install -y --no-install-recommends \
    libgl1-mesa-glx \
    libglib2.0-0 \
    libgflags-dev \
    libopencv-dev \
    libgoogle-glog-dev \
    libboost-all-dev \
    libprotobuf-dev \
    libhdf5-serial-dev \
    libatlas-base-dev && \
    rm -rf /var/lib/apt/lists/* && \
    pip install opencv-python && \
## install st-gcn dependency
    pip install pyyaml \
    argparse \
    numpy \
    h5py \
    imageio \
    scikit-video && \
    # conda install pytorch==1.2.0 torchvision==0.4.0 cudatoolkit=10.0 -c pytorch
    pip install torch==1.2.0 torchvision==0.4.0


WORKDIR /workspace