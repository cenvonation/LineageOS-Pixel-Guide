# Welcome!
This is an unofficial guide to install Lineage OS on a Pixel device.

if there is any mistakes in this guide, please 
##### guide written by ben

## ! NOTICE !
### this is a guide for Windows users. I advise you to get a hold of a windows PC to continue.

## 1. Unlocking Bootloader

#### !!! WARNING !!!
##### Unlocking your Bootloader WILL erase all of your data and may void your warranty. Be sure to back up anything you have on your device before beginning.

### a) Preparing device

go to Settings > About > Build number (tap it 7 times).
Then go to Settings > system > Developer options 

Enable these:
- OEM Unlocking
- USB debugging

Go to settings > passwords And accounts > remove all Google accounts

### b) Downloading ADB/Fastboot commands and Google USB drivers

OPTIONAL: You can make a folder somewhere on your PC and store all of these files on it.

visit this Link and download the Google USB driver ZIPfile:
https://developer.android.com/studio/run/win-usb

visit this link to download ADB/Fastboot commands (SDK platform tools for Windows): 
https://developer.android.com/tools/releases/platform-tools

save both ZIPs to your preferred location on your PC.

### c) Setup

Unzip the Google USB driver and run installer. After installing drivers it is safe to delete installer since you won't need it anymore.

Unzip the SDK platform tools for Windows.

### d) Start Unlock process

Power off your Pixel and hold Power button + Volume down to go into Fastboot mode. once done, plug in the Pixel in the PC.

go to `platform-tools` folder and Click on searchbar then type `CMD`. A command Prompt window should appear.

In the CMD window, type these commands in ORDER:

#### check if device connected to PC
```
fastboot devices
```

#### Unlock bootloader command
```
fastboot flashing unlock
```

On the Pixel, use Volume buttons to choose option `Unlock the bootloader` and press Power.

Once done, you can press Power to boot device. You will boot onto setup. Don't sign in with Google account.

## 2. Flashing Lineage OS 20

### a) Downloading ROM files

Download Gapps (needed for Google play services, Google play, etc.): https://androidfilehost.com/?w=files&flid=322935&sort_by=date&sort_dir=DESC

#### Pixel 7:

For the Pixel 7 series, we will be needed the LineageOS zip as well as 4 img files:
- Lineage OS (Download links are below)
- boot.img
- dtbo.img
- vendor_kernel_boot.img
- vendor_boot.img

#### Pixel 6:

For the Pixel 6 series, we will be needed the LineageOS zip as well as 4 img files:
- Lineage OS (Download links are below)
- boot.img
- dtbo.img

#### Pixel 5:

For the Pixel 5 series, we will be needed the LineageOS zip as well as 4 img files:
- Lineage OS (Download links are below)
- boot.img
- dtbo.img

##### Download:

Pixel 7:
Pixel 7 pro:
Pixel 7a: 

Pixel 6:
Pixel 6 pro:
Pixel 6a: 

Pixel 5:
Pixel 5 pro:
Pixel 5a: 
