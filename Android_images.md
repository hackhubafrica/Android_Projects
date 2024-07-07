If RamDisk is Yes-You willl need to download ,patch and flash boot

If RamDisk is NO-You willl need to download ,patch and flash Recovery

2 Ways to get boot.img OR recovery.img
	-from the phone itself
	-from the internet

Download your recovery software(whether twrp or cwn) go into fastboot mode and temporary boot into custom recovery -- fastboot boot twrp.img

Once into custom recovery run adb shell and and ls command
 
ls -al --color $(find /dev|grep by-name$)

dd if=<boot path> of=/sdcard/boot.img
