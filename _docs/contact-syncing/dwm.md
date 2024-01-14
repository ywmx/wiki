  DWM Setup Guide  body { background-color: black; color:white; font-family: monospace; font-size: 18px; } [SpaceLegion.wiki](index.html)  

dwm installation guide

  
1 Complete arch linux base installation and also install your Gpu drivers  
  
2 _\# sudo pacman -S xorg-server xorg-xinit xorg-xsetroot xorg-xrandr firefox/chromium nitrogen picom dmenu nano_  
  
(basic display server, web browser, nitrogen- for wallpaper, picom- compositor dmenu- quick access menu, xrandr- setting display resolution)  
  
3 _\# cp /etc/X11/xinit/xinitrc .xinitrc_ (copies xinitrc for lauching WM and starting other daemon process)  
  
4 _\# nano .xinitrc_ (clear the last five lines)  
  
_setxkbmap en &  
  
picom -f &  
  
exec dwm  
  
_Add this, then save and exit nano  
  
5 _\# sudo pacman -S wget_ (retrieves content from web servers)  
  
6 _\# wget https://dl.suckless.org/dwm/dwm-6.2.tar.gz_  
  
(This downloads dwm from suckless's website. If the url is broken, visit suckless for upstream https://dwm.suckless.org/)  
  
7 _\# tar -xzvf dwm-6.2.tar.gz_ (This extracts dwm tar file)  
  
8 _\# cd dwm-6.2_  
  
9 _\# sudo make clean install_ (This will compile and install dwm)  
  
10 _\# sudo pacman -S xfce4-terminal_ (Installs xfce4 terminal)  
  
12 _\# nano config.def.h_  
  
Replace _"st"_ with xfce4-terminal in following line "static const char *termcmd\[ \]= {"xfce4-terminal", NULL};"  
  
then, save and exit nano  
  
13 _\# rm config.h_  
  
Type yes for removing the file  
  
14 _\# sudo make clean install_  
  
15 _\# reboot_  
  
16 _\# sudo nano /etc/xdg/picom.conf_  
  
comment out vsync true;, ie _\# vsync true;_ (Only do this if you are in a Virtual Machine)  
  
then save and exit nano  
  
17 _\# reboot_  
  
18 _\# startx_  
  
19 _\# nano .xinitrc_  
  
Add this command after the setxkbmap line  
  
xrandr --output "your display name" --mode "your resolution" & (Only do this if you are in a Virtual Machine)  
  
To get your display name type _xrandr_ in terminal  
  
Example:- _\# xrandr --output DisplayPort-0 --mode 1920x1080 &_  
  
save and exit nano  
  
20 _\# reboot_  
  
Alt + P , this opens dmenu. search nitrogen and open it > add a folder for the wallpaper directory and select an image and apply ( you can choose automatic, scaled zoom etc optional)  
  
21 _\# nano .xinitrc_  
  
Add a line new after picom  
  
_nitrogen --restore &_  
  
Enter the following lines after the nitrogen's line  
  

_while true; do_

_dwm >/dev/null 2>&1_

_done_

  
This command will start a while loop.  
  
save and exit nano  
  
Press Alt+shift+Q to exit and startx and then again alt+shift+q to test this  
  
23_\# sudo pacman -S pulseaudio pamixer pavucontrol_  
  
open terminal and type pavucontrol to launch audio manager and to control other audio input or output devices  
  
By [Nebulaxyz](https://github.com/nebulaxyz)