FROM heegreis/aacp:openpose

RUN apt-get update
# install face dependence

# Openpose Build

RUN pip3 install face_recognition && \
    pip3 install imutils && \
    pip3 install dlib && \
    pip3 install pandas && \
    pip3 install matplotlib

WORKDIR /AACP