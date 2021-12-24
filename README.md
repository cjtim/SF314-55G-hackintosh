
  
#  Acer Swift 3 2019 SF314-55G Hackintosh

For Mojave Clover (discontinued) -> [Mojave-clover branch](https://github.com/cjtim/SF314-55G-hackintosh/tree/mojave-clover)

**Status: WIP Daily usable**

This EFI aiming to config mostly DSDT patch and try to not install kext if possible.


## Known working version
* Catalina
* Big Sur

## Contributors
 - cjtim
 - [pawanzZ](https://github.com/pawanzZ/SF314-55G-hackintosh) **for microphone working please use pawanzZ's Repo :), Thank you.**

## Table of content
- [Spec](#spec)
- [Know Working](#working)
- [Not Working](#notwork)
- [Installation](#install)
- [Post Installation](#postinstall)
- [Information](#Information)
- [Ref]()

### Spec <a name="spec"></a>
- I5-8562U Whiskey lake
- UHD 620
- Nvidia MX250
- ALC256
- WD SSD 512GB
- 2 USB3
- 1 USB-C with PD charging and Display port compatibility
- Intel(R) Wireless-AC 9560

### Working <a name="working"></a>
- Sound (speaker and headphone jack)
  - Headphone and headset work via ComboJack and VerbStub.kext
- Full QE/CI (accelerated graphics)
- HDMI and DisplayPort with audio
- Brightness control via setting
- all USB-A 3.0 port including USB-C
- Touchpad
- Wifi and Bluetooth
- Disabled dGPU
- Sleep
- FireVault

### Know not working <a name="notwork"></a>
- Finger print reader
- internal microphone

### Installation <a name="install"></a>
- Make USB from this guide [Making the installer](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#downloading-macos-modern-os) from Dortania
- Copy EFI folder to your root
- Generate new SMBIOS [https://github.com/corpnewt/GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)

	
### Post Installation <a name="postinstall"></a>
- Not things to do here. everything is include in EFI
- Make sure you got the right version of  [AirportItlwm.kext](https://github.com/OpenIntelWireless/itlwm/releases). Depends on MacOS version Catalina and Big Sur.
- Setting > TouchPad. Untick `Force Click and haptic feedback` this one causing invert click on touchpad


### Information  <a name="Information"></a>
- Config.plist ** 
	- The one from dortania's tutorial won't works and gets kernel panic. Change to following settings.
	- `EnableWriteUnprotector=True`
	- `RebuildAppleMemoryMap=False`
	- Recommend `MacBookPro15,2` 
		- tried `MacBookPro15,1` seems like brightness control not working.

 - Graphics - `PciRoot(0x0)/Pci(0x2,0x0)`
	 - `AAPL,ig-platform-id` = `0000A53E`
	 - `device-id` = `A53E0000`

 - DSDT
	 - Touchpad
		 - `SSDT-GPIO.aml`
		 - `SSDT-XOSI.aml`
	 - `SSDT-EC.aml` - 
	 - `SSDT-HPET.aml`
	 - `SSDT-PLUG.aml` - Allow Native CPU Power management
	 - `SSDT-PMC.aml` - Fix Native NVRAM **(Your installation won't finished and freeze without this)
	 - `SSDT-PNLF.aml` - Fix backlight brightness control
	 - `SSDT-dGPU-Off.aml`  - Disable dGPU this one is special made for only this laptop.
 - Kext
	 - Wifi
		 - `AirportItlwm.kext`
	 - Bluetooth
		 - `IntelBluetoothFirmware.kext`
		 - `IntelBluetoothInjector.kext`
	 - Sound - `layout-id` is `56`
	 	 - `AppleALC.kext`
		 - `AppleALCU.kext`	
	 - `Lilu.kext` and `WhateverGreen.kext`
	 - VirtualSMC
		 - `SMCBatteryManager.kext`
		 - `SMCProcessor.kext`
		 - `SMCSuperIO.kext`
		 - `VirtualSMC.kext`
	 - VoodooI2C with DSDT patch to work.
		 - `VoodooI2C.kext`
		 - `VoodooI2CHID.kext`
	 - `VoodooPS2Controller.kext`
	 - `USBMap.kext` - Special made for this device [Why should you USB map](https://dortania.github.io/OpenCore-Post-Install/usb/#macos-and-the-15-port-limit)

### TODO
- [x] Fix HDMI

## Ref.
- Thanks to richardchiu [Guide] Acer Swift 5 SF514-53t whiskey lake MacOS10.14.5
