---
title: 安装前准备
comments: true
---

# 安装前准备

本文主要描述安装 Linux 前应当做的一些预备工作。

## 硬件需求

本文档建议您确认电脑的硬件满足以下要求，以获得较为完整和流畅的使用体验：

- 核心数不少于 2 个，主频为 2GHz 以上的 x86_64 CPU；
- 4GB 物理内存（RAM）；
- 至少 32GB 大小的硬盘；
- 现代的声卡、显卡和外设；
- 分辨率至少为 800x600 的显示器。

即便电脑无法满足以上要求，也可能可以运行 Linux 桌面系统。不过这种情况下，可能会时不时遇到卡顿，或是屏幕太小而无法显示完整的内容。因此，还是建议确保电脑硬件规格满足以上要求。

<!-- TODO 教用户检查硬件规格 -->

## 选择桌面环境

Linux 可用的桌面环境（Desktop Environment）非常多，流行的桌面环境主要有 KDE，Gnome 和 Xfce，您可以先选择一个最喜欢的。有关这三个桌面的介绍详见[此处](./../prologue/desktop-environment.md)。

如果觉得难以抉择，也可以使用自带桌面环境的 LiveDVD，体验一下几种桌面环境。

## 选择发行版类型

按软件技术来划分，发行版主要分为滚动发行版和固定更新发行版。

与 Windows 不同的是，Linux 上的第三方软件一般由发行版打包提供，通常情况下并不是用户自己从网络上寻找、下载的。

发行版直接决定用户电脑上软件的版本，滚动发行版会不断升级这些软件的版本，这样您电脑上的软件始终是比较新的；固定更新发行版会选择一个固定的版本，之后在发行版的维护周期中，软件的版本不会升级，但是发行版会修复这个版本中的漏洞，这样您电脑上的软件会比较稳定。

!!! info
    固定更新发行版的维护周期是指某个版本从发布到停止维护的这段时间。  
    在某个版本维护周期结束后，这个版本对应软件漏洞的修复也会停止，您就不能再继续用这个版本了，否则太老的软件可能无法满足您的需求，同时漏洞修复的停止也可能让您暴露在网络攻击之中。  
    这种情况下，要想继续使用电脑，您需要升级到更新的版本。

<!-- TODO 介绍一下Fedora和openSUSE等等的细微区别 -->

从体验上来说，滚动发行版能体验到更新的软件，而固定更新发行版上的软件更稳定。您可以结合对软件版本的需求和对漏洞的容忍程度，选择最适合的类型。

!!! info
    openSUSE Leap 和 Fedora 是固定版本发行版；openSUSE Tumbleweed 是滚动发行版。

## 下载可启动镜像

为了简化流程，我们直接提供了指向镜像站的 DVD 离线镜像。

