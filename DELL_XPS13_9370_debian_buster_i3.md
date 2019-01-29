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

startx

# keyboard, function keys (sound, brightness)
xev, pactl, xrandr, xmodmap -pke  
.i3/config/i3

vi ~/.xinitrc  
[[ -f ~/.Xmodmap ]] && xmodmap ~/.Xmodmap

# mouse, enable tap to click

vi ~/.config/i3/config

exec xinput set-prop 10 279 1


