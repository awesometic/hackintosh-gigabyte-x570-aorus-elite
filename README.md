# Ryzen Hackintosh EFI

![Ryzen Hackintosh](docs/hackintosh_macos_bigsur.png)

## What is this

This repository contains the EFI directory for Ryzen 3900X and Gigabyte X570 Aorus Elite combo, with somewhat diverse additional components.

## Specification of my computer

| Component    | Product Name                                     | Note                                           |
|--------------|--------------------------------------------------|------------------------------------------------|
| CPU          | AMD Ryzen 9 3900X                                | PBO enabled                                    |
| Mainboard    | Gigabyte X570 Aorus Elite                        | F33a BIOS                                       |
| Memory       | Samsung DDR4 2666MHz 16GB 2EA                    | Overclocked at 3200MHz with 16-18-18-36 timing |
| Graphics     | XFX AMD Radeon RX 5700 XT 8GB GDDR6 RAW II Ultra |                                                |
| NVMe         | WD Black SN750 500GB                             | macOS installed                                |
| SSD 1        | Sandisk Ultra 3D 1TB                             | Windows installed                              |
| SSD 2        | ADATA SP920 256GB                                | Shared storage between those two OSes          |
| PCI Ethernet | EFM ipTIME PX2500 2.5 GbE LAN Card (RTL8125B)    | Using this as the main Ethernet device         |
| BT/WIFI      | Fenvi T919 (BCM94360CD)                          |                                                |
| PSU          | Antec EAG PRO 750W 80PLUS GOLD Modular           |                                                |
| CPU Paste    | Thermal Grizzly Kryonaut                         |                                                |
| CPU Cooler   | Thermalright Le GRAND MACHO RT                   |                                                |
| MEM Cooler   | BRAVOTEC JONSBO NC-1 Black RGB                   |                                                |
| Case         | 3RSYS L530                                       |                                                |
| USB DAC      | Audinst HUD-DX1 Blue24                           |                                                |

## EFI structure

### WARNING

- This EFI contains additional kexts and PCI informations in **config.plist** rather than the essential things for X570 + Zen2 CPU. You should remove them to apply this to your PC. I recommend you use this as only a reference resource. You should make your own config.plist file for your PC.
- **I'm not responsible for any damage to your device with this EFI. Process at your own risk!**

### OpenCore

- Version: 0.6.6

### ACPI

- SSDT-HPET.aml
- SSDT-NVME.aml
- SSDT-PLUG.aml
- SSDT-SBRG.aml
- SSDT-SBUS-MCHC.aml
- SSDT-EC-USBX-DESKTOP.aml
- SSDT-XHC.aml

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
- SmallTreeIntel82576.kext
- SMCAMDProcessor.kext
- VirtualSMC.kext
- WhateverGreen.kext

### Tools

- OpenShell.efi

## What works and what doesn't work

### Works

- Almost everything including Apple continuity (Handoff, iMessage, Airdrop, Facetime, ...).

### Doesn't work

- Virtualization is not perfectly working.
- Sleep seems like occur kernel panic sometimes.
- A 3.5mm Microphone. A USB Microphone is working.
- Specific professional applications may need to be patched for AMD processor such as Adobe apps, Davinci Resolve, etc.

## References

- https://dortania.github.io/OpenCore-Install-Guide/
- https://forum.amd-osx.com/index.php?threads/ms-x570-aorus-elite-5700-xt-r7-3800x-big-sur-oc-0-6-6.1524/
