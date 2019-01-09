# debian buster on Dell XPS 13 9370 with i3 window manager

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


disable UEFI secure boot BIOS option
press F12 at boot time


# wifi (https://linuxcommando.blogspot.com/2013/10/how-to-connect-to-wpawpa2-wifi-network.html)
vi /etc/network/interfaces
> auto wlp1s0
> iface wlp1s0 inet dhcp
>     wpa-ssid "myssid"
>     wpa-psk "mypassword"
ifup wlp1s0
ping orf.at
apt update && apt install vim less tree ack locate xinit x11-xserver-utils i3 suckless-tools pulseaudio pulseaudio-utils

startx

# keyboard function keys
xev, pactl, xrandr, xmodmap -pke
.i3/config/i3

