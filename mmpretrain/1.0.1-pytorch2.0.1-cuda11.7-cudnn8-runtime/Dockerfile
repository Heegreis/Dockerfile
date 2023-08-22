FROM heegreis/open-mmlab-ubuntu-requirement:pytorch2.0.1-cuda11.7-cudnn8-runtime

# Install MIM
RUN pip install openmim

# Install MMPretrain
RUN conda clean --all
RUN git clone https://github.com/open-mmlab/mmpretrain.git
WORKDIR ./mmpretrain
RUN git checkout v1.0.1
RUN mim install --no-cache-dir -e .