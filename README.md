# archlinux-install
## [archlinux](https://archlinux.org)

### 校对时间
>timedatectl set-ntp true

### 验证
>date

### 分区 查看磁盘号
>fdisk -l | lsblk给                        

### 进入图形化分区(GPT)
>cfdisk /dev/磁盘号

>New #G type EFI System

>New #G type Linux swap

>New #G type Linux filesystem

>write写入 quit保存

### 格式化分区
>mkfs.ext4 /dev/Linux filesystem根目录分区

>mkswap /dev/Linux swap交换分区

>mkfs.fat -F 32 /dev/EFI System^EFI分区

### 挂载分区
>mount /dev/Linux filesystem根目录分区 /mnt

>mount --mkdir /dev/EFI System^EFI分区 /mnt/boot

>swapont /dev/Linux swap交换分区

### 改软件源
>nano /etc/pacman.d/mirrorlist

>添加:    Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch

### 重新安装密钥
>pacman -Sy

>pacman -S archlinux-keyring

### 安装基本系统
>pacstrap -K /mnt base base-devel linux | [linux-zen] | linux-lts | ... linux-firmware linux-zen-headers

### 挂载信息进入系统
>genfstab -U /mnt >> /mnt/etc/fstab

### 进入系统
>arch-chroot /mnt

### 设置时区
>ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

> hwclock --systohc

### 下载软件
>networkmanager dhcpcd openssh git nano vim

### 设置语言
>cd /etc

>nano locale.gen    去掉en.US | zh.CN的注释

>locale-gen 加载配置

### 编辑locale.conf
>nano locale.conf 输入 LANG=en_US.UTF-8

### 安装中文字体
>pacman -S adobe-source-han-sans-cn-fonts

>pacman -S ttf-dejavu wqy-zenhei wqy-microhei

### 设置root密码
>passwd

### 添加用户
>useradd -m -G wheel username

> 编辑visudo 去掉wheel的注释

### nano hostname [input you like name]

### nano hosts
>127.0.0.1      localhost

>::1            localhost

### 安装grub | efibootmgr | 双系统安装 os-prober
cd/

>nano /etc/default/grub 去掉最后一行的注释

### UEFI引导
>grub-install --target=x86_64-efi --efi-directory=boot --bootloader-id=GRUB

### 生成GRUB配置文件
>grub-mkconfig -o /boot/grub/grub.cfg

### 编辑软件库
>nano /etc/pacman.conf

去掉multilib的注释
最下面添加: 
>[archlinuxcn]

>SigLevel = Optional TrustAll

>Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch

导入密钥
>pacman -Sy archlinuxcn-keyring

### 安装paru yay
>pacman -S paru yay

### 安装KDE桌面
>pacman -S xorg sddm plasma wayland konsole kate filelight dolphin ark sudo

设置sddm开机自启动

### 安装英伟达显卡驱动
>pacman -S nvidia-dkms nvidia-utils linux-zen-headers

### 安装nvtop查看显卡使用率
>pacman -S nvtop

### 编辑grub
>nano /etc/default/grub

>在GRUB_CMDLINE_LINUX_DEFAULT中加入nvidia_drm.modeset=1

更新
>grub-mkconfig -o /boot/grub/grub.cfg

### 编辑mkinitcpio
>nano /etc/mkinitcpio.conf

>去掉HOOKS的   kms

>在MODULES中加入:   nvidia nvidia_modeset nvidia_uvm nvidia_drm

### 重构
>mkinitcpio -P linux-zen

### 安装蓝牙驱动
>pacman -S bluez bluez-utils

配置开机自启动

### 安装中文输入法
>pacman -S fcitx5-im fcitx5-chinese-addons fictx5-material-color

### 输入法配置编辑
最下面添加

GTK_IM_MODULE=fcitx

QT_IM-MODULE=fcitx

XMODIFIERS=@im=fcitx

SDL_IM_MODULE=fcitx

GLFW_IM_MODULE=ibus

保存重启

---



### 安装微信
>yay -S deepin-wine-wechat | com.qq.weixin.deepin

### 安装wps
>yay -S wps-office-cn

### 安装字体
>yay -S ttf-wps-fonts

### 中文语言包
>yay -S wps-office-mui-zh-cn

### 安装网易云音乐
>yay -S netease-cloud-music-gtk-bin | netease-cloud-music

### 安装qq音乐
>yay -S qqmusic-electron

### 壁纸插件 [安装steam]
>yay -S plasma6-wallpapers-wallpaper-engine-git

### 安装edge
>yay -S microsoft-edge-dev-bin

### 安装google-chrome
>yay -S google-chrome

### 安装b站
>yay -S bilibili-bin

### 安装qq
>yay -S linuxqq