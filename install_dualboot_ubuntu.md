# Install Ubuntu 16.04 in dual boot with Windows 10
Follow the instructions from [How to install Ubuntu from USB (Official Dell Tech Support)](https://youtu.be/RW9UWDOJjL4).

## Prepare Ubuntun iso
Download the Ubuntu iso file from [Ubuntu](https://www.ubuntu.com/download/desktop).  
In my case, I downloaded ***ubuntu-16.04.6-desktop-amd64.iso*** from [Ubuntu 16.04.6 LTS](http://releases.ubuntu.com/16.04/) (recommended) instead of the latest version.

## Create recovery drive by Dell OS Recovery Tool
1. Download [Dell OS Recovery Tool](http://downloads.dell.com/MediaCreationUtility/DellOSRecoveryTool.msi)
2. Insert a flash drive and follow the steps to create a recovery drive of Ubuntu 16.04.

### Troubleshooting
* The Recovery Tool has an error when trying to create recovery drive with Ubuntu 18.04.
Instead of using Ubuntu 18.04, I used Ubuntu 16.04. Close the Recovery Tool and try again if error occurs while creating recovery drive of Ubuntu 16.04.

## Install Ubuntu 16.04
1. Insert recovery drive of Ubuntu 16.04 and reboot the machine.
2. Keep clicking F12 while rebooting to enter the boot menu. Select one of the options under "UEFI boot" that boots with flash drive. You might need to change settings in the boot menu if there no option that boots with flash drive under "UEFI boot".
3. In the Ubuntu boot menu, choose "Try Ubuntu without installing". Install Ubuntu 16.04 with the installation file appears on the desktop.
