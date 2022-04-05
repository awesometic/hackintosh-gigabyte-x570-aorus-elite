# Ryzen Hackintosh EFI

![Ryzen Hackintosh](docs/hackintosh_macos_monterey.png)
![Ryzen Hackintosh - About this Mac](docs/about_this_mac.png)

## What is this

This repository contains the EFI directory for Ryzen 3900X and Gigabyte X570 Aorus Elite combo, with somewhat diverse additional components.

## Specification of my computer

| Component    | Product Name                                     | Note                                           |
|--------------|--------------------------------------------------|------------------------------------------------|
| CPU          | AMD Ryzen 9 3900X                                | PBO enabled                                    |
| Mainboard    | Gigabyte X570 Aorus Elite                        | F35 BIOS                                       |
| Memory       | Samsung DDR4 2666MHz 16GB 2EA                    | Overclocked at 3600MHz with 18-22-22-44 timing |
| Graphics     | XFX AMD Radeon RX 5700 XT 8GB GDDR6 RAW II Ultra | Changed its thermal pad and thermal paste      |
| NVMe 1       | Samsung 980 PRO 1TB                              | Windows 11 installed                           |
| NVMe 2       | RevuAhn NX2300 1TB                               | Ubuntu 22.04 installed                         |
| NVMe 3       | WD Black SN750 500GB (via PCIe to NVMe adapter)  | macOS 12 installed                             |
| SSD 1        | Sandisk Ultra 3D 1TB                             | Miscellaneous storage                          |
| PCI Ethernet | EFM ipTIME PX2500 2.5 GbE LAN Card (RTL8125B)    | Using this as the main Ethernet device         |
| BT/WIFI      | Fenvi T919 (BCM94360CD)                          |                                                |
| PSU          | Antec EAG PRO 750W 80PLUS GOLD Modular           |                                                |
| CPU Paste    | Thermalright TFX                                 |                                                |
| CPU Cooler   | Thermalright Le GRAND MACHO RT                   |                                                |
| MEM Cooler   | BRAVOTEC JONSBO NC-1 Black RGB                   |                                                |
| Case         | 3RSYS L530                                       |                                                |
| USB DAC      | Audinst HUD-DX1 Blue24                           |                                                |
| USB MIC      | Blue Yeti X                                      |                                                |

## EFI structure

### WARNING

- I recommend you use this as only a reference resource.
  - Obviously, this build may not be the best one.
  - This EFI contains additional kexts in **config.plist** rather than only the essential things for X570 + Zen2 CPU. You should remove them before using this on your PC.

### One more, check this before you use

In the [config.plist](EFI/OC/config.plist) file, I've replaced the private serial codes into the `EDIT_HERE` words because to keep my personal information safe.

So if you are going to use this, you have to make sure that the `EDIT_HERE` texts are changed to yours. To generate the serial key, please refer to the [Dortania's OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#platforminfo). When you are about to generate one, you should select `MacPro7,1` to properly use your machine.

> - If you are going to convert SMBIOS from **iMacPro1,1** to **MacPro7,1**, make sure that you must logout Apple ID from your current system and regenerate all the SMBIOS details such as MLB, serial number, UUID for MacPro7,1.
> - If your CPU has less than 8 cores, go to `config.plist` file and find "PlatformInfo->Generic" and change the "ProcessorType" from 0 to 1537.

### You got another one you must check

From the recent AMD CPU patch, now we have to specify the CPU core counts to the `algrey - Force cpuid_cores_per_package` nodes. Currently, my EFI setup sets that for the **12-core** CPU model because I'm using Ryzen 3900X.

- `algrey - Force cpuid_cores_per_package`
  - 10.13,10.14
    - B8**0C**0000 0000
  - 10.15,11.0
    - BA**0C**0000 0000
  - 12.0
    - BA**0C**0000 0090

Please refer to [the author's description](https://github.com/AMD-OSX/AMD_Vanilla#read-me-first) to get further information.

### OpenCore

- Version: 0.7.9

### ACPI

- SSDT-HPET.aml - Fixes IRQ conflicts
- SSDT-NVME.aml - Makes NVMe drives shown as an internal storage
- SSDT-PLUG.aml - Fixes CPU power management
- SSDT-SBRG.aml - Fixes EC, RTC, IRQ conflicts
- SSDT-SBUS-MCHC.aml - Fixes SMBus support
- SSDT-EC-USBX-DESKTOP.aml - Fixes embedded controller and USB power properties
- SSDT-XHC.aml - Fixes USB ports mapping

### Drivers

- OpenCanopy.efi
- OpenHfsPlus.efi
- OpenRuntime.efi

### Kexts

- AGPMInjector.kext
- AMDRyzenCPUPowerManagement.kext
- AppleALC.kext
- AppleMCEReporterDisabler.kext
- CtlnaAHCIPort.kext
- Lilu.kext
- LucyRTL8125Ethernet.kext
- NVMeFix.kext
- RadeonSensor.kext
- RestrictEvents.kext
- SmallTreeIntel82576.kext
- SMCAMDProcessor.kext
- SMCRadeonSensor.kext
- VirtualSMC.kext
- WhateverGreen.kext

### Tools

- OpenShell.efi

## What works and what doesn't work

### Works

- Almost everything including Apple continuity (Handoff, iMessage, Airdrop, Facetime, Universal Control, ...).

### Partially works

- 3.5mm audio jacks
  - The speaker output on the front/back panel works.
  - The microphone input on the front/back panel doesn't work.
  - Have not tested line in/out and digital out.
- The common Ryzentosh issues. Please refer to the CPU support part of [Dortania's OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/macos-limits.html#cpu-support)
  - Specific professional applications may need to be patched for AMD processors such as Adobe apps, Davinci Resolve, etc.
  - Virtualization (Apple Hypervisor and the apps using this like AVD on Android Studio, Parallels) is not working but VirtualBox works.

### Doesn't work

- Sidecar
- Ethernet (Our NIC, Intel I211)
  - After macOS 12 Monterey, the kext `SmallTreeIntel82576.kext` is not working anymore. It detects the NIC device but reports the cable is disconnected.
  - <https://github.com/khronokernel/SmallTree-I211-AT-patch/issues/3>

## Main References

I've got the SSDTs and configuring hints from the following links.

- <https://dortania.github.io/OpenCore-Install-Guide/>
- <https://forum.amd-osx.com/index.php?threads/ms-x570-aorus-elite-5700-xt-r7-3800x-big-sur-oc-0-6-6.1524/>
- <https://forum.amd-osx.com/index.php?threads/audiogods-gigabyte-aorus-x570-pro-pro-wifi-ultra-master-big-sur-monterey-beta-opencore-0-7-4-efi.1344/>
