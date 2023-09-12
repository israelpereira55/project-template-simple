FROM ubuntu:22.04

# Install necessary packages available from standard repos
RUN apt-get update -qq && export DEBIAN_FRONTEND=noninteractive && \
    apt-get install -y --no-install-recommends \
                    make ninja-build git \
                    python3 python3-pip
#                   software-properties-common wget apt-utils file zip \
#                   openssh-client gpg-agent socat rsync \

RUN python3 -m pip install --upgrade pip setuptools && \
    python3 -m pip install numpy pandas 
#    python3 -m pip install conan && \
#    conan --version

#RUN python3 -m pip install matplotlib (needs apt python3-tk)

# Dependencies
RUN apt-get update -qq && export DEBIAN_FRONTEND=noninteractive && \
    apt-get install -y --no-install-recommends \
                    g++ \
                    libssl-dev libgtest-dev \
                    clang clang-format clang-tidy cppcheck \
                    vim valgrind

# CMake v3.27.4
# Deppends on: openssl (libssl-dev)
RUN mkdir ~/libraries && \
    cd ~/libraries && \
    git clone https://gitlab.kitware.com/cmake/cmake.git && \
    cd cmake && \
    git checkout v3.27.4 && \
    ./bootstrap && \
    make -j8 && \
    make install && \
    rm -rf ~/libraries/cmake/
#    ldconfig

# OpenCV v3.4.16
#RUN cd ~/libraries && \
#    git clone https://github.com/opencv/opencv.git && \
#    git clone https://github.com/opencv/opencv_contrib.git && \
#    cd opencv_contrib && \
#    git checkout 3.4.16  && \
#    cd ../opencv && \
#    git checkout 3.4.16 && \
#    mkdir build && cd build && \
#    cmake -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_INSTALL_PREFIX=/usr/local -DWITH_EIGEN=ON -DOPENCV_GENERATE_PKGCONFIG=ON -DBUILD_SHARED_LIBS=OFF -DOPENCV_EXTRA_MODULES_PATH=~/libraries/opencv_contrib/modules .. && \
#    make -j12 && \
#    make install && \
#    rm -rf ~/libraries/opencv/

# Highly optional
# Adding sudo support
#RUN apt-get update -qq && export DEBIAN_FRONTEND=noninteractive && \
#   apt-get install -y --no-install-recommends \
#                   sudo && \
#   useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo