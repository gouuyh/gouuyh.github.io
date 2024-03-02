---
title: "用于日常使用的Arch Linux的安装"
slug: "Arch-Linux-installation-for-daily-use"
tags:
  - IT
  - OS
date: "2021-08-29"
update: "2021-08-29"
draft: false
---

# 前言
如标题所言，这篇文章主要介绍以Arch Wiki为基础的Arch Linux的安装与配置，以使之适合日常使用，又在一定程度上兼顾安全与操作效率。另一方面，我也希望通过创作这篇文章来作为自己未来可能的安装新系统的备忘录。（注：这篇文章不会详细介绍各安装细节，大量可以在[ArchWiki](https://wiki.archlinux.org/title/Installation_guide)上找到的基本步骤将被省略）

# 基本系统的安装
## 磁盘分区
为了能够最大化地利用磁盘容量，我决定使用LVM（Logical Volume Manager, 逻辑卷管理）来管理磁盘。LVM的具体使用方法，详见ArchWiki的[这篇文章](https://wiki.archlinux.org/title/LVM)。

我利用`cfdisk`将磁盘分出512MB大小的分区用于挂载`/boot`分区。参考[这篇文章](https://wiki.archlinux.org/title/Install_Arch_Linux_on_LVM)可以将整个系统全部安装在LV上，并从LV正常启动。如果直接将`/boot`目录放在LV上，就会出现GRUB安装不成功的情况。

### 创建PV
在刚才分区之后未利用的磁盘分区上创建PV。例如：
```bash
pvcreate /dev/nvme0n1p2
```

### 创建VG
我使用"arch"这个名字来命名将要创建的VG。一般情况下，只需创建一个VG即可。
```bash
vgcreate arch /dev/nvme0n1p2
```
可使用`vgs`命令查看系统所有的VG名称。

如果有更多的磁盘，可以在它们上创建PV然后添加到VG中。例如：
```bash
pvcreate /dev/sdb1
vgextend arch /dev/sdb1		# 添加新的PV到已存在的VG中
```

### 创建LV
**方法一**
```bash
lvcreate -L 100G -n lv_home arch	# "-n"后为任意LV名(name)；"-L"后为大小(large)，其中"L"和"G"需大写
```
**方法二**
```bash
lvcreate --extents 100%FREE arch -n lv_home		# "100%FREE"会用尽VG的剩余空间
```
可使用`lvs`命令查看LV及每个LV所属的VG。

### LV扩容
**方法一**
```bash
lvresize -L +50G arch/lv_home	# [没有]"/dev"；在原来的基础上增加了50G
```
**方法二**
```bash
lvresize -L 150G arch/lv_home	# 增加到150G
```
如果是格式化后的LV扩容，需要使用以下命令使文件系统扩容（EXT家族）：
```bash
resize2fs /dev/arch/lv_home
```
- LV的路径似乎可以用另一种方式表示：`/dev/mapper/'VG'-'LG'`。感兴趣的同学可以使用虚拟机尝试。

### 格式化
```bash
mkfs.ext4 /dev/arch/lv_home
```
swap分区使用`mkswap`命令。


## 安装与配置
完成了分区与格式化，并且将不同磁盘分区挂载到相应的挂载点上，就要修改`/etc/pacman.conf`，将`#Color`的注释去掉，再修改镜像源文件。

### 下载与安装
接着，安装系统和必要组件：
```bash
pacstrap /mnt base linux-lts linux-firmware base-devel lvm2 dhcp iwtcl git vim man zsh
```
对于与ArchWiki的不同的解释：
- `linux-lts`: 长期稳定版本，与`linux`相比bug更少。
- `base-devel`: 包含了基本工具的软件包。
- `lvm2`: LVM配置工具。
- `dhcp iwctl`: 网络。
- `git vim man zsh`: 略。

### 配置
若按照ArchWiki的步骤，到达[Initramfs](https://wiki.archlinux.org/title/Installation_guide#Initramfs)步骤时，就要稍微注意一下。这个系统主要安装在LVM上，因此要参照[Adding mkinitcpio hooks](https://wiki.archlinux.org/title/Install_Arch_Linux_on_LVM#Adding_mkinitcpio_hooks)小节修改`/etc/mkinitcpio.conf`并运行`mkinitcpio -P`。
（注：若`/usr`在一个单独的分区，请注意被修改的`HOOKS`行上方的"NOTE"。）

若将ArchWiki上的被本文忽略的步骤也都做完并成功的话，重启即可进入简陋的tty界面。至此，基本安装已全部完成。登录后参阅[General recommendations](https://wiki.archlinux.org/title/General_recommendations)来进行进一步的配置。


# 图形环境
## 安装
如果不太确定要安装的具体组件，可以直接安装整个包组：
```bash
sudo pacman -S xorg
```
接下来要安装显示管理器（`GDM`, `lightDM`等）或`xinit`以及桌面环境（DE）或窗口管理器（WM）。
# 结语
至此，一个非常基本的Arch Linux就安装完成了。
