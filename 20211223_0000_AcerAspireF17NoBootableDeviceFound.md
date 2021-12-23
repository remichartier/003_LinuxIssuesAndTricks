# "No Bootable Device Found"

## Background

- Tried to install Debian and Ubuntu on a Windows 10 laptop however it was blocked by secure boot.

- --> F2 boot for UEFI/BIOS, had to set the Supervisor Password, in order to disable `Secure boot`.

- Then could install Debian/Ubuntu via USB Disk.

- At the end of install, installer request to eject USB stick and reboot.

- Then we get this black screen at the boot, saying "No Bootable Devce Found", like in article https://itsfoss.com/no-bootable-device-found-ubuntu/.

## Solution

- As mentioned in https://itsfoss.com/no-bootable-device-found-ubuntu/ : 

  - boot with F2 --> Enter UEFI/BIOS, menu boot, *re-enable Secure Boot*, and follow instructions from https://itsfoss.com/no-bootable-device-found-ubuntu/, ie : 

    - Step 1

Turn the power off and boot into boot settings. I had to press Fn+F2 (to press F2 key) on Acer Aspire R13 quickly. You have to be very quick with it if you are using SSD hard disk because SSDs are very fast in booting. Depending upon your manufacturer/model, you might need to use Del or F10 or F12 keys.

    - Step 2
    
In the boot settings, make sure that Secure Boot is turned on. It should be under the Boot tab.

    - Step 3
    
Go to Security tab and look for “Select an UEFI file as trusted for executing” and click enter.

Fix no bootable device found 
Just for your information, what we are going to do here is to add the UEFI settings file (it was generated while Ubuntu installation) among the trusted UEFI boots in your device. If you remember, UEFI boot’s main aim is to provide security and since Secure Boot was not disabled (perhaps) the device did not intend to boot from the newly installed OS. Adding it as trusted, kind of whitelisting, will let the device boot from the Ubuntu UEFI file.

    - Step 4
You should see your hard disk like HDD0 etc here. If you have more than one hard disk, I hope you remember where did you install Ubuntu. Press Enter here as well.

Fix no bootable device found in boot settings

    - Step 5

You should see <EFI> here. Press enter.

Fix settings in UEFI

    - Step 6
You’ll see <Ubuntu> in next screen. Don’t get impatient, you are almost there :)

Fixing boot error after installing Ubuntu

    - Step 7
Fix no bootable device found 
You’ll see shimx64.efi, grubx64.efi and MokManager.efi file here. The important one is shimx64.efi here. Select it and click enter.

In next screen, type Yes and click enter.

No_Bootable_Device_Found_7

    - Step 8
Once we have added it as trused EFI file to be executed, press F10 to save and exit.

Save and exist firmware settings
Reboot your system and this time you should be seeing the familiar Grub screen. Even if you do not see Grub screen, you should at least not be seeing “no bootable device found” screen anymore. You should be able to boot into Ubuntu.

If your Grub screen was messed up after the fix but you got to login into it, you can reinstall Grub to boot into the familiar purple Grub screen of Ubuntu.
