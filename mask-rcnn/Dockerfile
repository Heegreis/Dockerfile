FROM heegreis/opencv-ffmpeg:cuda10.0-cudnn7

# set UTF-8 that can support other language
ENV LANG C.UTF-8

# install keras
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
    pip3 install openpyxl && \
    # ==================================================================
    # mask-rcnn dependence
    # ------------------------------------------------------------------
    pip3 install Shapely && \
    pip3 install scipy && \
    pip3 install cython && \
    pip3 install matplotlib && \
    pip3 install scikit-image && \
    pip3 install imgaug && \
    pip3 install IPython
    # ==================================================================
    # mask-rcnn
    # ------------------------------------------------------------------
RUN git clone https://github.com/matterport/Mask_RCNN.git && \
    pip3 install --no-cache-dir git+https://github.com/waleedka/coco.git#subdirectory=PythonAPI
