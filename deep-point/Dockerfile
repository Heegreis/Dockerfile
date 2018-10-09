
FROM ufoym/deepo:all-py36

RUN add-apt-repository ppa:v-launchpad-jochen-sprickerhof-de/pcl && \
    apt-get update; exit 0
RUN apt-get -y install libpcl-dev && \
    apt-get -y install libproj-dev && \
    git clone https://github.com/PointCloudLibrary/pcl.git && \
    cd pcl && mkdir build && cd build && \
    cmake -DCMAKE_BUILD_TYPE=Release .. && \
    make -j2 && \
    make -j2 install
