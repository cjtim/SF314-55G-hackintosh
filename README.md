


  
#  Acer Swift 3 2019 SF314-55G Hackintosh

For Mojave Clover (discontinued) -> [Mojave-clover branch](https://github.com/cjtim/SF314-55G-hackintosh/tree/mojave-clover)

**Status: ✅ Daily usable**

This EFI aiming to config mostly DSDT patch and try to not install kext if possible.


## Known working version
* Catalina - 10.15.7
* Big Sur - 11.6.1

## Table of content
- [Spec](#spec)
- [Working ✅](#working)
- [Not working ❌](#notwork)
- [Installation 🍱](#install)
- [Post Installation](#postinstall)
- [FYI](#Information)
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

### Working ✅  <a name="working"></a>
**Everythings is working.**

| Feature | Note |
|--|--|
| Sound 🔊 | ✅ Speaker and Headphone (headset microphone work via ComboJack and VerbStub.kext) |
| Graphic 🏞 | ✅ Intel UHD 620 and completly disable dGPU (with DSDT and Whatevergreen)|
| HDMI and DisplayPort 📺 | ✅ With audio on both port|
| Brightness ☀️ | ✅ |
| USB-A and USB-C 📁 | ✅ Completly disable Fingerprint and SDCard reader with USBMapping|
| Touchpad 🖱| ✅ |
| Wifi and Bluetooth ☁️ | ✅ Handoff, copy file across device (but No AirDrop)|
| Sleep 🛌 | ✅ |
| FireVault 🔐  | ✅ |

### Know not working ❌<a name="notwork"></a> 
- Internal microphone 🎤 (No workaround to get Intel® SST working yet)

### Installation 🍱 <a name="install"></a>
- Make USB from this guide [Making the installer](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#downloading-macos-modern-os) from Dortania
- Copy EFI folder to your root
- Make sure you got the right version of  [AirportItlwm.kext](https://github.com/OpenIntelWireless/itlwm/releases). Depends on MacOS version Catalina and Big Sur.
- Generate new SMBIOS [https://github.com/corpnewt/GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)

	
### Post Installation <a name="postinstall"></a>
- Not things to do here. everything is include in EFI
- Setting > TouchPad. Untick `Force Click and haptic feedback` this one causing invert click on touchpad
- (Optional) Install ComboJack for working headset microphone and VerbStub.kext.

### For your infomation  <a name="Information"></a>
- Config.plist ** 
	- Start with this [Laptop Coffee Lake and Whiskey Lake](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake.html) 
	- The one from dortania's tutorial won't works and gets kernel panic. Change to following settings.
		- `EnableWriteUnprotector=True`
		- `RebuildAppleMemoryMap=False`
		- Recommend `MacBookPro15,2` 
			- tried `MacBookPro15,1` seems like brightness control not working.
 - Graphics - `PciRoot(0x0)/Pci(0x2,0x0)`
	 - `AAPL,ig-platform-id` = `0000A53E`
	 - `device-id` = `A53E0000`

 - DSDT
	 - Touchpad [Fixing Trackpads (SSDT-GPI0/XOSI)](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad.html)
		 - `SSDT-GPIO.aml`
		 - `SSDT-XOSI.aml`
	 - `SSDT-EC.aml` - [EC fix](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)
	 - `SSDT-HPET.aml` - [Sound](https://dortania.github.io/Getting-Started-With-ACPI/Universal/irq.html)
	 - `SSDT-PLUG.aml` - [Allow Native CPU Power management](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html)
	 - `SSDT-PMC.aml` - [Fix Native NVRAM](https://dortania.github.io/Getting-Started-With-ACPI/Universal/nvram.html) **(Your installation won't finished and freeze without this)
	 - `SSDT-PNLF.aml` - [Fix backlight brightness control](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/backlight.html)
	 - `SSDT-dGPU-Off.aml`  - Disable dGPU this one is special made for only this laptop.
 - Kext
	 - Wifi
		 - `AirportItlwm.kext` - [v2.0.0](https://github.com/OpenIntelWireless/itlwm/releases/tag/v2.0.0)
	 - Bluetooth - [v2.0.1](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/releases/tag/v2.0.1)
		 - `IntelBluetoothFirmware.kext`
		 - `IntelBluetoothInjector.kext`
	 - Sound - `layout-id` is `17` or `5,11,13` is work as well
		 - [1.6.7](https://github.com/acidanthera/AppleALC/releases/tag/1.6.7)
	 	 - `AppleALC.kext`
		 - `AppleALCU.kext`	
	 - `Lilu.kext` - [1.5.8](https://github.com/acidanthera/Lilu/releases/tag/1.5.8)
	 - `WhateverGreen.kext` - [1.5.5](https://github.com/acidanthera/WhateverGreen/releases/tag/1.5.5)
	 - VirtualSMC - [1.2.8](https://github.com/acidanthera/VirtualSMC/releases/tag/1.2.8)
		 - `SMCBatteryManager.kext`
		 - `SMCProcessor.kext`
		 - `SMCSuperIO.kext`
		 - `VirtualSMC.kext`
	 - VoodooI2C with DSDT patch to work.
		 - [2.6.5](https://github.com/VoodooI2C/VoodooI2C/releases/tag/2.6.5)
		 - `VoodooI2C.kext`
		 - `VoodooI2CHID.kext`
	 - `VoodooPS2Controller.kext` - [2.27](https://github.com/acidanthera/VoodooPS2/releases/tag/2.2.7)
	 - `USBMap.kext` - Special made for this device [Why should you USB map](https://dortania.github.io/OpenCore-Post-Install/usb/#macos-and-the-15-port-limit)

## Ref.
- Thanks to richardchiu [\[Guide\] Acer Swift 5 SF514-53t whiskey lake MacOS10.14.5](https://www.tonymacx86.com/threads/guide-acer-swift-5-sf514-53t-whiskey-lake-macos10-14-5.277618/)


## Contributors
 - cjtim
 - [pawanzZ](https://github.com/pawanzZ/SF314-55G-hackintosh) **for microphone working please use pawanzZ's Repo :), Thank you.**
