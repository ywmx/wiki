  Install Arch Linux in Legacy system  body { background-color: black; color:white; } [SpaceLegion.wiki](index.html)  
  

**After booting into Arch iso**  
  
1 _\# ping stallman.org_ (to check internet connectivity)  
  
2 _\# timedatectl set-ntp true_ (to ensure the system clock is accurate)  
  
3 _\# lsblk_ (to list all partitions with drives)  
  
4 _\# cfdisk /dev/sda_ (your hardisk name)  
  
  
**For a basic partition.**  
=====================  
  
BIOS System partition (/dev/sda1) with 128M (512M might be a lit bit too much or its your choice )size, ext4 formatted.  
  
Root partition (/dev/sda2) with at least 20G size or rest of HDD space, ext4 formatted.  
  
Home directory is optional.  
  
=\> Select new type the partition size in 128MB and press enter key, make it bootable by clicking 'B'  
  
=\> For /(root) partition use the following configuration: New -> Size: rest of free space -> Type Linux filesystem.  
  
Then select Write, answer with yes in order to apply disk changes and then Quit the utility  
  
Type lsblk to review your changes.  
  
  
5 _\# mkfs.ext4 /dev/sda1_ (creates a file system for bios System partition)  
  
6 _\# mkfs.ext4 /dev/sda2_ (create the EXT4 file system for the root partition)  
  
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
  
_\# mkfs.ext4 /dev/sdX_  
  
_\# mkdir /mnt/home_  
  
_\# mount /dev/sdX /mnt/home_ \- optional, if you need home partition  
  
\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-  
  
7 _\# mount /dev/sda2 /mnt_ (In order to install Arch Linux, the /(root) partition must be mounted to /mnt directory mount point)  
  
8 _\# mkdir /mnt/boot_ (In order to make sda1 mount on boot directory)  
  
9 _\# mount /dev/sda1 /mnt/boot_ (mounting sda1 to boot directory)  
  
10 _\# pacman -Syy_ (to sync)  
  
11 _\# pacstrap /mnt base base-devel linux linux-firmware vim_ (installs base system, base development tools, linux kernel, firmware, cli editor)  
  
12 _\# genfstab -U /mnt >> /mnt/etc/fstab_ (generates fstab file for your new Linux system)  
  
**Arch Linux System configuration**  
===============================  
  
13 _\# arch-chroot /mnt_ (chroots into /mnt the system path)  
  
14 _\# ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime_ (configure your region and city, This is an example)  
  
15 _\# hwclock --systohc_ (configure the hardware clock to use UTC, the hardware clock is usually set to the local time)  
  
16 _\# vim /etc/locale.gen_ (Configuring your system Language. Choose and uncomment your preferred encoding languages from /etc/locale.gen)  
  
In this scenario- "en\_US.UTF-8 UTF-8", "en\_US ISO-8859-1"  
  
17 _\# locale-gen_ (Generates your system language layout)  
  
18 _\# echo LANG=en_US.UTF-8 >> /etc/locale.conf_ (This assigns english as default language)  
  
19 _\# echo Arch Linux >> /etc/hostname_ (type a name for your host, eg: Archlinux)  
  
20 _\# passwd_ (create a password for root user)  
  
21 _\# pacman -S grub networkmanager_ (installs grub, network manager)  
  
22 _\# grub-install /dev/sda_ (installing grub on the entire drive )  
  
23 _\# grub-mkconfig -o /boot/grub/grub.cfg_ (creating GRUB configuration file)  
  
24 _\# systemctl enable NetworkManager_ (enabling it from boot itself)  
  
25 _\# useradd -mG wheel "username"_ (creates a user account with sudo permissions)  
  
26 _\# passwd "username"_ (create a password for user account)  
  
27 _\# EDITOR=vim visudo_ (adding user account to sudoers group)  
  
uncomment "%wheel ALL=(ALL) ALL" Then save and exit  
  
28 _\# exit_ (exiting chroot environment)  
  
29 _\# umount -R /mnt_ (This will unmount drives)  
  
30 _\# reboot_  
  
**The base installation has been finished**  
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  
  
Setting up your desktop  
=======================  
  
24 # _pacman -S xorg_ (display server)  
  
