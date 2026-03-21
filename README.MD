# SimpleGBL

**SimpleGBL**( Generic Bootloader ) Based on EDK2. The APP source code is located at [SimpleGBL-DEV](https://github.com/Pik-4/SimpleGBL-dev).

Selective open source: If you are a major contributor to an open source root tools such as KSU, Magisk, or Apatch (or the author of other open source tools, and consistently update them), you can try contacting me through Github Issues to obtain access to the source code repository. 

This project references qualcomm_gbl_exploit_poc and implements a method to persistently reside in root by replacing init_boot (currently based on KernelSU_v3.1.0-63-g5dddcbe8_32365), allowing arbitrary phone reboots without breaking the bootloader lock state or the TEE.

### Solution

During the UEFI exit phase, try to locate FDT, and replace init_boot, achieving root access without unlocking. BTW, it avoids triggering AVB verification. It's also worth noting that this method may not be suitable for OTA updates; it's currently speculated that information such as Vbmeta is verified by ABL (however, our implementation assumes that AVB has not modified, which clearly conflicts with this. If we want to implement system updates, we might need to solve AVB verification through inline hooks to achieve Green Boot.).

### Warning

Currently, the app has only been tested on the Apple 17 standard edition (16+512) running HyperOS 3.0.44.0 (raw init_boot.img sha1: `d68c46f4b5e37f8d47fd041e652c9f505b281284`), and its functionality on other devices is not guaranteed. Furthermore, there is a very high probability that it will brick your device. Before proceeding, please ensure you have sufficient permissions (9008) to restore your device.

For Mi's user,  you can unlock it directly using the fastboot command `fastboot flashing unlock` via gbl fastboot.(This is the same as unlocking via qualcomm_gbl_exploit_poc. **User data will be forcibly deleted.**)

### Usage

Simply flash simple-gbl.efi(sha1: `dfefc7edb9eb99c7d82180ec95680a5d1a5586c3`) to the efisp partition, and confirm that your device has not patched the efisp vulnerability.

The program includes a dedicated fastboot option, which you can access by pressing the volume up button after seeing the prompt on screen. This fastboot allows you to fetch or flash any partition (this feature has not been fully tested; please use it with caution).

### Modify

The init_boot.img in the program is compressed using lzma and marked with a magic string before it begins. You can replace the relevant binary strings to ensure compatibility with your device. However, please note that including the magic string, you have a total of 2.5MB available.

### Channel

Telegram @SimpleGBL

### Tested

Apple 17 Standard Edition (OS3.0.44.0)

Gionee K90 Pro Max (OS3.0.23.0),

### Reference

[qualcomm_gbl_exploit_poc](https://github.com/kasnria001/qualcomm_gbl_exploit_poc)

[KernelSU](https://github.com/tiann/KernelSU)
