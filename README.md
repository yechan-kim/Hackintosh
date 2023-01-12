# Hackintosh
OpenCore EFI for MSI Prestige 15 A10SC

## Specification
| **Component** | **Model** |
| ------------- | --------- |
| CPU | Intel Comet Lake i7-10710u |
| RAM | 16GB (2 x 8GB) Samsung DDR4 @2666MHz |
| IGPU | Intel Graphics UHD 630	|
| DGPU | Nvidia GTX1650 Max-Q |
| Display | CMN N156HCE-EN1 1920*1080(FHD) |
| NVMe 1 | Kingston 256GB |
| NVMe 2 | Samsung 970 EVO PLUS 500GB |
| Audio | Realtek ACL298 |
| Wireless | Intel AX201 |


**OpenCore version**: [0.8.8](https://github.com/acidanthera/opencorepkg/releases)

## Compatible macOS versions
 - Ventura (13.1)

## What Works
 - Wi-Fi : DW1560 (If you wnat to use it, please use [AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup) and [BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM)) / Intel AX201
 - Bluetooth (see sleep/wakeup hint)
 - HDMI (thanks to @vomesk)
 - Internal/External audio jacks
 - Sleep/Wake up
 - OTA Update (If you wnat to use it, please edit SecureBootModel option [**here**](https://dortania.github.io/OpenCore-Post-Install/universal/security/applesecureboot.html#securebootmodel)in config.plist -> Misc -> Security -> SecureBootModel)

## What Doesn't Work
 - Nvidia GTX1650 Max-Q (Disabled via SSDT)
 - Fingerprint Reader Synaptics WBDI
 - Card Reader Realtek RTS5250 PCI-E
 - AirDrop



## How to use
  1. Make your USB installer with [**this guide**](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
  	sudo /Applications/Install\ macOS\ YOUR\ VERSION.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --nointeraction 
  2. Clone the repository and paste "BOOT" and "OC" directories into your's pendrive "EFI" folder
  3. Download [**GenSMBIOS**](https://github.com/corpnewt/GenSMBIOS) to generate unique SMBIOS information. Run it and follow all steps, as the model select **MacBookPro15,4 1**
  4. Boot it!  

**You CAN NOT use SMBIOS from this repository, it MUST be unique for every macOS installation**
**If You CAN NOT install this, please edit SecureBootModel option to Disabled in config.plist -> Misc -> Security -> SecureBootModel**

## Steps
 - BIOS:
 	- Turn off Secure Boot
 	- Press L-ALT + R-CTRL + R-SHIFT + F2 or (fn + F2) for see hidden feature
 	- Advanced → Power & Performance → CPU - Power Management Control → CPU Lock Configuration → CFG Lock : Disabled

 		
## Post Installation
- Move your OpenCore EFI folder to a MacOS drive: https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html#grabbing-opencore-off-the-usb

## Hints
- If you've dual boot:
	- To enable macOS-only SMBIOS injection (disabled for Windows 10):
		- Kernel -> Quirks ??CustomSMBIOSGuid -> True
		- Platforminfo -> UpdateSMBIOSMode -> Custom
	- To have UTC clock and fix Windows 10 issues : DualBoot/UniversalTimeFix.reg
	- Disable Fast Boot on Windows 10 : DualBoot/DisableFastBoot.reg
	- NTFS r/w support : brew install --cask osxfuse; brew install --cask mounty

## BlueTooth fix after sleep/wakeup
	- brew install blueutil
	- brew install sleepwatcher
	- echo "blueutil -p 0 && sleep 1 && blueutil -p 1" > ~/.wakeup
	- chmod +x ~/.wakeup
	- sudo cp -avi /usr/local/Cellar/sleepwatcher/2.2.1/de.bernhard-baehr.sleepwatcher-20compatibility.plist /Library/LaunchDaemons/
	- sudo chown root:wheel /Library/LaunchDaemons/de.bernhard-baehr.sleepwatcher-20compatibility.plist
	- sudo reboot
	- ps -ef | grep -i sleepwatcher

## Kext
 - [Lilu v1.6.3](https://github.com/acidanthera/Lilu)
 - [WhateverGreen v1.6.3](https://github.com/acidanthera/WhateverGreen)
 - [VirtualSMC/SMCBatteryManager/SMCProcessor/SMCSuperIO/SMCLightSensor v1.3.0](https://github.com/acidanthera/VirtualSMC)
 - [AppleALC v1.7.8](https://github.com/acidanthera/AppleALC)
 - [VerbStub v1.0.4](https://github.com/hackintosh-stuff/ComboJack/tree/master/ComboJack_Installer)
 - [VoodooPS2Controller v2.3.3](https://github.com/acidanthera/VoodooPS2)
 - [VoodooI2C v2.7.1 / VoodooI2CHID V1.0.0](https://github.com/VoodooI2C/VoodooI2C)
 - [CPUFriend v1.2.6](https://github.com/acidanthera/CPUFriend)
 - [NoTouchID v1.0.4](https://github.com/al3xtjames/NoTouchID)
 - [NVMeFix v1.1.0](https://github.com/acidanthera/NVMeFix)
 - [IOElectrify v1.0.0](https://github.com/the-darkvoid/macOS-IOElectrify)
 - [USBInjectAll v0.7.1](https://github.com/Sniki/OS-X-USB-Inject-All)
 - [BlueToolFixup v2.6.4](https://github.com/acidanthera/BrcmPatchRAM)
 - [AirportItlwm v2.1.0](https://github.com/OpenIntelWireless/itlwm)
 - [IntelBluetoothFirmware/IntelBluetoothInjector/IntelBTPatcher v2.2.0](https://github.com/OpenIntelWireless/IntelBluetoothFirmware)
 - [IntelMausi V1.0.7](https://github.com/acidanthera/IntelMausi/)





## Special Thanks to...
 - https://github.com/aleixsr/MSI-Prestige-15-A10SC-Hackintosh
 - https://x86.co.kr/


# Hackitosh Apps
- Install Homebrew : 
	- /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
- Karabiner :
	- brew install --cask karabiner-elements
	- Import settings from karabiner/ folder
	- If doesn't work change keyboard to "virtual" and change to USB Keyboard again
- [Hackintool](https://github.com/benbaker76/Hackintool)
- [OpenCore Configurator](https://mackie100projects.altervista.org/download-opencore-configurator/)
- [OpenCore Updater](https://github.com/mswgen/oc-updater)


# MacOS Apps
- iTerm2 + Oh My Zsh! :
	- brew install --cask iterm2
	- brew install zsh zsh-completions
	- Follow https://www.freecodecamp.org/news/how-to-configure-your-macos-terminal-with-zsh-like-a-pro-c0ab3f3c1156/
- XtraFinder : https://www.trankynam.com/xtrafinder/
- HyperDock : brew install --cask hyperdock
- HyperSwitch : brew install --cask hyperswitch
- CopyQ : brew install --cask copyq
- Caffeine : brew install --cask caffeine
- iStat Menus : brew install --cask istat-menus
- Keka : brew install --cask keka
- Lightshot Screenshot : https://app.prntscr.com/es/download.html
- MonitorControl : brew install --cask monitorcontrol
- Numi : brew install --cask numi
- PingMenu : brew install --cask pingmenu
- Tunnelblick : brew install --cask tunnelblick
- Sublime Text : brew install --cask sublime-text