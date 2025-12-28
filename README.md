# Lenovo IdeaPad Gaming 3 15ACH6 Hackintosh EFI

This EFI configuration is tailored for the **Lenovo IdeaPad Gaming 3 15ACH6** running **macOS Sequoia 15.7.2**.

## 💻 System Specifications

| Component | Specification |
| :--- | :--- |
| **Model** | Lenovo IdeaPad Gaming 3 15ACH6 |
| **CPU** | AMD Ryzen 5 5600H |
| **iGPU** | AMD Radeon Graphics (NootedRed) |
| **dGPU** | NVIDIA GeForce RTX 3050 (Disabled) |
| **WiFi / BT** | Intel AX210 / Intel Bluetooth |
| **Ethernet** | Realtek RTL8111 |
| **Audio** | Realtek (alcid=11) |

## 🛠 Features & Status

*   **macOS Version**: Sequoia 15.7.2
*   **Bootloader**: OpenCore
*   **Graphics**: Hardware acceleration supported via `NootedRed.kext`.
*   **Wi-Fi**: Working via `itlwm.kext` (requires HeliPort for full functionality) or AirportItlwm.
*   **Bluetooth**: Working via Intel firmware kexts.
*   **Audio**: Working via `AppleALC.kext` (alcid=11).
*   **Trackpad**: Working with multi-touch gestures (`VoodooI2C`).
*   **Battery**: Indicator working (`SMCBatteryManager`).
*   **Brightness**: Keys and slider working.
*   **Sleep/Wake**: Working properly (with `GenericUSBXHCI` and USB mapping).

## 📂 EFI Contents

### ACPI (SSDTs)
Patches to align hardware with macOS requirements:
*   `SSDT-ALS0.aml`: Ambient Light Sensor fake.
*   `SSDT-Disable_GPU_GPP0.aml`: Disables unsuported NVIDIA dGPU.
*   `SSDT-EC.aml`: Embedded Controller fix.
*   `SSDT-PLUG-ALT.aml`: CPU power management for AMD.
*   `SSDT-PNLF.aml`: Backlight control fix.
*   `SSDT-USB-Reset.aml`: Resets USB controllers.
*   `SSDT-USBX.aml`: USB power properties.
*   `SSDT-XOSI.aml`: OS spoofing for better hardware support (Trackpad).

### Kexts (Kernel Extensions)
Drivers and patches for hardware support:
*   **Core**: `Lilu.kext`, `VirtualSMC.kext` (plus `SMCBatteryManager`, `SMCLightSensor`, `SMCAMDProcessor`, `SMCRadeonSensors`).
*   **Graphics**: `NootedRed.kext` (AMD Vega iGPU support), `ForgedInvariant.kext`.
*   **Audio**: `AppleALC.kext`.
*   **Networking**:
    *   Wi-Fi: `itlwm.kext`.
    *   Bluetooth: `IntelBluetoothFirmware.kext`, `IntelBTPatcher.kext`, `BlueToolFixup.kext`.
    *   Ethernet: `RealtekRTL8111.kext`.
    *   USB Tethering: `HoRNDIS.kext`.
*   **Input**: `VoodooI2C.kext` & `VoodooI2CHID.kext` (Trackpad), `VoodooPS2Controller.kext` (Keyboard), `BrightnessKeys.kext`.
*   **USB**: `USBToolBox.kext`, `USBMap.kext`, `GenericUSBXHCI.kext`.
*   **Fixes**: `NVMeFix.kext` (Power management), `RestrictEvents.kext`, `FeatureUnlock.kext`, `AppleMCEReporterDisabler.kext`.

### Drivers (UEFI)
*   `OpenRuntime.efi`: Essential for OpenCore.
*   `HfsPlus.efi`: HFS+ filesystem support.
*   `AudioDxe.efi`: Boot chime/audio support.
*   `OpenCanopy.efi`: GUI for OpenCore picker.
*   `OpenLinuxBoot.efi`: Linux dual-boot support.
*   `ResetNvramEntry.efi`: Adds Reset NVRAM option to picker.

## 📝 Usage Notes

*   **USB Mapping**: The included `USBMap.kext` is configured for this specific model. If you experience USB issues, you may need to remap your ports.
*   **Wi-Fi**: `itlwm.kext` is used, which typically requires the [HeliPort app](https://github.com/OpenIntelWireless/HeliPort) to connect to networks.
*   **AMD Spindown**: `SSDT-Disable_GPU_GPP0.aml` attempts to turn off the NVIDIA GPU to save battery.

## ⚠️ Disclaimer
Hackintoshing involves modifying system files and using unofficial software. Detailed knowledge of your hardware is recommended. Use this EFI at your own risk.