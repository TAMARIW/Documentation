This guide explains how to setup and compile OpenCV from scratch. Optionally you can also follow the quickstart guide to install a precompiled package.

Quickstart Guide with precompiled package:
- 1. Find the raspberry pis IP Address.
- 2. Copy the OpenCV Package from the packages folder: scp ./Packages/opencv-install.tar.gz TMW@[IPAddress]:~/
- 3. Install package while ssh inside the raspberry pi: sudo tar -xvpzf /home/TMW/opencv-install.tar.gz

How to compile and install from scratch:
- 1. Go into home directory: cd
- 2. Create the Main directory: mkdir OpenCV / cd OpenCV
- 3. Clone repo: git clone https://github.com/opencv/opencv.git --branch 4.9.0
- 4. mkdir build / cd build
- 5. Prepare build with CMake: cmake -DENABLE_NEON=ON -DBUILD_TESTS=OFF -DCMAKE_BUILD_TYPE=Release -DBUILD_EXAMPLES=OFF -DBUILD_opencv_apps=OFF -DBUILD_DOCS=OFF -DBUILD_PERF_TESTS=OFF -DWITH_TBB=ON -DWITH_OPENMP=ON -DWITH_IPP=OFF -DENABLE_FAST_MATH=ON ../opencv
- 6. Build OpenCV: make -j 2
- 7. Install: sudo make install


