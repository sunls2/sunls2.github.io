---
layout: mypost
title: Arch Linux 真·简明安装教程
categories: [Linux]
---

*制作启动盘和从U盘启动（略）*

```bash
# 更换控制台字体
setfont /usr/share/kbd/consolefonts/LatGrkCyr-12x22.psfu.gz
```

```bash
# 连接无线网络
iwctl
device list					# 设备列表
station wlan0 scan			# 扫描网络
station wlan0 get-networks	# 列出网络
station wlan0 connect xxx	# 连接网络
exit
```

```bash
# 更换镜像源，也可通过编辑 /etc/pacman.d/mirrorlist 手动更改
reflector -c CN --sort rate -n 8 --save /etc/pacman.d/mirrorlist
systemctl stop reflector.service
```

```bash
# 更新系统时间
timedatectl set-ntp true
timedatectl status
```

*硬盘分区（略）*

```bash
# 格式化分区
mkfs.vfat /dev/<efi>	# 格式化efi分区
mkfa.ext4 /dev/<ext4>	# 格式化数据分区

mkswap -f /dev/<swap>	# 格式化swap分区
swapon /dev/<swap>		# 打开swap分区
```

```bash
# 挂载分区
mount /dev/<ext4> /mnt
mkdir /mnt/efi
mount /dev/<efi> /mnt/efi
```

```bash
# 安装系统
# base base-devel linux linux-firmware	基础系统
# intel-ucode grub efibootmgr os-prober 微码和引导程序
# gnome gnome-tweaks	vim ibus-rime		Gnome桌面和优化工具，vim编辑器和输入法
# zsh zsh-autosuggestions zsh-syntax-highlighting zsh-theme-powerlevel10k	zsh相关
# ntfs-3g adobe-source-han-sans-cn-fonts wqy-zenhei	识别NTFS格式的硬盘和思源黑体，文泉驿选装
pacstrap /mnt base base-devel linux linux-firmware \
	intel-ucode grub efibootmgr os-prober \
	gnome gnome-tweaks vim ibus-rime \
	zsh zsh-completions zsh-autosuggestions zsh-syntax-highlighting zsh-theme-powerlevel10k \
	ntfs-3g adobe-source-han-sans-cn-fonts wqy-zenhei
```

[zsh和rime自用配置文件](https://github.com/sunls24/config)

```bash
# 将镜像地址copy到新系统
cp /etc/pacman.d/mirrorlist /mnt/etc/pacman.d/mirrorlist
```

```bash
# 生成fstab文件
genfstab -U /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab
```
------

```bash
# 切换到新系统
arch-chroot /mnt
```

```bash
# 设置主机名
vim /etc/hostname
arch

vim /etc/hosts
127.0.0.1	localhost
::1			localhost
127.0.1.1	arch.localdomain	arch
```

```bash
# 时区
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```

```bash
# 同步硬件时间
hwclock --systohc
```

```bash
# 设置系统语言，取消注释下面两行
vim /etc/locale.gen
en_US.UTF-8
zh_CN.UTF-8

locale-gen
vim /etc/locale.conf
LANG=en_US.UTF-8
```

```bash
# 设置root用户密码
passwd root
```

```bash
# 安装引导程序
grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=Arch

# 修改grub配置，可选操作
# GRUB_DEFAULT=saved 启动记住上次的选择
# 取消 GRUB_SAVEDEFAULT=true 的注释
# GRUB_CMDLINE_LINUX_DEFAULT="loglevel=3 quiet nowatchdog" 提高开机速度
vim /etc/default/grub

# 生成配置文件
grub-mkconfig -o /boot/grub/grub.cfg
```

```bash
# 添加非root用户，sunls替换为你的用户名
# wheel附加组可sudo进行提权，-m同时创建用户家目录
useradd -m -G wheel -s /bin/bash sunls
# 设置新用户的密码
passwd sunls
```

```bash
# 编辑sudo文件
# 取消注释 #%wheel ALL=(ALL) ALL 这一行
EDITOR=vim visudo
```

```bash
# 开机自启gdm和网络管理器
systemctl enable gdm NetworkManager
```

```bash
# 重启
exit
umount -R  /mnt
reboot
```

```bash
good works. enjoy it!
```

------

```bash
# 开启32位支持库
# 取消[multilib]两行的注释
vim /etc/pacman.conf
# 开启ArchLinuxCN支持库
[archlinuxcn]
SigLevel = Never
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch	# 中科大源
```

```bash
# 更新系统
sudo pacman -Syyu
```

```bash
# 安装aur助手yay
sudo pacman -S archlinuxcn-keyring
sudo pacman -S yay
```

------

可选部分：

```bash
# 启动蓝牙
sudo systemctl enable --now bluetooth
```

```bash
# 安装materia主题和papirus图标
sudo pacman -S materia-gtk-theme papirus-icon-theme
```

```bash
# 翻墙软件
sudo pacman -S v2ray qv2ray
```

