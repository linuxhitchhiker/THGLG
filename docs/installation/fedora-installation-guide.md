---
title: "Fedora 安装指南"
description: "Doks is a Hugo theme for building secure, fast, and SEO-ready documentation websites, which you can easily update and customize."
lead: "Doks is a Hugo theme for building secure, fast, and SEO-ready documentation websites, which you can easily update and customize."
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "installation"
weight: 200
toc: true
---

# 概述

## 什么是 Fedora Linux

Fedora Linux（第七版以前为 Fedora Core）是著名的 Linux 主流发行版之一，由 [Fedora 项目](https://getfedora.org/)社群开发、[红帽公司](https://www.redhat.com/zh)赞助，目标是创建一套新颖、多功能并且自由（开放源代码）的操作系统。

Fedora 是一个贴近上游，软件包版本新旧程度仅次于 [Arch Linux](https://archlinux.org/)，Linux 新兴技术的开放测试平台。

详细的用户使用文档可[在此](https://docs.fedoraproject.org/)处找到。

## 本文的目的

本文主要描述如何在 Windows 10 上使用虚拟机（平台为 [VMWare](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)）安装 Fedora Linux 以及物理机双系统所需要注意的事项。

- 参考：[Fedora 35 - Installation Guide](https://docs.fedoraproject.org/en-US/fedora/f35/install-guide/)

# 获取 ISO

你可以在 [Get Fedora](https://getfedora.org/en/) 上直接下载**最新的** Fedora Workstation ISO 文件；或者查找一个距离你地理位置最近的开源镜像站，下载**最新的** Fedora ISO。

- 如果你不喜欢 Workstation 的桌面环境（Gnome Desktop），你可以选择 [Fedora Spin](https://spins.fedoraproject.org/)。

## Fedora ISO 的主要类型

- **Live 镜像**</p>
  Live 镜像允许你在不对电脑进行更改的情况下，快速预览一下 Fedora 图形化界面，然后决定要不要安装。Live 镜像包含安装一个基本的 Fedora 所需的全部文件。

- **netinstall 镜像**</p>
  netinstall 镜像直接引导到安装环境，并使用在线 Fedora 软件包存储库作为安装源。你可以使用 netinstall 镜像安装任何 Fedora 版本或选择各种软件包来创建自定义的 Fedora 安装。

- **DVD 镜像**</p>
  DVD 镜像直接引导到安装环境，并允许你从随它提供的各种软件包中进行选择。在 Fedora 21 中，DVD 选项仅在 Fedora 服务器版中可用。

# 制作安装介质

如果你只在虚拟机中安装 Fedora，那你可以跳过该步骤，阅读下一节“安装”。

如果你需要将 Fedora 安装至硬盘中，你需要使用 [Rufus](https://rufus.ie/zh/) 或 [Fedora Media Writer](https://getfedora.org/en/workstation/download/) 之类的 ISO 刻录工具将下载好的 ISO 文件刻录到移动储存介质中。

## Fedora Media Writer

将你的 U 盘插入电脑，打开 Fedora Media Writer 选择“**自定义镜像**”，选择你刚刚下载好的 ISO 文件，请确认选择正确的设备，然后点击 “**写入磁盘**”，等刻录自动完成。

## Rufus

将你的 U 盘插入电脑，打开 Rufus，它会自动选择可用的移动存储设备。点击“**选择**”打开要刻录的镜像文件。请确认选择正确的设备，然后点击底端的“**开始**”等待刻录自动完成。

## 划分未分配的磁盘空间

如果你是在实体机上安装 Fedora，请提前用磁盘分区工具划分一个大小为 20GB 或更大的未分配的磁盘空间（不要格式化和写入文件系统）。

# 安装

## 准备安装

在安装好 VMWare Workstation 后，点击左上方“**文件(F)**” ，选择“**新建虚拟机(N)**”。

在弹出的新建虚拟机向导中，点击“**下一步(N)**”，然后选择“**安装程序光盘映像文件(iso)**”，打开你下载好的 Fedora ISO 文件。点击“**下一步(N)**”。

在“命名虚拟机”中指定你的虚拟机的名称和位置。点击“**下一步(N)**”，指定“**最大磁盘大小(GB)**”，你可以使用默认值，或者指定更大的容量。完成后点击“**下一步(N)**”。

在“已准备好创建虚拟机”页面中，检查虚拟机[硬件配置](https://docs.fedoraproject.org/en-US/fedora/rawhide/release-notes/welcome/Hardware_Overview/)是否合乎要求：

- 最小安装的系统硬件需求：
  - 2GHz 双核处理器或更快的处理器
  - 2GB 系统内存
  - 15GB 未分配的硬盘空间
- 推荐的系统配置：
  - 2GHz 四核处理器
  - 4GB 系统内存
  - 20GB 未分配的硬盘空间

你可以在“**自定义硬件(C)**”中自行调整配置。完成后点击“**完成**”启动虚拟机。

- `Ctrl + Alt` 快捷键组合可以让 VMware 停止捕获你的鼠标。
- 对于需要将 Fedora Linux 安装至实体机上的用户，请将刻录好的安装介质插入到电脑中，重启电脑，手动进入引导界面，选择安装介质作为引导启动的对象。

然后你就会看到 Fedora 的引导启动页面，选择“**Test this media & start Fedora**”。进入下一步。

然后你就会进入到 Fedora Live 环境，你此时可以体验一下 Fedora 的图形界面，你此时所作出的更改基本不会影响到电脑原有的布局。如果你要开始安装，请找到并启动带有 Fedora 图标，名为“**Install to Hard Drive**”的应用程序。

## 使用 Anaconda 安装系统

Fedora 使用 Anaconda 作为系统安装器。启动 Anaconda 后，第一步是选择语言，找到“**中文**”，并选择“**简体中文**”，然后进入下一步。

- 注意，选择语言后，你无法更改语言，除非你停止并重新启动安装程序，才能再次选择语言。

在“安装信息摘要”页面中，请注意“**时间和日期**”的正确性，如中国大陆用户应将时区设置为“**亚洲/上海时区**”。如果你发现时区不正确，请点击该按钮，在世界地图上选择你所在的位置，Anaconda 会自动匹配你所在位置的时区，然后点击左上方的“**完成(D)**”关闭页面。

你可以在“**安装目的地**”中，对 Fedora 安装位置进行设置。

### 手动分区

- 使用虚拟机安装 Fedora 的用户可在“**本地标准磁盘**”中勾选空闲的磁盘空间，然后选择“**自动**”进行自动分区。最后点击两次“**完成(D)**”确认更改即可。
 
在“**安装目的地**”中，点击你之前预留的未分配的磁盘空间或虚拟机磁盘。然后在“**存储配置**”中选择“**高级自定义 (Blivet-GUI)**”，点击“**完成(D)**”进入配置页面。

使用鼠标右键单击右侧逻辑视图下方的 free space，选择“**新建**”，若磁盘没有分区表或者你打算删除原有系统进行一次全新的安装，Anaconda 会提示你选择新分区表类型（推荐设置为 GPT）。

为了安装 Fedora，你至少需要 `/` 和 `/boot` 两个基本的分区。
|分区|描述|
|---|---|
|`/boot`|这个分区包含操作系统内核和在引导过程中使用的其他文件。推荐大小为 1GB。文件系统类型可设置为 `ext4`|
|`/boot/efi`|独立的 [EFI](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface) 分区，推荐当 Fedora 需要与 Windows 共存时创建该分区，大小为 512MB，格式为 `vfat` 或 `fat32`。|
|`/(root)`|这是根目录所在的位置。根目录是目录结构的顶层。默认情况下，所有文件都写入此分区，除非在写入的路径中安装了不同的分区（例如，`/boot` 或 `/home`）。</p>Fedora 现在已经使用 [Btrfs](https://wiki.archlinux.org/title/Btrfs) 卷作为根目录的默认文件系统。官方推荐大小为 25GB 及以上。实际上你只需要保证根目录大于 15GB 即可。|
|`/home`|独立的用户目录，具体大小取决于你想要放入多少文件；不是必需的分区。分区格式为 `xfs`、`ext4` 或 `btrfs` 等你所偏好的分区格式。|
|`biosboot`|如果你的电脑使用了 [MBR](https://wiki.archlinux.org/title/Partitioning#Master_Boot_Record_(bootstrap_code)) 而不是 [UEFI](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface) 作为启动模式，则你需要额外创建一个大小为 1MB，格式为 `biosboot` 的空白分区。|
|`swap`|[交换分区](https://wiki.archlinux.org/title/Swap)，Linux 将物理内存分为内存段，叫做页面。交换是指内存页面被复制到预先设定好的硬盘空间(叫做交换空间)的过程，目的是释放这份内存页面。物理内存和交换空间的总大小是可用的虚拟内存的总量。分区格式为 `swap`。|

SWAP 分区推荐大小如下所示：

|系统物理内存（RAM）大小|推荐的 swap 分区大小|推荐的 swap 分区大小（如果需要休眠）|
|---|---|---|
|小于 2GB|RAM 的两倍|RAM 的三倍|
|2GB - 8GB|和 RAM 相同|RAM 的两倍|
|8GB - 64GB|RAM 的 0.5 倍|RAM 的 1.5 倍|
|大于 64GB|基于实际工作负载而定|不推荐休眠|

然后点击 free space（注意，你只能在 free space 中创建新分区），点击上方的“**+**”，添加一个新的分区：

- 对于 MBR 用户：
  - **/boot**：设备类型设置为**分区**，大小设置为 1GB，文件系统设置为 `ext4`，挂载点设置为 `/boot`。
  - **biosboot**：设备类型设置为**分区**，大小设置为 1~2MB，文件系统设置为 `BIOS Boot`。
  - **swap**：设备类型设置为**分区**，大小请参考上表而定，文件系统设置为 `swap`。
  - **/(root)**：设备类型设置为 **Btrfs 卷**，大小设置为剩余空闲空间大小。
  - **/home**：*请根据实际需要创建该分区*。设备类型设置为**分区**，大小和文件系统类型依照实际需要而定，挂载点为 `/home`。</p>
- 对于 UEFI 用户：
  - **/boot**：设备类型设置为**分区**，大小设置为 1GB，文件系统设置为 `ext4`，挂载点设置为 `/boot`。
  - **/boot/efi**：设备类型设置为**分区**，大小设置为 512MB，文件系统设置为 `vfat` 或 `fat32`，挂载点为 `/boot/efi`。
  - **swap**：设备类型设置为**分区**，大小请参考上表而定，文件系统设置为 `swap`。
  - **/(root)**：设备类型设置为 **Btrfs 卷**，大小设置为剩余空闲空间大小。
  - **/home**：*请根据实际需要创建该分区*。设备类型设置为**分区**，大小和文件系统类型依照实际需要而定，挂载点为 `/home`。

如果你创建了错误的分区，可以点击“+”右侧的 “X” 删除错误的分区，或者右下方的**撤销上一次操作**进行回退。完成创建分区后，点击两次右上角**完成**确认分区结果即可。

- Tips:</p>
  - 创建分区的时候，先创建小分区（如：`/boot`），再创建大分区（如：`/home`）。
  - 独立的 `/boot/efi` 可避免 Windows 更新 EFI 分区时导致损坏 Linux 的引导文件的可能情况（Windows Boot Manager 不是为多系统引导而设计的）。
  - 不创建 `swap` 分区也可安装 Fedora。
  - 独立的 `/home` 不是必须的，你也可以编辑现有的磁盘分区或创建一个新的大分区（用于储存大量个人文件），设置挂载点挂载到 `/` 或 `/home` 下（如果挂载的分区存储有重要文件，请勿格式化该分区）。

---

在完成分区后，点击**网络和主机名**，即可为你的 Fedora 设置一个主机名。安装系统后，你可以使用 `hostnamectl` 进行[修改主机名](https://docs.fedoraproject.org/en-US/quick-docs/changing-hostname/)。

点击**创建用户**，然后在子页面设置好你的用户全名、用户名、用户密码，然后点击**完成**。

- 请牢记你的用户密码，丢失密码可能会导致你无法进入系统。
- root 用户不是必须创建的。

最后，点击右下方的**开始安装(B)**开始安装 Fedora。

完成后，弹出安装介质或拔出 U 盘即可。

祝你玩的愉快！