Forked in order to support the OV01A10 sensor that is in my Dell Precision 5490. Previously camera has barely worked, suffering from low fps and barely and color, but after installing this it works as intended. Many thanks to @henkv1.

Intel MIPI ov01a10 sensor driver for Arch Linux 

Install:
```
sudo pacman -Sy git base-devel dkms linux-headers gst-plugin-libcamera pipewire-libcamera libcamera-tools libcamera-ipa v4l2loopback-dkms v4l2loopback-utils

install the ipu6 icamerasrc drivers and software:
- https://github.com/intel/ipu6-drivers - kernel drivers for the IPU and sensors
- https://github.com/intel/ipu6-camera-bins - IPU firmware and proprietary image processing libraries
- https://github.com/intel/ipu6-camera-hal - HAL for processing of images in userspace
- https://github.com/intel/icamerasrc/tree/icamerasrc_slim_api (branch:icamerasrc_slim_api) - Gstreamer src plugin

git clone https://github.com/Majorklesk/ov01a10_arch_icamerasrc.git
cd ov01a10_arch_icamerasrc
sudo dkms add usbio-drivers/
sudo dkms add ov01a10/
sudo dkms autoinstall
# This step might be redundant, sensor should already be installed when insalling ipu6-camera-hal
sudo cp ov01a10-uf.xml /etc/camera/ipu6epmtl/sensors/ov01a10-uf.xml
cd v4l2-relayd
makepkg -si
sudo systemctl enable v4l2-relayd
echo -e "gpio-usbio\ni2c-usbio\nv4l2loopback" | sudo tee -a /etc/modules-load.d/ov01a10.conf

sudo reboot
```
