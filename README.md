# sluarchlinuxdoc.github.io
Arch Linux Installation Documentation

Software: VMWare Workstation Pro

Download the Arch Linux ISO 
Boot the Arch Linux ISO 
    Make sure you boot the Arch Linux ISO in UEFI mode
Based on preference set the keyboard layout and font using the commands loadkeys and setfont. I'm using US format which is the default but for the font I'm using the command "setfont ter-132b" to increase the font size.

Test the internet connection using the command "ip link" and then ping a site for example "ping archlinux.org" and to end the command use ctrl c to stop the pings
Partition the disks 
    lsblk to show the current partitions we will be using this command repeatedly to check the following changes effects
    use command "cfdisk" then go to gpt
    press enter on the free space for a new partition set the first one to 100M thats /dev/sda1
    then do the same thing again to the free space but the next partition have it be 4G thats /dev/sda2
    rinse and repeat for the last time and have that one be whatever free space is left thats /dev/sda3
    make sure to write this to the disk by using the arrow keys to Write and then type yes
    use lsblk to see the changes in affect
Format the partitions
    using the commands "mkfs.ext4 /dev/sda3", "mkfs.fat -F 32 /dev/sda1", and mkswap /dev/sda2
Mount the Drives 
    "mount /dev/sda3 /mnt"
    "mkdir -p /mnt/boot/efi" and then "mount /dev/sda1 /mnt/boot/efi"
    "swapon /dev/sda2"
    lsblk to show the changes in effect 
Installing Base systems and other essential packages 
    "pacstrap /mnt base linux linux-firmware sof-firmware base-devel grub efibootmgr nano amd-ucode"
Generate filesystem tab 
    "genfstab /mnt" 
    "genfstab /mnt > /mnt/etc/fstab"
Change our root and enter the installed systems
    "arch-chroot /mnt"
Timezone: "ln -sf /usr/share/zoneinfo/America/Chicago /etc/localtime" and then "hwclock --systohc"
Localization
    "nano etc/locale.gen" and then find #en_US.UTF-8 UTF-8 and remove the # and then save and exit the file and then use the command "locale-gen" 
    "nano /etc/locale.conf" and then write LANG=en_US.UTF-8 and then save and exit
Hostname
    "nano /etc/hostname" and then give it whatever name you want 
Set Root Password
    "passwd" and set a good password
Exit chroot using the command "exit"
install grub using "grub-install /dev/sda"
Reboot using the command "reboot"
Login to the the newly created system using the default username root and the password being whatever password you set