Installing Graphics drivers  
===========================  
If you're installing Arch in VirtualBox you should install the VirtualBox Guest Additions. The VirtualBox Guest Additions contain the video drivers, You can install the guest additions from the Arch repositories  
  
\# _pacman -S linux-headers_  
\# _pacman -S virtualbox-guest-utils_  
\# _systemctl enable vboxservice_  
  
For AMD GPU  
===========  
\# _pacman -S xf86-video-amdgpu_  
\# _pacman -S xf86-video-ati_ (older cards only)  
  
For Intel  
=========  
\# _pacman -S xf86-video-intel_ (Warning, If you are planning to install cinnamon destop environment, skip this driver install)  
  
For Nvidia  
==========  
\# _pacman -S xf86-video-nouveau_  
\# _pacman -S nvidia_ (This is a properietary driver)  
  
Installing a desktop environment  
================================  
  
Listed below are most of the popular desktop environments and their associated packages. Pick the one you like and install it!  
  
\* XFCE- _xfce4 xfce4-goodies_  
\* GNOME- _gnome gnome-extra_  
\* KDE- _plasma kde-applications_  
\* Cinnamon- _cinnamon_  
\* MATE- _mate mate-extra_  
\* LXDE- _lxde_  
\* LXQt- _lxqt_  
  
Note:- For the GTK-based desktops (XFCE, GNOME, Cinnamon, MATE and LXDE), you'll want to install gvfs alongside the desktop to get wastebasket and mounting support for regular users. Install gvfs-mtp as well if you're planning to connect your Android phone.  
  
Cinnamon as an example:  
======================  
  
\# _pacman -S cinnamon gvfs gvfs-mtp gnome-terminal gnome-screenshot blueberry_  
  
(gvfs & gvfs-mtp- Mounting support for android devices, terminal for linux terminal emulator, screenshot for there purpose, blueberry for bluetooth adapter)  
  
Installing and setting up a Display Manager  
===========================================  
XFCE- _lightdm gdm_  
GNOME- _gdm lightdm_  
KDE- _sddm_  
LXDE- _lightdm_  
LXQt- _sddm_  
  
LightDM as an example:  
=====================  
  
\# _pacman -S lightdm lightdm-webkit2-greeter_  
\# _sudo nano /etc/lightdm/lightdm.conf_ (uncomment greeter-sessions)  
  
rename it to _greeter-sessions=lightdm-webkit2-greeter_  
  
To enable it from boot  
======================  
  
\# _systemctl enable lightdm_  
  
For Audio  
=========  
Pulseaudio is recommended. To install:-  
  
\# _pacman -S pulseaudio pulseaudio-alsa pavucontrol_  
  
Recommended Common Packages  
===========================  
  
\# _pacman -S ntfs-3g git celluloid vlc rhythmbox feh xed chromium firefox gvfs gvfs-mtp_  
  
(ntfs-3g- support for ntfs drives, git- git tools, celluloid- video player, Vlc- video player, rhythmbox- muisc player, feh- image viewer, xed- text editor, chromium & firefox- browsers,gvfs & gvfs-mtp- Mounting support for android devices)  
  
25 # reboot  
  
**Extras:-** If your mirrors are slow you can change it by using the following command, reflector package is required.  
  
\# _pacman -S reflector_  
  
\# _reflector --verbose --latest 50 --sort rate --save /etc/spacman.d/mirrorlist_ (Add all mirrors generated from the arch linux official website.)  
  
**[Arch linux Mirrors](https://www.archlinux.org/mirrorlist/all/)**  
  
\# _reflector --verbose --country 'Canada' -l 5 --sort rate --save /etc/pacman.d/mirrorlist_  
  
Retrieves top five mirrors of Canada according to the download rate, and save them to the mirrorlist file.  
  
**Extras:-** opening tty- Alt+control+F2, closing tty- Alt+control+F7  
  
**Bonus:-** Cinnamon DE recommendations - lightdm-slick-greeter lightdm-settings (edit it from /etc/lightdm/lightdm.conf,modify value of greeter-session) (from yay), arc-gtk-theme papirus-icon-theme (pacman)  
  
By **[Nebulaxyz](https://github.com/nebulaxyz)**