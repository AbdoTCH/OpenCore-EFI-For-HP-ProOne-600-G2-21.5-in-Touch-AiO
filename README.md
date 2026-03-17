# OpenCore EFI For HP ProOne 600 G2 21.5" Touch AiO

> **⚠️ STATUS: UNTESTED / WORK IN PROGRESS**
> This EFI is configured specifically for the HP ProOne 600 G2 (21.5-in Touch) with the Intel Core i5-6500. While based on the Skylake desktop architecture, it has not been verified on this specific unit. **Use at your own risk.**

> **❗Note :**
> Please Use Offline Installer Because SomeTimes it Doesn't Work

<div align="center">
             <img src="https://github.com/dortania/OpenCore-Legacy-Patcher/raw/main/docs/images/OC-Patcher.png" alt="OpenCore Patcher Logo" width="256" />
</div>

## 🖥 System Specifications (Confirmed)

| Component | Specification |
| :--- | :--- |
| **Model** | HP ProOne 600 G2 21.5-in Touch All-in-One |
| **Motherboard** | HP 805E (Proprietary Q150 Chipset) |
| **CPU** | Intel® Core™ i5-6500 @ 3.20GHz (Skylake) |
| **iGPU** | Intel® HD Graphics 530 |
| **RAM** | 8GB DDR4 |
| **BIOS Version** | HP N12 Ver. 02.58 (UEFI Mode) |
| **Audio** | (Not Working !)|
| **Ethernet** | Intel® I219-LM |
| **MacOS Version** | Monterey (**Booted On Recovery**) 

## ⚙️ BIOS Settings for HP ProOne

Access the BIOS by tapping `F10` (or `Esc` then `F10`) during startup.

**Required Changes:**
* **Advanced > Boot Options:**
    * Disable `Fast Boot`
    * Disable `New Slot Solution` (if present)
* **Advanced > Secure Boot Configuration:**
    * Configure Legacy Support and Secure Boot: `Legacy Support Disable and Secure Boot Disable`
* **Advanced > System Options:**
    * Enable `Turbo Boost`
    * Enable `Hyper-Threading`
    * Enable `Multi-Processor`
    * Disable `VTD-T` (Virtualization Technology for Directed I/O) — *Alternatively, keep it ON and use `DisableIoMapper` in config.plist*
* **Advanced > Built-in Device Options:**
    * Video Memory: `64MB` or higher

## 🛠 Installation & Setup

1. **SMBIOS:** This EFI is set up for `iMac17,1`. You **must** generate your own Serial, UUID, and MLB using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) and paste them into the `PlatformInfo -> Generic` section of the `config.plist`.
2. **ACPI:** Includes `SSDT-PLUG`, `SSDT-EC-USBX`, and `SSDT-BRG0` (if needed for NVMe).
3. **Kexts included (Standard):** * `Lilu.kext`
    * `VirtualSMC.kext`
    * `WhateverGreen.kext` (For HD 530 support)
    * `AppleALC.kext` (Layout ID `11` or `15` for ALC221)
    * `IntelMausi.kext` (For the I219-LM Ethernet)
    * `USBMap.kext` (replace with a your map later)

## 🖱 Touchscreen & USB
The touch functionality on this AiO usually interfaces via an internal USB header. 
* To ensure the touchscreen works, you will likely need to perform a **USB Map** using `Hackintool` or `USBMap.kext` once you reach the desktop. 
* If it uses an I2C interface, `VoodooI2C.kext` may be required.
