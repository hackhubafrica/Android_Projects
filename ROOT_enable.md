Enable Developer Options and USB Debugging

Alloe OEM unlocking

adb reboot bootloder to go into fastboot mode

fastboot oem unlock $$$ fastboot flashing unlock to unlock the bootloader

Phone will be reset and you have to re-enable developer options and ...

Download ZIP file which is pretty big ,extract it and locate a boot.img file or recover.img

# If RamDisk is Yes-You willl need to download ,patch and flash boot

# If RamDisk is NO-You willl need to download ,patch and flash Recovery


Transfer this file to Android phone

Download Magisk and patch this boot.img or recovery.img file
 
Transfer this file to your PC magisk_patched.img

adb reboot bootloder to go into fastboot mode

fastboot flash boot magisk_patched.img

Reboot phone



