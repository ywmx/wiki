  BSPWM Installation Guide  body { background-color: black; color: white; font-family: monospace; font-size: 18px; }  [SpaceLegion.wiki](index.html)  

BSPWM Install Guide

=======================================

  
  

1 Complete arch linux base installation and also install your Gpu drivers

  
  

2 # sudo pacman -S xorg-server xorg-xinit xorg-xsetroot xorg-xrandr firefox nitrogen picom dmenu bspwm sxhkd xfce4-terminal

  

(basic display server, web browser, nitrogen- for wallpaper, picom- compositor dmenu- quick access menu, xrandr- setting display resolution, bspwm- window manager, sxhkd- hot key daemon, xfce4- terminal emulator)

  
  

3 # mkdir .config/bspwm (creates configs directory)

  
  

4 # mkdir .config/sxhkd (creates configs directory)

  
  

5 # cp /usr/share/doc/bspwm/examples/bspwmrc .config/bspwm/ (copy sample configs to home directory)

  
  

6 # cp /usr/share/doc/bspwm/examples/sxhkdrc .config/sxhkd/ (copy sample configs to home directory)

  
  

7 # vim .config/sxhkd/sxhkdrc (find terminal emulator section and change it from urxvt to xfce4-terminal

  
  

8 # cp /etc/X11/xinit/xinitrc .xinitrc (copies xinitrc for lauching WM and starting other daemon process)

  
  

9 # vim .xinitrc (remove last 5 lines)

  
  

10 # sudo nano /etc/xdg/picom.conf

  

(Only do this if you are in a Virtual Machine) comment out vsync true;, ie # vsync true;

  
  

11 # startx (to start the window manager)

  
  

12 # vim .xinitrc (add "xsetroot -cursor\_name left\_ptr" above the picom line to get a pointer mouse instead of x)

  
  

13 # vim .xinitrc

  

Add this command after the setxkbmap line

  
  

xrandr --output "your display name" --mode "your resolution" & (Only do this if you are in a Virtual Machine)

  
  

To get your display name type xrandr in terminal

  
  

Example:- # xrandr --output DisplayPort-0 --mode 1920x1080 &

  
  

Alt + P , this opens dmenu. search nitrogen and open it > add a folder for the wallpaper directory and select an image and apply ( you can choose automatic, scaled zoom etc optional)

  
  

15 # vim .xinitrc

  
  

Add a line new after picom

  
  

nitrogen --restore & (restores your wallpaper)