# archinstall
So is this repo I'm gonna show you guys how you can install art Linux on your system. Just follow my steps and you are good to go.

**Boot Without USB**
1) Downlaod the ISO and mount that.
2) Make a FAT32 Partition 8GB approx size
3) Convert that into EFI with cmd (DISKPART)
     Open CMD > DISKPART > sel disk 0 > sel part 4 > help set (this command is used to converstion ) > use set id = xxxxxxxxxxxx and then its converted into efi
4) Then copy the mounted content into that 8GB partition.
5) You can now reboot and boot into that.


**Make bootable USB**

You can make the USB bootable with a software called **Balena Etcher** and the steps are pretty basic you can easily do it on your own.

