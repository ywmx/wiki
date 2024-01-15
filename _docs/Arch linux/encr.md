---
title: Arch linux encryption guide
category: Arch linux
order: 1
---


# Install Arch Linux in UEFI System

[SpaceLegion.wiki](index.html)

**After booting into Arch ISO**

1. `# ping stallman.org` (to check internet connectivity)
2. `# timedatectl set-ntp true` (to ensure the system clock is accurate)
3. `# lsblk` (to list all partitions with drives)
4. `# cfdisk /dev/sda` (your hard disk name)

**For a basic partition.**

- EFI System partition (/dev/sda1) with 512M size, FAT32 formatted.
- Root partition (/dev/sda2) with at least 20G size or rest of HDD space, ext4 formatted.
- Home directory is optional.

    - Select new type the partition size in MB (512M) and press enter key, select Type from the bottom menu and choose EFI.
    - For /(root) partition use the following configuration: New -> Size: rest of free space -> Type Linux filesystem.
    - Then select Write, answer with yes in order to apply disk changes and then Quit the utility.
    - Type `lsblk` to review your changes.

5. `# mkfs.fat -F32 /dev/sda1` (creates a FAT32 file system for EFI System partition)
6. `# mkfs.ext4 /dev/sda2` (create the EXT4 file system for the root partition)

```bash
# mkfs.ext4 /dev/sdX
# mkdir /mnt/home
# mount /dev/sdX /mnt/home  # optional, if you need a home partition
# mount /dev/sda2 /mnt (In order to install Arch Linux, the /(root) partition must be mounted to /mnt directory mount point)
# mkdir -p /mnt/boot/efi (making a directory for EFI installation)
# mount /dev/sda1 /mnt/boot/efi (mounting EFI for installation)
# pacman -Syy (to sync)
# pacstrap /mnt base base-devel linux linux-firmware vim (installs base system, base development tools, Linux kernel, firmware, CLI editor)
# genfstab -U /mnt >> /mnt/etc/fstab (generates fstab file for your new Linux system)
```
Arch Linux System configuration

# arch-chroot /mnt (chroots into /mnt the system path)

# ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime (configure your region and city, This is an example)

# hwclock --systohc (configure the hardware clock to use UTC, the hardware clock is usually set to the local time)

# vim /etc/locale.gen (Configuring your system Language. Choose and uncomment your preferred encoding languages from /etc/locale.gen)

In this scenario - "en_US.UTF-8 UTF-8", "en_US ISO-8859-1"

# locale-gen (Generates your system language layout)

# echo LANG=en_US.UTF-8 >> /etc/locale.conf (This assigns English as the default language)

# echo Arch Linux >> /etc/hostname (type a name for your host, e.g., Archlinux)

# passwd (create a password for the root user)

# pacman -S grub efibootmgr networkmanager (installs grub, efibootmgr for UEFI system, and network manager)

# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB (installs grub)

# grub-mkconfig -o /boot/grub/grub.cfg (creating GRUB configuration file)

# systemctl enable NetworkManager (enabling it from boot itself)

# useradd -mG wheel "username" (creates a user account with sudo permissions)

# passwd "username" (create a password for the user account)

# EDITOR=vim visudo (adding the user account to sudoers group)

Uncomment "%wheel ALL=(ALL) ALL" Then save and exit

# exit (exiting chroot environment)

# umount -R /mnt (This will unmount drives)

# reboot

The base installation has been finished

Setting up your desktop

# pacman -S xorg (display server)
Installing Graphics drivers

If you're installing Arch in VirtualBox, you should install the VirtualBox Guest Additions. The VirtualBox Guest Additions contain the video drivers. You can install the guest additions from the Arch repositories.

bash
Copy code
# pacman -S linux-headers
# pacman -S virtualbox-guest-utils
# systemctl enable vboxservice
For AMD GPU

bash
Copy code
# pacman -S xf86-video-amdgpu
# pacman -S xf86-video-ati  # (older cards only)
For Intel

bash
Copy code
# pacman -S xf86-video-intel  # (Warning: If you are planning to install the Cinnamon desktop environment, skip this driver install)
For Nvidia

bash
Copy code
# pacman -S xf86-video-nouveau
# pacman -S nvidia  # (This is a proprietary driver)
Installing a desktop environment

Listed below are most of the popular desktop environments and their associated packages. Pick the one you like and install it!

XFCE: xfce4 xfce4-goodies
GNOME: gnome gnome-extra
KDE: plasma kde-applications
Cinnamon: cinnamon
MATE: mate mate-extra
LXDE: lxde
LXQt: lxqt
Note: For the GTK-based desktops (XFCE, GNOME, Cinnamon, MATE, and LXDE), you'll want to install gvfs alongside the desktop to get wastebasket and mounting support for regular users. Install gvfs-mtp as well if you're planning to connect your Android phone.

Cinnamon as an example:

bash
Copy code
# pacman -S cinnamon gvfs gvfs-mtp gnome-terminal gnome-screenshot blueberry
(gvfs & gvfs-mtp - Mounting support for android devices, terminal for the Linux terminal emulator, screenshot for their purpose, blueberry for the Bluetooth adapter)

Installing and setting up a Display Manager

XFCE: lightdm gdm
GNOME: gdm lightdm
KDE: sddm
LXDE: lightdm
LXQt: sddm
LightDM as an example:

bash
Copy code
# pacman -S lightdm lightdm-webkit2-greeter
# sudo nano /etc/lightdm/lightdm.conf  # (uncomment greeter-sessions)
rename it to greeter-sessions=lightdm-webkit2-greeter

To enable it from boot

bash
Copy code
# systemctl enable lightdm
For Audio

Pulseaudio is recommended. To install:-

bash
Copy code
# pacman -S pulseaudio pulseaudio-alsa pavucontrol
Recommended Common Packages

bash
Copy code
# pacman -S ntfs-3g git celluloid vlc rhythmbox feh xed chromium firefox gvfs gvfs-mtp
(ntfs-3g- support for ntfs drives, git- git tools, celluloid- video player, Vlc- video player, rhythmbox- music player, feh- image viewer, xed- text editor, chromium & firefox- browsers,gvfs & gvfs-mtp- Mounting support for android devices)

bash
Copy code
# reboot
Extras:- If your mirrors are slow you can change it by using the following command, reflector package is required.

bash
Copy code
# pacman -S reflector
# reflector --verbose --latest 50 --sort rate --save /etc/pacman.d/mirrorlist  # (Add all mirrors generated from the Arch Linux official website.)
Arch Linux Mirrors

bash
Copy code
# reflector --verbose --country 'Canada' -l 5 --sort rate --save /etc/pacman.d/mirrorlist
Retrieves the top five mirrors of Canada according to the download rate and saves them to the mirrorlist file.

Extras:- Opening tty- Alt+control+F2, closing tty- Alt+control+F7

Bonus:- Cinnamon DE recommendations - lightdm-slick-greeter lightdm-settings (edit it from /etc/lightdm/lightdm.conf, modify the value of greeter-session) (from yay), arc-gtk-theme papirus-icon-theme (pacman)

By Nebulaxyz