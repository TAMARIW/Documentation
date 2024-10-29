This guide will explain how to compile and flash the STM32.

# Prerequirements #
This guide is for linux systems.
You must have the arm toolchain for the STM32F4 installed. Usually available via package manager like apt, dnf or yum.
CMake and make are also required for the build process.

# How to setup #
- 1. Clone project: git clone https://gitlab.com/chst15/tamariw/stm32tmw.git
- 2. Go into folder: cd stm32tmw
- 3. Init submodules: git submodule init
- 4. Update submodules: git submodule update

# How to build #
Use the build.sh script to build. Append the type of toolchain/platform to build for (e.g skith, discovery posix). 
For TAMARIW: ./build.sh skith

# How to flash #\
For flashing we have two options. Either over wifi using the tamariw raspberry pi or over usb via the debug connector. 
WiFi requires an ethernet connection a satellite and their IP addresses must be known. Due to the ADHOC setup, flashing the satellite that is not connected over ethernet, requires a proxy. So either we flash from C -> A (host to tamariw A) or C -> A -> B (host to B over A). The IP address of B is then the IP adress in the adhoc network
For usb: ./upload.sh USB
For wifi C -> A: ./upload.sh TMW [IPADDRESS]
For wifi C -> A -> B: ./upload.sh TMW [IPADDRESS OF A] TMW [IPADDRESS OF B]

Example for wifi C -> A -> B: ./upload.sh TMW 10.42.0.10 TMW 192.168.10.2
Here 10.42.0.10 is the IP adress of the satellite connected to the host and 192.168.10.2 the ip adress of the satellite connected over the adhoc network.