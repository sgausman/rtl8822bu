# RTL8822BU for Linux

Driver for 802.11ac USB Adapter with RTL8822BU chipset. 
Only STA/Monitor Mode is supported, no AP.  

Forked specifically to compile drivers for Hawking Technologies HW12ACU USB adapter (https://hawkingtech.com/product/hw12acu/) on Ubuntu 16.04 which would not compile with the sourced project. 
Sourced the dkms.conf file from (https://github.com/cilynx/rtl88x2BU_WiFi_linux_v5.3.1_27678.20180430_COEX20180427-5959)

A few other known wireless cards that use this driver include 
* [Edimax EW-7822ULC](http://us.edimax.com/edimax/merchandise/merchandise_detail/data/edimax/us/wireless_adapters_ac1200_dual-band/ew-7822ulc/)
* [ASUS AC-53 NANO](https://www.asus.com/Networking/USB-AC53-Nano/)
* [D-Link DWA-182 (Revision D1 only)](http://ca.dlink.com/products/connect/wireless-ac1200-dual-band-usb-adapter/)


> NOTE: At least v4.7 is needed to compile this module
> sorry people with older kernels, the code is removed.

## DKMS installation

```bash
cd rtl88x2bu
VER=$(sed -n 's/\PACKAGE_VERSION="\(.*\)"/\1/p' dkms.conf)
sudo rsync -rvhP ./ /usr/src/rtl88x2bu-${VER}
sudo dkms add -m rtl88x2bu -v ${VER}
sudo dkms build -m rtl88x2bu -v ${VER}
sudo dkms install -m rtl88x2bu -v ${VER}
sudo modprobe 88x2bu
```

## Normal compiled installation 

Currently tested on X86_64 and ARM platform(s) **only**,  
cross compile possible.

For compiling type  
`make`  
in source dir  

To install the firmware files  
`sudo make install`

To Unload driver you may need to disconnect the device  

If the driver fails building consult your distro how to  
install the kernel sources and build an <u>external</u> module.

## NOTES
This driver allows use of wpa_supplicant by using the nl80211 driver
`wpa_supplicant -Dnl80211`

If installing on Rasberry Pi or other "armv71" devices, edit the Makefile and set `CONFIG_PLATFORM_ARM_RPI = y` and `CONFIG_PLATFORM_I386_PC = n`

## STATUS
Driver works fine (some sort of)  
Most of the work is done is cleaning the driver and make this mess **readable**   for conversion.
Updates for wireless-ext/cfg80211  are not accepted.  
  
## BUGS 
