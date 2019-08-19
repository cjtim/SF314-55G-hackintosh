# SF314-55G-hackintosh
Acer swift 2019 SF314-55G hackintosh
Acer Swift 3 2019 SF314-55G

Boot

	Normal boot : config.plist
	Installer boot : RehabMan-laptop-UHD630.plist

Sound

  Fix headphone
	applealc (ID:13) , set ID in config.plist Device/properties/....0x3f..../audio id 13
	CodecCommander.kext
	ALCPlugFix
	[Fix] Audio Distortion when using Headphones on Laptops
  
  
Use VirualSMC to fix battery percent
NoTouchID.kext fix slow show password digitbox
