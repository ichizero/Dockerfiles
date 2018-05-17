FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

LABEL maintainer="ichizero"

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    python3-dev \
    python3-pip \
    python3-wheel \
    python3-setuptools && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

RUN pip3 install --no-cache-dir \
    cupy-cuda90 \
    chainer


RUN apt-get update

RUN apt-get install -y \
  cmake \
  wget \
  unzip

# ref) http://www.python36.com/how-to-install-opencv340-on-ubuntu1604/
RUN apt-get install -y build-essential
RUN apt-get install -y \
  git \
  libgtk2.0-dev \
  pkg-config \
  libavcodec-dev \
  libavformat-dev \
  libswscale-dev

# To process images
RUN apt-get install -y \
  python-dev \
  python-numpy \
  libtbb2 \
  libtbb-dev \
  libjpeg-dev \
  libpng-dev \
  libtiff-dev \
  libjasper-dev \
  libdc1394-22-dev

# To process videos
RUN apt-get install -y \
  libavcodec-dev \
  libavformat-dev \
  libswscale-dev \
  libv4l-dev
RUN apt-get install -y \
  libxvidcore-dev \
  libx264-dev

# For GUI
RUN apt-get install -y libgtk-3-dev

# For optimization
RUN apt-get install -y libatlas-base-dev gfortran pylint

# To build OpenCV binding for both python 2 and 3
RUN apt-get install -y python2.7-dev python3-dev

# Python dependencies
RUN pip3 --no-cache-dir install \
  numpy \
  hdf5storage \
  h5py \
  scipy \
  py3nvml

WORKDIR /
RUN wget https://github.com/opencv/opencv/archive/3.4.0.zip -O opencv-3.4.0.zip \
  && wget https://github.com/opencv/opencv_contrib/archive/3.4.0.zip -O opencv_contrib-3.4.0.zip \
  && unzip -q opencv-3.4.0.zip \
  && unzip -q opencv_contrib-3.4.0.zip \
  && cd opencv-3.4.0 \
  && mkdir build \
  && cd build \
  && cmake -DCMAKE_BUILD_TYPE=RELEASE \
  -DCMAKE_INSTALL_PREFIX=/usr/local \
  -DOPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-3.4.0/modules \
  -DBUILD_TIFF=ON \
  -DBUILD_opencv_java=OFF \
  -DWITH_CUDA=OFF \
  -DENABLE_AVX=ON \
  -DWITH_OPENGL=ON \
  -DWITH_OPENCL=ON \
  -DWITH_IPP=ON \
  -DWITH_TBB=ON \
  -DWITH_EIGEN=ON \
  -DWITH_V4L=ON \
  -DBUILD_TESTS=OFF \
  -DBUILD_PERF_TESTS=OFF \
  -DBUILD_opencv_python3=yes \
  -DPYTHON_EXECUTABLE=$(which python3) \
  -DPYTHON_INCLUDE_DIR=$(python3 -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())") \
  -DPYTHON_PACKAGES_PATH=$(python3 -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())") .. \
  && make -j8 \
  && make install \
  && rm /opencv-3.4.0.zip \
  && rm /opencv_contrib-3.4.0.zip \
  && rm -r /opencv-3.4.0 \
  && rm -r /opencv_contrib-3.4.0

RUN apt-get install -y x11-apps \
  python3-tk

RUN apt-get clean

RUN pip3 install  --no-cache-dir \
  cython \
  argparse \
  matplotlib
