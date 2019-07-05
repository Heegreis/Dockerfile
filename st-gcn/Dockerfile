FROM heegreis/openpose:no-ffmpeg
# set UTF-8 that can support other language
ENV LANG C.UTF-8

RUN apt-get update
WORKDIR /
# install tools
RUN apt-get -y install wget
# install ffmpeg
RUN mkdir ffmpeg_sources && \
    cd ffmpeg_sources/ && \
    apt -y  remove ffmpeg x264 libav-tools libvpx-dev libx264-dev && \
    apt-get -y install build-essential checkinstall git libfaac-dev libgpac-dev \
        libjack-jackd2-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev \
        librtmp-dev libsdl1.2-dev libtheora-dev libva-dev libvdpau-dev libvorbis-dev \
        libx11-dev libxfixes-dev pkg-config texi2html yasm zlib1g-dev && \
    wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz && \
    tar xzvf yasm-1.3.0.tar.gz && \
    cd yasm-1.3.0 && \
    ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" && \
    make && make install && cd .. && \
    wget http://www.nasm.us/pub/nasm/releasebuilds/2.13.01/nasm-2.13.01.tar.bz2 && \
    tar xjvf nasm-2.13.01.tar.bz2 && \
    cd nasm-2.13.01 && \
    apt-get -y install autoconf && \
    ./autogen.sh && \
    PATH="$HOME/bin:$PATH" ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" && \
    PATH="$HOME/bin:$PATH" make && make install && cd .. && \

    apt-get -y install libx264-dev libx265-dev libfdk-aac-dev libmp3lame-dev libopus-dev libvpx-dev && \
    wget https://downloads.sourceforge.net/freetype/freetype-2.10.0.tar.bz2 && \
    tar jxvf freetype-2.10.0.tar.bz2 && cd freetype-2.10.0 && \
    ./configure --prefix=/usr --enable-freetype-config --disable-static && make && make install && cd .. && \    
    export PKG_CONFIG_PATH=/usr/lib/pkgconfig && \

    wget https://github.com/fribidi/fribidi/releases/download/v1.0.5/fribidi-1.0.5.tar.bz2 && \
    tar jxvf fribidi-1.0.5.tar.bz2 && cd fribidi-1.0.5 && \
    ./configure --prefix=/usr --disable-docs && make && make install && cd .. && \
    
    wget https://www.freedesktop.org/software/fontconfig/release/fontconfig-2.13.1.tar.bz2 && \
    tar jxvf fontconfig-2.13.1.tar.bz2 && cd fontconfig-2.13.1 && \
    apt-get -y install uuid-dev gperf && \
    ./configure --prefix=/usr -disable-docs && make && make install && cd .. && \
    
    git clone https://github.com/libass/libass.git && cd libass && \
    apt-get -y install libtool && \
    sh autogen.sh && \
    ./configure --prefix=/usr --disable-static && make && make install && cd .. \
    export PKG_CONFIG_PATH=/usr/local/ass/lib/pkgconfig:$PKG_CONFIG_PATH && \
    
    git clone --depth 1 https://git.ffmpeg.org/ffmpeg.git && cd ffmpeg && \
    PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure \
        --prefix="$HOME/ffmpeg_build" \
        --pkg-config-flags="--static" \
        --extra-cflags="-I$HOME/ffmpeg_build/include" \
        --extra-ldflags="-L$HOME/ffmpeg_build/lib" \
        --bindir="$HOME/bin" \
        --enable-gpl \
        --enable-libass \
        --enable-libfdk-aac \
        --enable-libfreetype \
        --enable-libmp3lame \
        --enable-libopencore-amrnb \
        --enable-libopencore-amrwb \
        --enable-librtmp \
        --enable-libopus \
        --enable-libtheora \
        --enable-libvorbis \
        --enable-libvpx \
        --enable-libx264 \
        --enable-libx265 \
        --enable-nonfree \
        --enable-version3 \
        --enable-libxcb && \
    PATH="$HOME/bin:$PATH" make && make install && hash -r
# install st-gcn requirements.txt
RUN pip3 install https://download.pytorch.org/whl/cu80/torch-0.4.0-cp35-cp35m-linux_x86_64.whl && \
    pip3 install pyyaml && \
    pip3 install argparse && \
    pip3 install h5py && \
    pip3 install imageio && \
    pip3 install scikit-video && \
    pip3 install opencv-python

WORKDIR /
# 失敗 無法執行