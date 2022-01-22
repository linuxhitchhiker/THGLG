---
title: 在虚拟机中安装 Linux
---

# 在虚拟机中安装 Linux

## 虚拟机与物理机

在不熟悉 Linux 基本知识的情况下，在物理机上安装 Linux 可能会导致数据丢失，或者是硬件损坏。所以，在付诸行动之前，你需要先在虚拟机上练习以下如何安装和使用 Linux。

- [Virtualbox](https://www.virtualbox.org/) 是一个让你再不破坏当前系统结构的情况下，能够获得最接近原生 Linux 环境体验的工具。你也可以使用 [VMware](https://www.vmware.com/products/workstation-pro.html) 安装 Fedora 。
- 注意，在物理机上安装 Fedora 并非是必须的步骤，不安装到物理机上可以省去大量的迁移工作，但安装到物理机上会让系统具备更强的性能和更多的功能。

## 配置虚拟机（VMWare Workstation）

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
- 如果不喜欢为 VMware 付费，你可以选择开源免费的 [Virtualbox](https://www.virtualbox.org/)。相关的操作内容另见：[Virtualbox - openSUSE Wiki](https://zh.opensuse.org/Virtualbox)。

然后你就会看到 Fedora 的引导启动页面，选择“**Test this media & start Fedora**”。进入下一步。

然后你就会进入到 Fedora Live 环境，你此时可以体验一下 Fedora 的图形界面，你此时所作出的更改基本不会影响到电脑原有的布局。如果你要开始安装，请找到并启动带有 Fedora 图标，名为“**Install to Hard Drive**”的应用程序。

