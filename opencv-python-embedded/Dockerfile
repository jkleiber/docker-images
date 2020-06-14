FROM python:3.8.2

WORKDIR /

# Update the repository list
RUN apt-get update

# Install prerequisites
RUN apt-get install -y build-essential cmake unzip pkg-config
RUN apt-get install -y libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
RUN apt-get install -y libxvidcore-dev libx264-dev
RUN apt-get install -y libgtk-3-dev
RUN apt-get install -y libcanberra-gtk*
RUN apt-get install -y libatlas-base-dev gfortran
RUN apt-get install -y python3-dev
RUN python3 -m pip install numpy

# Acquire OpenCV 4.3.0
RUN wget -O opencv.zip https://github.com/opencv/opencv/archive/4.3.0.zip

# Unzip OpenCV
RUN unzip opencv.zip

# Set up the build
WORKDIR /opencv-4.3.0
RUN mkdir build
WORKDIR build

# Build using CMake
RUN cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D ENABLE_NEON=ON \
    -D ENABLE_VFPV3=OFF \
    -D BUILD_TESTS=OFF \
    -D INSTALL_PYTHON_EXAMPLES=OFF \
    -D BUILD_EXAMPLES=OFF ..

# Make
RUN make -j4
RUN make install
RUN ldconfig

# Reset working directory
WORKDIR /
