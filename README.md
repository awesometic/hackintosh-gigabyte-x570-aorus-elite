# Ryzen Hackintosh EFI

## What is this

This repository contains the EFI directory for Hackintosh system. Especially, this is designed for the Ryzen Zen2/3 system with a specific mainboard. This is of course though. :)

## Specification of my computer

| Component    | Product Name                                     | Note                                           |
|--------------|--------------------------------------------------|------------------------------------------------|
| CPU          | AMD Ryzen 9 3900X                                | PBO enabled                                    |
| Mainboard    | Gigabyte X570 Aorus Elite                        | F31 BIOS                                       |
| Memory       | Samsung DDR4 2666MHz 16GB 2EA                    | Overclocked at 3200MHz with 16-18-18-36 timing |
| Graphics     | XFX AMD Radeon RX 5700 XT 8GB GDDR6 RAW II Ultra |                                                |
| NVMe         | WD Black SN750 500GB                             | macOS installed                                |
| SSD 1        | ADATA SP920 256GB                                | Windows installed                              |
| SSD 2        | Sandisk Ultra 3D 1TB                             | Shared storage between those two OSes          |
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

- 0.6.4

### ACPI

### Drivers

### Kexts

### Tools

## What works and what doesn't work

### Works

### Doesn't work

## To do

## References

- https://dortania.github.io/OpenCore-Install-Guide/
