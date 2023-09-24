# Welcome!
This is an unofficial guide to install Lineage OS on a Pixel device.

If there are any mistakes in this guide, please make a pull request.
##### guide written by arm64 and Yeet1000

## ! NOTICE !
### Although this guide is designed for Windows users, many steps are similar on macOS and Linux.
### If you're running these OSes, remember to download the binaries (ADB platform tools) for your platform.
## 1. Unlocking Bootloader

#### !!! WARNING !!!
##### Unlocking your Bootloader WILL erase all of your data and may void your warranty. Be sure to back up anything you have on your device before beginning.

### a) Preparing device

Go to Settings > About, then look for Build Number. Tap it 7-8 times until you see "You are now a developer!" or "Development settings have been enabled!"
Then go to Settings > System > Developer Options.

Enable these:
- OEM Unlocking
- USB debugging

Go to Settings > Passwords and accounts, then remove all the Google accounts listed.

### b) Downloading ADB/Fastboot binaries and Google USB drivers

OPTIONAL: You can make a folder somewhere on your PC and store all of these files in it.

Visit [this link](https://developer.android.com/studio/run/win-usb) and download the Google USB driver ZIP file.

Visit [this link](https://developer.android.com/tools/releases/platform-tools) to download ADB/Fastboot binaries (SDK platform tools for Windows).

Save both ZIPs to your preferred location on your PC.

### c) Setup

Unzip the Google USB driver and run the installer. After installing the drivers it is safe to delete the installer since you won't need it anymore.

Unzip the SDK platform tools for Windows.

### d) Start Unlock process

Power off your Pixel and hold Power button + Volume down to go into Fastboot mode. Once done, plug the Pixel into the PC.

Go to the `platform-tools` folder, click on the folder path at the top, then type `CMD`. A Command Prompt window should appear.

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

| Devices  | Download |
| ------------- | ------------- |
| Pixel 7  | [panther](https://download.lineageos.org/devices/panther/builds)  |
| Pixel 7 Pro  | [cheetah](https://download.lineageos.org/devices/cheetah/builds)  |
| Pixel 7a  | [lynx](https://download.lineageos.org/devices/lynx/builds)  |
| Pixel 6  | [oriole](https://download.lineageos.org/devices/oriole/builds)  |
| Pixel 6 Pro  | [raven](https://download.lineageos.org/devices/raven/builds)  |
| Pixel 6a  | [bluejay](https://download.lineageos.org/devices/bluejay/builds)  |
| Pixel 5  | [redfin](https://download.lineageos.org/devices/redfin/builds)  |
| Pixel 5a  | [barbet](https://download.lineageos.org/devices/barbet/builds)  |

If your device is not listed here, unfortunately this guide does NOT cover your device at this moment.

### b) Google Apps/Services (Gapps)

#### ! NOTICE !
##### GAPPS are optional. If you don't want any Google Play Services and want an OS with stock applications then feel free to skip this.

#### !!! WARNING 3 !!!
##### It is very important you download the arm64 version or else you will run into errors.

We will flash the Gapps right after flashing the OS later.
Download Gapps [here](https://androidfilehost.com/?w=files&flid=322935&sort_by=date&sort_dir=DESC).

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

fastboot flash dtbo dtbo.img

fastboot flash vendor_kernel_boot vendor_kernel_boot.img

fastboot flash vendor_boot vendor_boot.img
```

#### Pixel 6:
```
fastboot flash boot boot.img

fastboot flash dtbo dtbo.img

fastboot flash vendor_boot vendor_boot.img
```

#### Pixel 5:
```
fastboot flash boot boot.img

fastboot flash dtbo dtbo.img

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

Once the OS has been successfully flashed we can now optionally finish it up by flashing the GAPPS.

Now head over to the CMD window open on your computer and type this command:
```
adb sideload [GAPPS ZIPFILE NAME].zip
```
replace `[GAPPS ZIPFILE NAME]` with the name of the GAPPS zipfile.

The screen will show an error indicating that the Signature Verification Failed, just hit Yes/continue.

Once done you can exit out of `Apply Update` and select `Reboot System Now`.

## CONGRATS! 🎉
### You have installed Lineage OS. If you encounter any errors, consider getting support from the Official Discord server.

https://discord.com/invite/gD6DMtf

##
##### © 2016 - 2023 The LineageOS Project
##### LineageOS LLC is not a 501(c)(3) non-profit, as such donations are not tax-exempt.
##### Unofficial Pixel guide by arm64 and Yeet1000.
