
# SF314-55G-hackintosh
## Only tested in Mojave

## Contributors
 - cjtim
 - [pawanzZ](https://github.com/pawanzZ/SF314-55G-hackintosh) **for microphone working please use pawanzZ's Repo :), Thank you.**

## Table of content
- [Spec](#spec)
- [Know Working](#working)
- [Not Working](#notwork)
- [Installation](#install)
- [Post Installation](#postinstall)
- [DSDT patch](#dsdt)
- [Dual Boot Windows](#windows)
- [Audio Line-in fix](#headphone-line-in)
- [Ref]()
## Model 
Acer swift 2019 SF314-55G hackintosh
Acer Swift 3 2019 SF314-55G

### Spec <a name="spec"></a>
- I5-8562U
- UHD 620
- Nvidia MX250
- ALC256
- WD SSD 512GB
- 2 USB3
- 1 USB-C with PD charging and Display port compatibility

### Working <a name="working"></a>
- HDMI output
- Sound (speaker and headphone jack)
- Full QE/CI (accelerated graphics)
- Brightness control via setting
- all USB-A 3.0 port(USB-C not test)
- Webcam
- Microphone (With line-in/ headphone) ref: https://github.com/hackintosh-stuff/ComboJack
### Know not working <a name="notwork"></a>
- Finger print reader
- Brightness adjust button (Up with insert botton NEED REMAP WITH DSDT)
- Sleep
- Microphone internal
- Wifi need replace with DW1820A

### Installation <a name="install"></a>
- Clover
	- **use OsxAptioFix3Drv** or you will get stuck on installation
	- Use RehabMan Clover config_UHD630.plist
- Boot
	- Normal boot : config.plist
	- Installer boot : RehabMan-laptop-UHD630.plist

	
### Post Installation <a name="postinstall"></a>

- KEXT
	- AppleALC.kext
	- CPUFriend.kext
	- Lilu.kext
	- NoTouchID.kext
	- VirtualSMC.kext (instead of FakeSMC.kext) all plugins
	- VoodooI2C.kext + VoodooI2CHID.kext
	- VoodooPS2Keyboard.kext
	- WhateverGreen.kext

- Sound(ALC256)
	- applealc (ID:13) , 
	- set ID in config.plist Device/properties/....0x3f..../audio id 13
	- FakePCIID.kext +FakePCIID_Intel_HDMI_Audio.kext
	- CodecCommander.kext
	- ALCPlugFix - [Fix] Audio Distortion when using Headphones on Laptops

- Use VirualSMC to fix battery percent
- NoTouchID.kext fix slow show password digitbox

### DSDT Patch <a name="dsdt"></a>

- Rename GFX0 to IGPU
- Fix _WAK Arg0 v2
- Fix Mutex with non-zero SyncLevel
- HPET Fix
- IRQ Fix
- OS Check Fix ( Windows 10 )
- RTC Fix
- SMBUS Fix
- TrackPad (IC2)
	- VoodooI2C.kext + VoodooI2CHID.kext
	- DSDT patch
		- I2C Controllers [SKL] +GPIO Controller Enable
### Microphone with line-in fix  <a name="headphone-line-in" href="https://github.com/hackintosh-stuff/ComboJack"></a>
- Hackintosh combojack support for alc256/alc255. ref: 
1. Delete CodecCommander.kext，put ComboJack_Installer/VerbStub.kext in Clover/kexts/Other
2. Run ComboJack_Installer/install.sh in terminal and reboot
3. Done. When you attach a headphone there will be a popup asking about headphone type.

### Dual Boot Windows < name="windows"></>

- I use my own clone windows from Acer service center (Acronis True image file)
- restore windows
- boot to WINPE 
- use DISKPART mount efi volume
	- bcdboot C:\Windows /s <efi letter>: /f UEFI


## Ref.
- Thanks to richardchiu [Guide] Acer Swift 5 SF514-53t whiskey lake MacOS10.14.5
