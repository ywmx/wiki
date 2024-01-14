  Install Virtual-box Arch  body { background-color: black; color:white; font-family: monospace; font-size: 18px; } [SpaceLegion.wiki](index.html)  

Virtual-Box Install Arch

  
_sudo pacman -S virtualbox_  
  
And select the package virtualbox-host-modules-arch, ie option 2 while installing  
  
_sudo modprobe vboxdrv_  
  
_sudo nano /etc/modules-load.d/virtualbox.conf_ (type vboxdrv then save and exit, So we don't have to start it manually )  
  
_yay virtualbox-ext-oracle_ (or go to virtualbox's and download the extension pack https://www.virtualbox.org/wiki/Downloads)  
  
_sudo gpasswd -a $USER vboxusers_ (This is necessary in order to fully access the features provided by VirtualBox, including the ability to use USB devices in a Guest operating system.)