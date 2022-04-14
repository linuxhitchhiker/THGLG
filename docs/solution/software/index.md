---
title: "概述"
---

本节主要描述如何获取和使用一些常用软件的内容。

## 预先准备

为了安装一些软件，你需要启用一些常用的第三方仓库。

### Fedora

添加 RPMfusion：

```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

安装多媒体解码器：

```
sudo dnf install gstreamer1-plugins-{bad-\*,good-\*,base} gstreamer1-plugin-openh264 gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel

sudo dnf install lame\* --exclude=lame-devel

sudo dnf group upgrade --with-optional Multimedia
```

### openSUSE

添加 Packman 源：

```
sudo zypper ar -cfp 90 https://mirrors.ustc.edu.cn/packman/suse/openSUSE_Tumbleweed/ packman
```
!!! note
    如果你不使用 vlc 作为多媒体播放器，你可以删除第三条命令末尾的 `vlc-codecs`。

更新并安装多媒体解码器：

```
sudo zypper refresh

sudo zypper dist-upgrade --from packman --allow-vendor-change

sudo zypper install --from packman ffmpeg gstreamer-plugins-{good,bad,ugly,libav} libavcodec-full vlc-codecs
```

### Flatpak

如果你对 Flatpak 感兴趣，并愿意使用它作为获取软件的一种途径，请参考[此文](./flatpak-get-start.md)对 Flatpak 进行初始化配置。