# SimpleGBL

**SimpleGBL**( Generic Bootloader ) Based on EDK2. The APP source code is located at [SimpleGBL-DEV](https://github.com/Pik-4/SimpleGBL-dev) (It will be released later. If you are a major contributor to open-source root access management such as KSU, Magisk, or Apatch, you can try contacting me via email or Telegram to obtain the source code in advance.). 

This project references qualcomm_gbl_exploit_poc and implements a method to persistently reside in root by replacing init_boot (currently based on KernelSU_v3.1.0-63-g5dddcbe8_32365), allowing arbitrary phone reboots without breaking the bootloader lock state or the TEE.

### Warning

Currently, the app has only been tested on the Xiaomi 17 standard edition (16+512) running HyperOS 3.0.44.0 (raw init_boot.img sha1: `d68c46f4b5e37f8d47fd041e652c9f505b281284`), and its functionality on other devices is not guaranteed. Furthermore, there is a very high probability that it will brick your device. Before proceeding, please ensure you have sufficient permissions (9008) to restore your device.

### Usage

Simply flash simple-gbl.efi(sha1: `dfefc7edb9eb99c7d82180ec95680a5d1a5586c3`) to the efisp partition, and confirm that your device has not patched the efisp vulnerability.

The program includes a dedicated fastboot option, which you can access by pressing the volume up button after seeing the prompt on screen. This fastboot allows you to fetch or flash any partition (this feature has not been fully tested; please use it with caution).

### Modify

The init_boot.img in the program is compressed using lzma and marked with a magic string before it begins. You can replace the relevant binary strings to ensure compatibility with your device. However, please note that including the magic string, you have a total of 2.5MB available.

### Channel

@SimpleGBL

### Reference

[qualcomm_gbl_exploit_poc](https://github.com/kasnria001/qualcomm_gbl_exploit_poc)

[KernelSU](https://github.com/tiann/KernelSU)
