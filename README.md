# Android 6.0.1 for RADAR

## Downloading Android image
Follow this [link](http://geektillithertz.com/wordpress/index.php/2016/06/26/androidpi3cpugpu-update/) for downloading the 
tar archive within the Android image.

## Installing Android image on Mac OS
### Formatting SD card
We need a SD card formatted with FAT32 file system.
* Open Disk Utility
* Select the device. In my case **Apple SDXC Reader Media**
* Click Erase
* Select **MS-DOS (FAT)** as format and **GUID Partition Map** as scheme
* Click **Erase**
![Disk Utility image](https://github.com/KHP-Informatics/RADAR-Pi3/blob/master/images/diskutility.png)

### Installation
* Open a terminal and run `df -h`
* Connect the SD card reader with the SD card inside
* Run `df -h` and look for the new device that was not listed before. In my case the device is `/dev/disk2s1`
* Unmount the partition `sudo diskutil unmount <partition>`. In my case `sudo diskutil unmount /dev/disk2s1`
* Infer the device name raw from the partition, removing the final **s1** and adding a **r**. Therefore `/dev/disk2s1` becomes `/dev/rdisk2`
* Write the image to the card `sudo dd bs=1m if=2<img-path> of=<raw-name>`. In my case `sudo dd bs=1m if=Desktop/andrpi3-20160626.img of=/dev/rdisk2`. This command does not provide any information until the end.
* When `dd` command terminates, eject the device running `sudo diskutil eject <raw-name>`. In my case `sudo diskutil eject /dev/rdisk2`
![Terminal result](https://github.com/KHP-Informatics/RADAR-Pi3/blob/master/images/terminalresult.png)

### Setting up Pi3
* Connect mouse and keyboard by USB
* Connect the HDMI cable
* Insert the SD card containing the OS
* Connect the power adaptor
* Android will automatically boot
### Setting up Android
* Go to Settings > Wi-Fi
* Sign in on your Wi-Fi connection
* Go to Settings > Developer options
* Enable **USB debugging**
* Go to About tablet > Status > IP address and note down Pi3's IP
* Connect your laptop to the same network of Pi
* Open a terminal and run `./adb connect <Pi3-IP>:5555`. You are now ready run and debug your Android application on Pi3
* Alternatively, on your terminal run `./adb shell ip -f inet addr show wlan0`. This command automatically finds the IP of your Pi3
* For shutting down your Pi3 open a terminal and run `./adb shell reboot -p`

## Installing Android image on Windows
See the [video](https://www.youtube.com/watch?v=ddVY6OEpZlU) until 5:10 minute

## Installing Android image on Ubuntu
See the [video](https://www.youtube.com/watch?v=aSgQDhM84Ko)

## Sources
* [Android iso](http://geektillithertz.com/wordpress/index.php/2016/06/26/androidpi3cpugpu-update/) 
* [Android developer repository](https://github.com/peyo-hd)
* [Set up SD card](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)
