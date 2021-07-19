# Asus X205TA on Debian list of fix
*Tested on GNU/Linux Debian 11 RC1 LXQT with kernel 5.10.0-7*

## Fix Wifi

todo...

you can check : https://wiki.debian.org/InstallingDebianOn/Asus/X205TA#WiFi

## Activate tap to click on the touchpad
*Based on https://askubuntu.com/questions/1087328/lubuntu-18-10-how-to-activate-tap-to-click#answer-1088009*

`sudo nano /etc/X11/xorg.conf.d/30-touchpad.conf`


>```
>Section "InputClass"   
>  Identifier "touchpad"  
>  Driver "libinput"  
>  MatchIsTouchpad "on"  
>  Option "Tapping" "on"  
>EndSection
>```

`sudo systemctl reboot`

## Disable Hibernation
*Based on https://wiki.debian.org/Suspend#Disable_suspend_and_hibernation*

`sudo systemctl mask hibernate.target hybrid-sleep.target`

## Fix touchpad and network will not respond after resume
*Based on https://wiki.debian.org/InstallingDebianOn/Asus/X205TA#Battery*

`sudo nano /opt/fixaftersleep.sh`
 
>```
>sudo modprobe -r elan_i2c
>sudo modprobe -r brcmfmac
>sudo modprobe brcmfmac
>sudo modprobe elan_i2c
>```
 
`sudo chmod +x /opt/fixaftersleep.sh`
 
`sudo nano /usr/lib/systemd/system-sleep/after-resume.sh`
 
>```
>#!/bin/bash
>if [ "${1}" == "post" ]; then
>        /opt/fixaftersleep.sh
>fi
>```
 
`sudo chmod +x /usr/lib/systemd/system-sleep/after-resume.sh`

---

### Bonus neofetch

```
       _,met$$$$$gg.          avak@X205TA
    ,g$$$$$$$$$$$$$$$P.       ---------- 
  ,g$$P"     """Y$$.".        OS: Debian GNU/Linux 11 (bullseye) i686 
 ,$$P'              `$$$.     Host: X205TA 1.0 
',$$P       ,ggs.     `$$b:   Kernel: 5.10.0-7-686-pae 
`d$$'     ,$P"'   .    $$$    Uptime: 20 mins 
 $$P      d$'     ,    $$P    Packages: 1687 (dpkg) 
 $$:      $$.   -    ,d$$'    Shell: bash 5.1.4 
 $$;      Y$b._   _,d$P'      Resolution: 1366x768 
 Y$$.    `.`"Y$$$$P"'         DE: LXQt 0.16.0 
 `$$b      "-.__              WM: Xfwm4 
  `Y$$                        WM Theme: Breeze 
   `Y$$.                      Theme: Adwaita [GTK3] 
     `$$b.                    Icons: Adwaita [GTK3] 
       `Y$$b.                 Terminal: qterminal 
          `"Y$b._             Terminal Font: Monospace 11 
              `"""            CPU: Intel Atom Z3735F (4) @ 1.832GHz 
                              GPU: Intel Atom Processor Z36xxx/Z37xxx Series Graphics & Displa 
                              Memory: 587MiB / 1896MiB 
```
