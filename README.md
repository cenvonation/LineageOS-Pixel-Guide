# Welcome!
This is an unofficial guide to install Lineage OS on a Pixel device.

if there are any mistakes in this guide, please make a PR.
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

Go to Settings > Passwords and Accounts > Remove all Google accounts

### b) Downloading ADB/Fastboot commands and Google USB drivers

OPTIONAL: You can make a folder somewhere on your PC and store all of these files on it.

Download the Google USB driver for Windows [here](https://developer.android.com/studio/run/win-usb "Google ADB USB driver").

Download ADB Platform Tools for Windows [here](https://developer.android.com/tools/releases/platform-tools "ADB Platform Tools for Windows").

Save both ZIPs to your preferred location on your PC.

### c) Setup

Unzip the Google USB driver and run the installer. After installing drivers it is safe to delete the installer since you won't need it anymore.

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

## 2. Downloading Files

### a) ROM and .img

#### !!! WARNING 2 !!!
##### You MUST put the LineageOS ROM and all of the provided .img files in the `platform-tools` folder for the flashing to work later.

#### Pixel 7:

For the Pixel 7 series, we will be needed the LineageOS zip as well as 4 img files:
- Lineage OS (Download links are below)
- boot.img
- dtbo.img
- vendor_kernel_boot.img
- vendor_boot.img

#### Pixel 6:

For the Pixel 6 series, we will be needed the LineageOS zip as well as 3 img files:
- Lineage OS (Download links are below)
- boot.img
- dtbo.img
- vendor_boot.img

#### Pixel 5:

For the Pixel 5 series, we will be needed the LineageOS zip as well as 3 img files:
- Lineage OS (Download links are below)
- boot.img
- dtbo.img
- vendor_boot.img

##### Links:

- [Pixel 7](https://download.lineageos.org/devices/panther/builds)
- [Pixel 7 Pro](https://download.lineageos.org/devices/cheetah/builds)
- [Pixel 7a](https://download.lineageos.org/devices/lynx/builds)

- [Pixel 6](https://download.lineageos.org/devices/oriole/builds)
- [Pixel 6 Pro](https://download.lineageos.org/devices/raven/builds)
- [Pixel 6a](https://download.lineageos.org/devices/bluejay/builds)

- [Pixel 5](https://download.lineageos.org/devices/redfin/builds)
- [Pixel 5a](https://download.lineageos.org/devices/barbet/builds)

### b) Google Apps/Services (Gapps)

#### ! NOTICE !
GAPPS are optional. If you don't want any Google Play Services and want it to be an OS with stock applications then feel free to skip this.

#### !!! WARNING 3 !!!
##### It is very important you download Arm64 version or else you will get errors.
You can choose to flash the Gapps after flashing the OS later.
Download Gapps [here](https://androidfilehost.com/?w=files&flid=322935&sort_by=date&sort_dir=DESC "Google Apps").

## 3. Flashing

### a) Partitions

We will start by flashing the .img files.

Since we reset the device by unlocking the bootloader, we will have to do the same steps in developer options:

go to Settings > About > Build number (tap it 7 times).
Then go to Settings > system > Developer options 

Enable these:
- OEM Unlocking
- USB debugging

go to `platform-tools` folder and Click on searchbar then type `CMD`. A command Prompt window should appear.

In the CMD window, type these commands in ORDER:

#### check if device connected to PC 
this might show a popup on your Pixel asking you to let you use your PC to debug. Just click Allow.

If it shows a string of numbers and letters with the word `unauthorized`, Allow the popup on your phone first.
```
adb devices
```
Once done, it should show the same string of numbers and letters and with the word `device`.

#### rebooting into fastboot mode (for flashing .img files)
```
adb reboot bootloader
```

#### check if device is connected to PC in fastboot mode
```
fastboot devices
```

#### This is the section of the tutorial where we flash the .img files onto the Pixel

Type these commands in order in the fastboot CMD window:

#### Pixel 7:
```
fastboot flash boot boot.img
```

```
fastboot flash dtbo dtbo.img
```

```
fastboot flash vendor_kernel_boot vendor_kernel_boot.img
```

```
fastboot flash vendor_boot vendor_boot.img
```

#### Pixel 6:
```
fastboot flash boot boot.img
```

```
fastboot flash dtbo dtbo.img
```

```
fastboot flash vendor_boot vendor_boot.img
```

#### Pixel 5:
```
fastboot flash boot boot.img
```

```
fastboot flash dtbo dtbo.img
```

```
fastboot flash vendor_boot vendor_boot.img
```

### b) Operating system

#### This is the section of the tutorial where we flash the LineageOS ZIPfile onto the Pixel. the phone MUST stay plugged into the PC until we're done with flashing.

While in fastboot mode, select either Volume Up or Volume Down to select recovery mode. Once selected, select Power to boot into recovery. You should boot into the custom Lineage OS recovery menu.

In the recovery mode, use the Volume keys or the touch screen to navigate and select `Factory Reset` > `Format Data` to remove the existing android Operating system.

Once done head over to `Apply update` > `Apply from ADB`.

##### MAKE SURE YOU HAVE THE LINEAGEOS AND GAPPS ZIPFILE IN THE SAME DIRECTORY AS `platform-tools` TO SIDELOAD AND FLASH.

Now head over to the CMD window open on your computer and type this command:

```
adb sideload [LINEAGE OS ZIPFILE NAME].zip
```
replace `[LINEAGEOS ZIPFILE NAME]` with the name of the LineageOS zipfile.

Wait for it to flash.

### c) GAPPS

### ! NOTICE !
Again, GAPPS are optional. If you don't want any Google Play Services and want it to be an OS with stock applications then feel free to skip this as well.

Once the OS has been successfully flashed we can now finish it up by flashing the GAPPS.

Now head over to the CMD window open on your computer and type this command:
```
adb sideload [GAPPS ZIPFILE NAME].zip
```
replace `[GAPPS ZIPFILE NAME]` with the name of the LineageOS zipfile.

The screen will show an error indicating that the Signature Verification Failed, just hit Yes/continue.

Once done you can exit out of `Apply Update` and select `Reboot System Now`.

## CONGRATS! 🎉
### You have installed Lineage OS. If you encounter any errors, consider getting support from the [official Discord server](https://discord.com/invite/gD6DMtf "LineageOS support Discord").

##
##### © 2016 - 2023 The LineageOS Project
##### LineageOS LLC is not a 501(c)(3) non-profit, as such donations are not tax-exempt.
##### Unofficial Pixel guide by Ben.
