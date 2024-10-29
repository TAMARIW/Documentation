This file explains how to setup the raspberry pi for Tamariw. This does not include the setup for the datalink or ORPE parts. This is the first thing to follow when starting from scratch.

# General setup #
- 1. Install raspberry pi imager.
- 2. Flash SDCard with the raspberry pi zero 2w os. Version should be 64 Bit lite. In the settings just before flashing, setup the name (TMW) and password (zero). Use the hostname TMWA for satellite A and TMWB for satellite B. Set in the corresponding tab, to activate the SSH and use password for authentication.
- 3. Plug SDCard into raspberry pi and connect a ethernet adapter to the raspberry pi's micro usb OTG port. Ethernet is required during first boot to enable ethernet access.
- 4. Power up the pi and wait for boot process to complete. Use sudo arp on linux to scan for the ip address of the raspberry pi. (example IP: 10.42.0.10)
- 5. SSH into the pi to continue the setup with: ssh TMW@[IPAddress] e.g ssh TMW@10.42.0.10. Use password zero
- 6. Do an update for the packages with: sudo apt-get -y upgrade
- 7. Install packages required by everything: sudo apt-get -y install cmake git build-essential pkg-config checkinstall libcamera-dev libjpeg-dev libpng-dev libtiff-dev libprotobuf-dev protobuf-compiler libv4l-dev libavcodec-dev libavformat-dev libswscale-dev openocd
- 8. Increase the SWAP to help with compilation: sudo sed -i 's/CONF_SWAPSIZE=200/CONF_SWAPSIZE=2048/g' /etc/dphys-swapfile
- 9. Enable SWAP inscrease: sudo /etc/init.d/dphys-swapfile restart


# Wifi setup #
It is highly recommended that you make a backup, as a mistake in this section could completely block access to the raspberry pi.
The IP address of satellite A will be 192.168.10.1 and B 192.168.10.2.

TAMARIW A:
- 1. stop the network manager process: sudo systemctl stop NetworkManager
- 2. Disable the network manager process: sudo systemctl disable NetworkManager
- 3. Place wifi settings into boot file: sudo nano /etc/rc.local
- 4. Add the following to the file:
```
sudo iwconfig wlan0 mode ad-hoc essid "TMWNetwork" key off channel 1
sudo ifconfig wlan0 192.168.10.1 netmask 255.255.255.0 up
```
- 5. Now save and exit nano.
- 6. Setup ethernet via interface file: sudo nano /etc/network/interfaces
- 7. Add following to the file and save and exit: 
```
auto eth0
iface eth0 inet static
    address 10.42.0.10
    netmask 255.255.255.0
    gateway 10.42.0.1
    dns-nameservers 8.8.8.8 8.8.4.4
```
- 8. Install Internet access package: sudo apt-get install iptables
- 9. Enalbe ip forwarding by uncommenting "net.ipv4.ip_forward=1": sudo nano /etc/sysctl.conf
- 10. Do these commands to enable internet access:
- sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
- sudo iptables -A FORWARD -i wlan0 -o eth0 -j ACCEPT
- sudo iptables -A FORWARD -i eth0 -o wlan0 -m state --state RELATED,ESTABLISHED -j ACCEPT
- sudo apt-get install iptables-persistent
- sudo sh -c "iptables-save > /etc/iptables/rules.v4"
- 11. Reboot: sudo reboot now 

TAMARIW B: 
- 1. stop the network manager process: sudo systemctl stop NetworkManager
- 2. Disable the network manager process: sudo systemctl disable NetworkManager
- 3. Place wifi settings into boot file: sudo nano /etc/rc.local
- 4. Add the following to the file and save and exit:
```
sudo iwconfig wlan0 mode ad-hoc essid "TMWNetwork" key off channel 1
sudo ifconfig wlan0 192.168.10.2 netmask 255.255.255.0 up
sudo route add default gw 192.168.10.1 wlan0
```
- 7. Reboot: sudo reboot now
- 8. Tamariw B will now only be accessable via ssh from inside tamariw A