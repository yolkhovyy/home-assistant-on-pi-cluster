# Hardware

## Raspberry Pi

Using Raspberry Pi 3 or 4 with 64-bit Raspbian OS. See [here](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/2) how to prepare SD card.

On all nodes (replace X in rpiX and 192.168.1.1X by node number):

```/etc/dhcpcd.conf
# Inform the DHCP server of our hostname for DDNS.
hostname rpiX
...
# Static IP configuration:
interface eth0
static ip_address=192.168.1.1X/24
static routers=192.168.1.1
static domain_name_servers=8.8.8.8 8.8.4.4
```

## Router

Using TP-Link 8-port Gigabit Desktop Switch.

## Zigbee

[CC2531](https://www.ti.com/product/CC2531) is used as a coordinator.

## C2531 coordinator installation

## How to flash CC2531 USB stick

* Compiled from [here](https://www.zigbee2mqtt.io/guide/adapters/flashing/alternative_flashing_methods.html)
* and [here](https://lemariva.com/blog/2019/08/zigbee-flashing-cc2531-using-raspberry-pi-without-cc-debugger)

On rpi2:

```console
sudo apt install git

wget https://github.com/WiringPi/WiringPi/releases/download/2.61-1/wiringpi-2.61-1-arm64.deb
sudo dpkg -i wiringpi-2.61-1-arm64.deb 
$ gpio -v
gpio version: 2.61

git clone https://github.com/jmichault/flash_cc2531.git
cd flash_cc2531/
make
$ ./cc_chipid 
ID=b524

cd
wget https://github.com/Koenkk/Z-Stack-firmware/archive/master.zip
unzip master.zip 
cd Z-Stack-firmware-master/coordinator/Z-Stack_Home_1.2/bin/default/
unzip CC2531_DEFAULT_20211115.zip 

cd flash_cc2531/
./cc_erase 
./cc_write ~/Z-Stack-firmware-master/coordinator/Z-Stack_Home_1.2/bin/default/CC2531ZNP-Prod.hex 

sudo reboot

$ ls -l /dev/serial/by-id
usb-Texas_Instruments_TI_CC2531_USB_CDC___0X0123456789ABCDEF-if00
```
