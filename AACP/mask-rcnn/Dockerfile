FROM heegreis/aacp:latest

# set UTF-8 that can support other language
ENV LANG C.UTF-8

RUN apt-get -y update && \
    # ==================================================================
    # mask-rcnn dependence
    # ------------------------------------------------------------------
    pip3 install Shapely && \
    pip3 install scipy && \
    pip3 install cython && \
    pip3 install matplotlib && \
    pip3 install scikit-image && \
    pip3 install imgaug && \
    pip3 install jupyter && \
    pip3 install --no-cache-dir git+https://github.com/waleedka/coco.git#subdirectory=PythonAPI

WORKDIR /AACP