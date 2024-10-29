This guide is for seting up and building the optical sensor (ORPE) section of the raspberry pi

# Prerequirements #
You must install OpenCV before ORPE. Go through the OpenCV setup guide.
In order for ORPE to use the camera, the LCCV library must be installed. Follow these instructions:
- 1. Go into home folder: cd
- 2. clone the repo: git clone https://github.com/kbarni/LCCV.git
- 3. Go into repo folder: cd LCCV
- 4. Create and enter build folder: mkdir build and cd build
- 6. Prepare build: cmake ..
- 7. Build and install via make: sudo make install

# Setting up ORPE #
- 1. Go into home folder: cd
- 2. clone the repo: git clone https://github.com/TAMARIW/ORPE.git
- 3. Go into repo folder: cd ORPE
- 4. Build via build script: ./build.sh

To Run ORPE, simply launch the "ORPE" executable located inside the build folder
- ~/datalinktmw/build/Datalink
