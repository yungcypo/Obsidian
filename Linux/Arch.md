# Arch Linux Installation
There is a quick guide to install Arch Linux  

> Note: There is also file called [ArchQuick](./ArchQuick.md), which is basically the same, but only commands without explanation 

## Arch Linux ISO
First of all, you need to download Arch Linux ISO  
Go to [archlinux.org/download/](https://archlinux.org/download/) and download it from there  

After downloading, make a bootable USB or use the ISO on VM or whatever you want and start it  

## First steps
### Internet connection
First, you need to make sure you have internet connection  
Connecting cable is the easiest thing to do  

I you have to use WiFi, you can use `iwctl` to connect to it  
```shell
# start iwctl
iwctl  

# find your device name, usually it's "wlan0"
device list

# if your device or adapter is off, turn it on
device *device* set-property Powered on  # replace *device* with actual device name
adapter *adapter* set-property Powered on  # replace *adapter* with actual adapter name

# start scanning for available networks
station *device* scan
station *device* get-networks

# connect to wifi
station *device* connect *SSID*  # replace *SSID* with actual wifi name
# you will be asked for wifi password

# exit iwctl after connecting
exit
```

To make sure you are connected to internet, try to ping something  
```shell
ping 8.8.8.8
```

### Clock sync
To make sure you have the correct time  
```shell
timedatectl set-ntp true
```

## Partitioning  
Make partitions of your drive  

**Warning!**  
Thing twice before you do something, because you can lose your data forever  

### Choose your drive
With the command `lsblk`, you can see all the devices on your PC/VM  
You will see more than one, but the correct one is most likely the one with the biggest size  
Usually, it's called `sda` (or `vda` on some VM's)  

### Making partitions  
Now you have to make the actual partitions for the drive you chose  
Mine is `sda`... If yours is different, replace all `sda` occurrences with the right one  

The location of my drive is `/dev/sda`

You can use `cfdisk` to make partitioning easier  
```shell
cfdisk /dev/sda  
```

First thing you will be asked for is Label type, choose `dos`  
> Note: If your drive is more that 2TB, you should choose `gpt`, but it's more complicated and this tutorial does not cover it  

Now you need to make at least these 2 partitions  

| Partition   | Minimal size      | Description                   |
| ----------- | ----------------- | ----------------------------- |
| `/dev/sda1` | 1G                | Bootable partition            |
| `/dev/sda2` | *remaining space* | Partition for everything else |
You can also make a separate partition for your `/home` directory (and use it across more systems) and/or `swap` partition, but that's not necessary  

After making partitions, `Write` them and then `Quit` the `cfdisk` program  
**Warning!**  
Writing may destroy your data, so make sure you know what you are doing  

### Formatting partitions
You can see your partitions with `lsblk` command  
Now you need to format them  

**Warning!**  
Formatting will erase ALL the data on your partitions  

If you are ready, format them with following commands  
```shell
mkfs.ext4 /dev/sda1  
mkfs.ext4 /dev/sda2
# if you have more partitions, format them as well  
```

## Mount partitions
For your `root` partition (`/`), it's as easy as this  
```shell
mount /dev/sda2 /mnt
```

For your `boot` partition (`/boot`), you also have to create folder for it and mount it there  
```shell
mkdir -p /mnt/boot
mount /dev/sda1 /mnt/boot
```

Now if you do `lsblk`, you should see `mountpoints` next to your partitions  

## Install system
I will use `pacstrap`, which is basically a tool, that will install Arch for you  
```shell
pacstrap /mnt base base-devel linux linux-firmware gnome neovim
```

This will download some stuff (up to 1GB or even more), so it might take a while  

> Note: I will be using `gnome` as desktop environment and `neovim` as editor as you can see, but you can use whatever you prefer. You also don't have to install them at all, but it makes your life easier    

## `fstab`  
Short for "File System Table"; is a configuration file, which tells your system which drives to load when booting   

```shell
genfstab -U /mnt >> /mnt/etc/fstab
```

The `-U` flag will use UUID's of drives instead of drive name  
Drive name can change in some special cases and cause problems, UUID stays the same  
If you won't redirect the output, it will just show the output and you will not have the actual configuration set  

## Login to `root`
Now you have kind of installed the system and you can kind of login to it as root with following command  

```shell
arch-chroot /mnt /bin/bash
```

This is required for following configuration

## Network Manager
Since you probably want to have internet connection when you start your machine, you have to install `networkmanager` and enable it  

```shell
pacman -S networkmanager  # install 
systemctl enable NetworkManager  # enable it on PC startup
```

> Note: When you try to install something with `pacman` for the first time, you might need to use `-Sy` flag instead of just `-S` 
## Grub
Grub will be your bootloader, which will basically be starting your PC  

```shell
pacman -S grub  # install grub
grub-install /dev/sda  
grub-mkconfig -o /boot/grub/grub.cfg
```

> Note: If your drive isn't `sda`, make sure to use the correct one   

## `root` password
You know that it's a bad idea to have `root` user without password  
To set it, just simply run the command `passwd`

## Locale
It's basically the language you want to use on your system  

You have to edit `/etc/locale.gen` file and uncomment the languages you want to use, such as `en_US.UTF-8 UTF-8`  
Just open the file in your editor that you installed before (`neovim` for me) and remove `#` at the beginning of line  

Now you need to generate it with following command  

```shell
locale-gen
```

Now type your language into `/etc/locale.conf`  
It should look something like this...

```
LANG=en_US.UTF-8
```

## Hostname
Hostname it basically the name of your PC, which will other users see on your network  
Just write your desired name in `/etc/hostname`  

## Time zone  
You already have all the time zones on your PC, now you just have to link it  
Choose whatever suits you, I will choose the one that suits me :)

```shell
ln -sf /usr/share/zoneinfo/Europe/Bratislava /etc/localtime
```

> Note: You can use `tab` key on your keyboard to autocomplete in commands, which will help you navigate in `/usr/share/zoneinfo` folder

## Gnome
This step is optional, but you will most likely want to use some desktop environment  
I like `gnome`, which I installed previously  

To actually use it, you have to use some kind of display manager  
For `gnome` it's `gdm` (Gnome Display Manager)  
Enter this command to enable it on startup  

```shell
systemctl enable gdm
```

## Reboot
Now, when everything is ready, you can reboot your PC and it should start  

```shell
exit  # exit chroot environment
reboot now
```