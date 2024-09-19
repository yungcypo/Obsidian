# Arch Linux Installation - Quick
There is a list of commands which are required to install Arch Linux  

> Note: If you want to understand it more, check out [the other one](./Arch.md)  

## Wifi
> It's just a lot easier to use Ethernet...
```shell
iwctl  
device list

device *device* set-property Powered on 
adapter *adapter* set-property Powered on 

station *device* scan
station *device* get-networks

station *device* connect *SSID*

exit

ping google.com
```

## Clock sync
```shell
timedatectl set-ntp true
```

## Partitioning, formatting, mouting
```shell
# make partitions
lsblk
cfdisk /dev/*drive*

# fortmat partitions
mkfs.ext4 /dev/*drive*1
mkfs.ext4 /dev/*drive*2

# mouting partitions
mkdir -p /mnt/boot
mount /dev/*drive*1 /mnt/boot
mount /dev/*drive*2 /mnt
```

## Installing
```shell
pacstrap /mnt base linux linux-firmware vim
```

## `fstab`
```shell
genfstab -U /mnt >> /mnt/etc/fstab
```

## Post-install config
```shell
# log in as root & change password
arch-chroot /mnt /bin/bash
passwd

# download additional packages
pacman -Sy networkmanager grub gnome

# enable packages on startup
systemctl enable NetworkManager
systemctl enable gdm

# grub
grub-install /dev/*drive*
grub-mkconfig -o /boot/grub/grub.cfg
```

## Optional
These can be done after booting to gnome, but you can do them now as well
```shell
# locales
vim /etc/locale.gen  # uncomment desired locale 
locale-gen

# language & hostname
echo "LANG=en_US.UTF-8" >> /etc/locale.conf
echo "arch" >> /etc/hostname

# timezone
ln -sf /usr/share/zoneinfo/Europe/Bratislava /etc/localtime
```

## Reboot
```shell
exit
reboot now
```

## `yay`
```shell
pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay .yay
cd .yay
makepkg -si
```