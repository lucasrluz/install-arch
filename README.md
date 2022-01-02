# Install arch

1. Set the console keyboard layout:
```
$ loadkeys br-abnt2
```
2. Connect to the internet
3. The connection may be verified with ping: 
```
$ ping archlinux.org
```
4. Partition the disks:
```
$ cfdisk /dev
```
5. Format the partitions:
```
$ mkfs.fat -F32 /dev/sda1

$ mkfs.ext4 /dev/sda2

$ mkfs.ext4 /dev/sda3

$ mkswap /dev/sda4
```
6. Mount the file systems:
```
$ mount /dev/sda2 /mnt

$ mkdir /mnt/home
$ mkdir /mnt/boot
$ mkdir /mnt/boot/efi

$ mount /dev/sda3 /mnt/home
$ mount /dev/sda1 /mnt/boot/efi

$ swapon /dev/sda4
```
7. Install essential packages:
```
$ pacstrap /mnt base linux linux-firmware
```
8. Fstab:
```
$ genfstab -U /mnt >> /mnt/etc/fstab
```
9. Chroot:
```
$ arch-chroot /mnt
```
10. Time zone:
```
$ ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
```

11. Edit ``` /etc/locale.gen``` and uncomment ```pt_BR.UTF-8 UTF-8```
```
$ locale-gen

$ echo "LANG=pt_BR.UTF-8" > /etc/locale.conf

$ echo "KEYMAP=br-abnt2" > /etc/vconsole.conf
```
12. Hostname: 
```
$ echo "arch" > /etc/hostname
```
13. Hosts:
```
$ echo "127.0.0.1 localhost.localdomain localhost" > /etc/hosts

$ echo "::1 localhost.localdomain localhost" >> /etc/hosts

$ echo "127.0.1.1	arch.localdomain arch" >> /etc/hosts
```
14. Grub:
```
$ pacman -S grub efibootmgr

$ grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB

$ grub-mkconfig -o /boot/grub/grub.cfg
```
15. Networkmanager:
```
$ pacman -S networkmanager

$ systemctl enable NetworkManager
```
16. Root password:
```
$ passwd
```
17. Add user:
```
$ useradd -m -g users -G wheel username

$ passwd username
```
18. Install packages:
```
$ pacman -Syu

$ pacman -S xorg xorg-xinit pulseaudio pavucontrol sudo neovim i3-wm i3blocks rofi alacritty chromium thunar thunar-volman gvfs lxappearance feh gnome-keyring
```
19. [Dotfiles](https://github.com/lucasrluz/dotfiles).
