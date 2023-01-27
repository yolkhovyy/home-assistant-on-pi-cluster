# Hardware

## Raspberry Pi

* Raspberry Pi 3 or 4 with 64-bit Raspbian OS
* Use [RPi Imager](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/2) to prepare SD card 

**Further X means node number**

* rpiX: replace X by node number
* 192.168.1.1X: replace X by node number

**Enable ssh, set username/password on OS 64**

    ```bash
    sudo touch /media/yo/boot/ssh
    echo YOUR_PASSWORD | openssl passwd -6 -stdin > /media/yo/boot/userconf
    # Single line, no spaces, crlf at the end
    # pi:hash
    ```

**/etc/hostname**

    ```conf
    rpiX
    ```

**/etc/hosts**

    ```conf
    127.0.0.1 localhost
    127.0.1.1 rpiX
    ...
    192.168.1.11 rpi1
    192.168.1.12 rpi2
    192.168.1.13 rpi3
    192.168.1.14 rpi4
    192.168.1.14 rpi5
    ```

**/etc/dhcpcd.conf**

    ```conf
    # Inform the DHCP server of our hostname for DDNS.
    hostname rpiX
    ...
    # Static IP configuration:
    interface eth0
    static ip_address=192.168.1.1X/24
    static routers=192.168.1.1
    static domain_name_servers=8.8.8.8 8.8.4.4
    ```

**/etc/fstab**

This saves the SD card from wearing.

    ```conf
    tmpfs /tmp tmpfs     defaults,noatime,nosuid,nodev,noexec,mode=0755,size=100m 0 0
    tmpfs /var/tmp tmpfs defaults,noatime,nosuid,nodev,noexec,mode=0755,size=30m 0 0
    tmpfs /var/log tmpfs defaults,noatime,nosuid,nodev,noexec,mode=0755,size=100m 0 0
    ```

**Install SD cards in PIs, boot**

**Remove old ssh keys**

On your PC:

    ```bash
    ssh-keygen -R rpiX
    ssh-keygen -R 192.168.1.1X
    ```

**Generate new ssh key**

On your PC:

    ```bash
    $ ssh-keygen
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/yo/.ssh/id_rsa): /home/yo/.ssh/id_rpi
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in /home/yo/.ssh/id_rpi.
    Your public key has been saved in /home/yo/.ssh/id_rpi.pub.
    ```

**Copy key to Pis**

On your PC, copy teh key to all nodes:

    ```bash
    ssh-copy-id -i ~/.ssh/id_rpi pi@rpiX
    ```

**~/.ssh/config**

On your PC:

    ```bash
    Host rpiX
        HostName rpiX
        PreferredAuthentications publickey
        IdentityFile ~/.ssh/id_rpi
        User pi
    ```

Restart ssh service on your PC:
    
    ```bash
    sudo service ssh restart
    ```

## Ethernet Switch

* TP-Link 8-port Gigabit Desktop Switch

## Zigbee

### C2531 coordinator installation

[CC2531](https://www.ti.com/product/CC2531) is used as a coordinator.

#### How to flash CC2531 USB stick

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
