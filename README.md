# SF314-55G-hackintosh
Acer swift 2019 SF314-55G hackintosh
Acer Swift 3 2019 SF314-55G

Boot

	Normal boot : config.plist
	Installer boot : RehabMan-laptop-UHD630.plist

Sound
	
	- Fix headphone
	- applealc (ID:13) , set ID in config.plist Device/properties/....0x3f..../audio id 13
	- CodecCommander.kext
	- ALCPlugFix
	- [Fix] Audio Distortion when using Headphones on Laptops
  
  
Use VirualSMC to fix battery percent

NoTouchID.kext fix slow show password digitbox


Acer Swift 3 2019 SF314-55G




Spec
	I5-8562U
	UHD 620
	Nvidia MX250
	ALC256
	WD SSD 512GB
	2 USB3
	1 USB-C with PD charging and Display port compatibility
Working
	HDMI output
	Sound (speaker and headphone jack)
	Full QE/CI (accelerated graphics)
	Brightness control via setting
	all USB-A 3.0 port(USB-C not test)
	Webcam
Know not working
	Finger print reader
	Brightness adjust button (Up with insert botton NEED REMAP WITH DSDT)
	Sleep
	Microphone
	Wifi need replace with DW1820A
Installation
	Clover
		use OsxAptioFix3Drv or you will get stuck on installation
		Use RehabMan Clover config_UHD630.plist
Post Installation
	KEXT
		AppleALC.kext
		CPUFriend.kext
		Lilu.kext
		NoTouchID.kext
		VirtualSMC.kext (instead of FakeSMC.kext) all plugins
		VoodooI2C.kext + VoodooI2CHID.kext
		VoodooPS2Keyboard.kext
		WhateverGreen.kext
Sound(ALC256)
	applealc (ID:13) , set ID in config.plist Device/properties/....0x3f..../audio id 13
	FakePCIID.kext +FakePCIID_Intel_HDMI_Audio.kext
	CodecCommander.kext
	ALCPlugFix - [Fix] Audio Distortion when using Headphones on Laptops
DSDT Patch
	Rename GFX0 to IGPU
	Fix _WAK Arg0 v2
	Fix Mutex with non-zero SyncLevel
	HPET Fix
	IRQ Fix
	OS Check Fix ( Windows 10 )
	RTC Fix
	SMBUS Fix
TrackPad (IC2)
	VoodooI2C.kext + VoodooI2CHID.kext
	DSDT patch
		I2C Controllers [SKL] +GPIO Controller Enable
Dual Boot Windows
	I use my own clone windows from Acer service center (Acronis True image file)
	restore windows
	boot to WINPE 
	use DISKPART mount efi volume
	bcdboot C:\Windows /s <efi letter>: /f UEFI
Ref.
	
	Thanks to richardchiu [Guide] Acer Swift 5 SF514-53t whiskey lake MacOS10.14.5
