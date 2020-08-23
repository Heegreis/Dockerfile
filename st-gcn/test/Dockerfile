# stage 1
FROM openpose:v1.5.0 as openpose

# stage 2
FROM cuda-python:3.8-cuda10.0-cudnn7-runtime as base

## copy openpose and install dependency
WORKDIR /

COPY --from=openpose /openpose/build /openpose/build

RUN apt-get update && apt-get install -y --no-install-recommends \
    libgl1-mesa-glx \
    libglib2.0-0 && \
    rm -rf /var/lib/apt/lists/* && \
    pip install opencv-python

WORKDIR /workspace

# cd /openpose/build/examples/tutorial_api_python/
# python 02_whole_body_from_image.py