!!! attention
    用于离线安装的 ISO 镜像体积较为庞大，推荐采用 [aria2](https://aria2.github.io/)、[FDM](https://www.freedownloadmanager.org/zh/) 或 [Motrix](https://motrix.app/) 之类的下载管理器下载，以免遇到某些浏览器下载较慢或者在下载失败后只能从头开始的问题。  
    如果您不熟悉下载管理器，也可以直接使用浏览器下载，只需要点击蓝色的下载链接即可。

本指南快速入门安装教程涵盖的发行版的镜像下载链接如下：

=== "openSUSE Leap 15.5"

    * 安装镜像：[openSUSE Leap (x86_64, DVD)](https://mirrors.tuna.tsinghua.edu.cn/opensuse/distribution/leap/15.5/iso/openSUSE-Leap-15.5-DVD-x86_64-Current.iso) [约 4.1GB]

=== "openSUSE Tumbleweed"

    * 安装镜像：[openSUSE Tumbleweed (x86_64, DVD)](https://mirrors.tuna.tsinghua.edu.cn/opensuse/tumbleweed/iso/openSUSE-Tumbleweed-DVD-x86_64-Current.iso) [约 4.7GB]

=== "Fedora"

    * 安装镜像：[Fedora 37 (x86_64, Workstation)](https://mirrors.tuna.tsinghua.edu.cn/fedora/releases/37/Workstation/x86_64/iso/Fedora-Workstation-Live-x86_64-37-1.7.iso) [约 2GB]

!!! attention
    许多 Linux 发行版会有多种不同的镜像。这些镜像会针对不同的 CPU 或者带有不同的软件，同时也有一种专门用于试用的 Live 镜像。  
    本教程只涵盖 x86_64 的计算机，本节介绍的是离线安装，因此提供的是 x86_64 DVD 镜像。

## 创建可启动盘

!!! info
    尽管您下载的镜像名字是“DVD”镜像，但并不是一定要烧录在 DVD 上才可以使用。事实上，现在人们装系统的时候都把镜像写到 U 盘上，然后从 U 盘上启动了。

首先，你需要一个储存空间大小在 8GB 或以上的 U 盘，这个 U 盘将会被做成可启动盘。

!!! attention
    制作可启动盘前，请先备份 U 盘上的所有数据，因为这些数据在 U 盘被做成可启动盘后都会永久丢失。  
    您可以将可启动盘恢复成普通数据盘，但丢失的数据是不会回来的。

<!-- TODO 写一个备份指南，因为U盘和电脑硬盘上的数据都要备份    -->
    
之后，可以使用 [Rufus](https://rufus.ie/zh/)、[balenaEtcher](https://www.balena.io/etcher/) 或 [Fedora Media Writer](https://getfedora.org/en/workstation/download/) 等工具将 ISO 文件刻录到 U 盘中，制成一个可引导启动的 Linux 系统安装介质。

- Rufus  
  将你的 U 盘插入电脑，打开 Rufus，它会自动选择可用的移动存储设备。点击“**选择**”打开要刻录的镜像文件。请确认选择正确的设备，然后点击底端的“**开始**”等待刻录自动完成。
- balenaEtcher  
  将你的 U 盘插入电脑，打开 balenaEtcher，点击最左侧的加号下面的“Flash from file”，选择要写入的ISO镜像。点击中间的磁盘图标下面的“Select target”，选择要写入的设备。点击最右边的“Flash!”按钮，开始写入。等待刻录自动完成。
- Fedora Media Writer  
  插入 U 盘，运行 Fedora Media Writer 选择“自定义镜像”，并选择刚刚下载的 ISO 镜像。请确保选择正确的设备，然后点击 “写入磁盘”，等待刻录完成后即可。

如果想同时将 U 盘用作启动盘和存放数据的盘，或者想用一个 U 盘容纳多个镜像，也可以在 U 盘上安装 [Ventoy](https://www.ventoy.net/cn/index.html) 。之后，把镜像（.iso 格式）复制到 Ventoy U 盘中即可。

如果你现在暂时不希望用 Linux 替换电脑上当前的操作系统，你可以阅读[使用虚拟机安装 Linux](./virtual-machine.md)获得更多信息。

## 引导启动

!!! attention
    在安装前，请确保电脑上的所有重要文件都已备份完成，因为 Linux 需要对您电脑上的硬盘进行一个彻底的重新分区，这会卸载电脑上的 Windows，删除硬盘上的所有资料（包括音频、文档、音乐、软件数据）。如果没有备份，删除后的资料就无法恢复。

确保所有备份都已经完成，然后关闭电脑。再次启动时，进入引导菜单，并选择从刚刚制作的可启动 U 盘上启动。

由于不同电脑进入引导菜单的方式不同，您需要自行搜索您的电脑上如何进入引导菜单。如果实在搜索不到，也可以在开机时反复按“F12”“DEL”“F2”“ESC”键，进行尝试。

在成功进入 U 盘中的安装程序后，请继续阅读具体发行版的安装步骤。

<!-- TODO 写一个安全启动指南 -->
