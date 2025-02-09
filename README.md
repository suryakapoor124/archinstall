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

**ACTUAL INSTALLATION**
CTRL+L = Clear Screen

**INSIDE THE ARCHTERMINAL**
1)loadkeys us (keyboard style = united states)
2) iwctl > station wlan0 get-networks > station wlan0 connect meowbile    (USed to connect wifi with cli)
3)cfdisk (a disk part tool for linux cli)
#partation
4) Create following partations 
     100M = Boot partation
     16G = Virtual Memory Part (SWAP,      used when your RAM gets full, keep 16 if you have space or else 8 or 4 gigs is fine)
     Rest = Your main storage'
make sure to write the changes (write = save)

# changing partation type 
5) lsblk
6) mkfs.ext4 /dev/sda7 (ext4 = linux file system , 7 in sda7 can be anything)          [ROOT PARTATION]
7) mkfs.fat -F 32 /dev/sda5   (fat -F 32 is file system for FAT32)                    [BOOT PARTATION]
8) mkswap /dev/sda6  (create a swap partation)                                        [SWAP PARTATON]

#mounting partations
9) mount /dev/sda7 /mnt      
10) mkdir -p /mnt/boot/efi  (make this directory so that you can mount the boot part here)
11) mount /dev/sda5 /mnt/boot/efi
12) swapon /dev/sda6 (We don't mount the SWAP, we trun that on by this command)
13) confirm if by running lsblk , it should look like this 

          Photo attached


#IMPORTANT package installation
14) pacstrap /mnt base linux linux-firmware sof-firmware base-devel grub efibootmgr vim nano networkmanager.

15)genfstab /mnt (give info about file system )

16) genfstab /mnt > /mnt/etc/fstab () transfer the command's contents to fstab file.

17) arch-chroot /mnt (chroot means changeRoot into mnt)

18) ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime (set date and time)

19) hwclock --systohc (syncronize system clock)

#localization
20) vim /etc/locale.gen

21) find es_US.UTF-8 and uncomment this.

22) locale-gen

23)open /etc/locate.conf with vim 

24)add "LANG=en_US.UTF-8" and save it.

25)open "/etc/hostname" and type the hostname there

26)passwd (to setup passwod)

27) useradd -m -G wheel -s /bin/bash username (to add new user) > passwd username

28) "EDITOR=vim visudo"  and uncomment the line "%wheel ALL=(ALL)"  (give sudo access to user)

#ENABLING CORE SERVICES
29) sudo systemctl enable NetworkManager

30) grub-install /dev/sda

31)grub-mkconfig -o /boot/grub/grub.cfg

32)"sudo vim /etc/default/grub" and uncomment this "GRUB_DISABLE_OS_PROBER=true"

33) grub-mkconfig -o /boot/grub/grub.cfg

34) exit > umount -a (to unmount all unactive partations)

35) reboot
