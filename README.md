Intel MIPI ov08x40 sensor driver for Arch Linux 

Install:
```
sudo pacman -Sy git base-devel dkms linux-headers gst-plugin-libcamera pipewire-libcamera libcamera-tools libcamera-ipa v4l2loopback-dkms v4l2loopback-utils
install:

- https://github.com/intel/ipu6-drivers - kernel drivers for the IPU and sensors
- https://github.com/intel/ipu6-camera-bins - IPU firmware and proprietary image processing libraries
- https://github.com/intel/ipu6-camera-hal - HAL for processing of images in userspace
- https://github.com/intel/icamerasrc/tree/icamerasrc_slim_api (branch:icamerasrc_slim_api) - Gstreamer src plugin

git clone https://github.com/henkv1/ov08x40_arch.git
cd ov08x40_arch
sudo dkms add usbio-drivers/
sudo dkms add ov08x40/
sudo dkms autoinstall
sudo cp ov08x40-uf.xml /etc/camera/ipu6epmtl/sensors/ov08x40-uf.xml
cd v4l2-relayd
makepkg -si
sudo systemctl enable v4l2-relayd
echo -e "gpio-usbio\ni2c-usbio\nv4l2loopback" | sudo tee -a /etc/modules-load.d/ov08x40.conf

sudo reboot
```
