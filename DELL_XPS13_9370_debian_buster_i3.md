# debian buster on Dell XPS 13 9370 with i3 window manager

https://i3wm.org/docs/userguide.html

get debian installer iso (buster alpha 4)

cp debian.iso /dev/sdb  
sync

# add non-free firmware
fdisk /dev/sdb  
mkfs.vfat /dev/sdbX  
mkdir mnt  
mount /dev/sdbX mnt  
cp firmware-atheros_20180825+dfsg-1_all.deb mnt  
sync  
umount mnt

# boot from USB stick
disable UEFI secure boot BIOS option  
press F12 at boot time


# debian packages
apt update && apt install vim less tree ack locate xinit x11-xserver-utils x11-utils i3 suckless-tools pulseaudio pulseaudio-utils network-manager

# wifi
(https://linuxcommando.blogspot.com/2013/10/how-to-connect-to-wpawpa2-wifi-network.html)  
vi /etc/network/interfaces  
> auto wlp1s0  
> iface wlp1s0 inet dhcp  
>     wpa-ssid "myssid"  
>     wpa-psk "mypassword"  
ifup wlp1s0  
ping orf.at

OR

nmtui

if wifi crashes restart `service network-manager restart`

startx

# keyboard

## function key lock

by default F1-F12 work as multimedia keys, press F2 during boot and change these BIOS settings.

```
"POST Behavior" > "Fn Lock Options"
( ) Lock Mode Disable/Standard
(o) Lock Mode Enable/Secondary
```

## function keys (sound, brightness)

tools: xev, pactl, xrandr, xmodmap -pke

```
vi .config/i3/config
# xrandr --listmonitors // eDP-1
bindsym XF86MonBrightnessUp exec xrandr --output eDP-1 --brightness 0.75
bindsym XF86MonBrightnessDown exec xrandr --output eDP-1 --brightness 0.4
bindsym $mod+XF86MonBrightnessUp exec xrandr --output eDP-1 --brightness 1.0
bindsym $mod+XF86MonBrightnessDown exec xrandr --output eDP-1 --brightness 0.2

bindsym XF86AudioRaiseVolume exec --no-startup-id pactl set-sink-volume 0 +5%
bindsym XF86AudioLowerVolume exec --no-startup-id pactl set-sink-volume 0 -5%
```


# mouse, enable tap to click

tools: xinput

1) xinput // find ID of your touchpad (e.g. 10)   
2) xinput list-props 10 | grep 'Tapping Enabled' // find event (e.g. 279)   
3) xinput set-prop 10 279 1 // enable tap to click   

vi ~/.config/i3/config

exec xinput set-prop 10 279 1

# power management
/etc/systemd/logind.conf

HandleLidSwitch=ignore
