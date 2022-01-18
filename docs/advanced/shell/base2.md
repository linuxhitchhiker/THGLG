---
title: "Linux 文件系统"
---

# Linux 文件系统

## 了解 Linux 文件系统

Linux 系统中所有东西（数据、命令、符号连结、设备和文件夹）都是以文件夹或文件的形式储存在文件系统中，而整个文件系统就像一棵树一样。所有的主要文件夹都存储在根目录（`/`）的下方，所有的文件都分散在各个文件夹中。

与 Windows 不同的一点，Linux 的不同层级的文件夹之间都是使用斜杠 `/` 进行区分，而不是 NTFS 文件系统常用的反斜杠，比如 `C:\Program Files (x86)\Microsoft`。这也是为什么当今所有的网页地址都是使用斜杠而非反斜杠的原因之一。且 Linux 中所有的绝对路径都是以 `/` 开头。

![file system](./assets/file-system.png)

如果你要确认某个文件或文件夹的位置，比如 `Applications` 文件夹中用户自己创建的 `Mount.sh`。你可以从 `/` 开始，将它的位置表示为 `/home/bh/Applications/Mount.sh`，这种表示形式称之为**绝对路径**，除此之外的表达都是**相对路径**。例如，从 `/home` 开始，该文件可以表示成 `~/Applications/Mount.sh`，如果你现在就在 `~` 文件夹中，你可以将它表示为 `Applications/Mount.sh`。

对于 `/` 目录之下的文件的常见用途，如下所示：

|名称|用途|
|---|---|
|/bin|包含普通的 Linux 用户命令，如 `ls`、`date` 等|
|/boot|具有可引导的 Linux 内核、初始 RAM 磁盘和引导加载程序配置文件 (GRUB)。|
|/dev|包含代表系统上设备访问点的文件。这些包括终端设备（tty*）、硬盘（hd* 或 sd*）、RAM（ram*）和 CD-ROM（cd*）。用户可以通过这些设备文件直接访问这些设备； 但是，应用程序通常会向最终用户隐藏实际的设备名称|
|/etc|包含管理配置文件。 这些文件中的大多数都是纯文本文件，只要用户有适当的权限，就可以使用任何文本编辑器对其进行编辑。|
|/home|包含分配给每个具有登录帐户的普通用户的目录。（root 用户是一个例外，使用 /root 作为他的主目录。|
|/media|为自动安装设备（尤其是可移动媒体）提供标准位置。 如果介质具有卷名，则该名称通常用作安装点。例如，卷名为 myusb 的 USB 驱动器将挂载到 `/media/myusb`。|
|/lib|包含 `/bin` 和 `/sbin` 中的应用程序启动系统所需的共享库|
|/mnt|在被标准 `/media` 目录取代之前，它是许多设备的通用挂载点。一些可引导的 Linux 系统仍然使用这个目录来挂载硬盘分区和远程文件系统。许多人仍然使用这个目录来临时挂载本地或远程文件系统，这些文件系统不是永久挂载的。|
|/misc|有时用于根据请求自动挂载文件系统的目录。|
|/opt|可用于存储附加应用软件的目录结构。|
|/proc|包含有关系统资源的信息。|
|/root|root 用户的主目录|
|/sbin|包含管理命令和守护进程。|
|/sys|包含调整块存储和管理 cgroup 等参数。|
|/temp|包含应用程序使用的临时文件。|
|/usr|包含用户文档、游戏、图形文件 (X11)、库 (lib) 以及引导过程中不需要的各种其他命令和文件。/usr 目录用于存放安装后不会更改的文件（理论上，/usr 可以只读方式挂载）</p>有关社区对于文件目录的调整（[Usr Merge](https://wiki.debian.org/UsrMerge)），详见[此处](https://www.suse.org.cn/%E6%8A%80%E6%9C%AF%E6%96%87%E7%AB%A0/2021/04/28/%E9%87%87%E5%8F%96-UsrMerge-%E6%8E%AA%E6%96%BD%E7%9A%84%E7%90%86%E7%94%B1.html)。|
|/var|包含各种应用程序使用的数据目录。特别地，你可以在此处放置作为 FTP 服务器 (`/var/ftp`) 或 Web 服务器 (`/var/www`) 共享的文件。它还包含所有系统日志文件 (`/var/log`) 和 `/var/spool` 中的假脱机文件（例如 mail、cups 和 news）。`/var` 目录包含经常更改的目录和文件。在服务器上，通常使用可以轻松扩展的文件系统类型将 `/var` 目录创建为单独的文件系统。|

在 Linux 中，文件并不需要像 windows 那样的后缀名（.txt、.xls）。后缀名也没有实际意义，后缀名并不影响文件的功能，但它有助于帮助用户理解此文件的用途。此外，Linux 文件系统有着严格且明确的权限和所有权管理系统，这将在后文详述。

## 使用基本的文件系统命令

要在命令行中与文件系统进行交互，你至少需要知道以下命令。

|命令|功能|
|---|---|
|cd|变更到另一个文件夹|
|pwd|将你当前所在的文件夹打印到屏幕上|
|mkdir|创建一个文件夹|
|chmod|更改一个文件夹或文件的权限|
|ls|列出指定目录的文件夹和文件|

一般地，当你打开一个终端后，你所在的文件夹是你的用户文件夹（`~`）。你可以使用 `cd` 命令移动到指定的目录（路径可以是绝对路径或相对路径），如：

```
[bh@c004-v1 ~]$ ls #列出当前目录的文件
公共  模板  视频  图片  文档  下载  音乐  桌面  Applications  FolderA
[bh@c004-v1 ~]$ cd Applications #移动到 Applications 子文件
[bh@c004-v1 Applications]$ ls #列出当前目录的文件
CFW  Icalingua-2.4.5.AppImage  mount.sh
[bh@c004-v1 Applications]$ pwd #打印当前目录至输出
/home/bh/Applications
[bh@c004-v1 Applications]$ cd /usr/share/backgrounds #移动到 /usr/share/backgrounds
[bh@c004-v1 backgrounds]$ ls #列出当前目录的文件
default.png  default.xml  f35  images  wallhaven-967zyk.jpg  xfce
[bh@c004-v1 backgrounds]$ pwd #打印当前目录至输出
/usr/share/backgrounds
[bh@c004-v1 backgrounds]$ cd ~ #回到用户主目录
[bh@c004-v1 ~]$ pwd #打印当前目录至输出
/home/bh
```

直接输入 `cd` 也可以立即回到用户主目录；你可以使用 `..` 表示上一级文件夹（相对路径），`.` 表示当前文件夹，如：

```
[bh@c004-v1 Applications]$ ls -lat
总用量 111440
drwx------. 1 bh bh       440  1月 18 16:22 ..
-rwxrw-rw-. 1 bh bh       117  1月 12 11:35 mount.sh
drwxr-xr-x. 1 bh bh        70  1月  8 14:54 .
drwxr-xr-x. 1 bh bh       620  1月  8 13:47 CFW
-rwxrwxrwx. 1 bh bh 114110270 12月 23 15:01 Icalingua-2.4.5.AppImage
[bh@c004-v1 Applications]$ cd ..
[bh@c004-v1 ~]$ pwd
/home/bh

[bh@c004-v1 Applications]$ cd ./CFW
[bh@c004-v1 CFW]$ pwd
/home/bh/Applications/CFW
```

`mkdir` 用于创建文件夹，要在用户目录内新建一个名为 test 文件夹，只需要：

```
$ mkdir test #或者 mkdir ~/test
```

## 使用元字符和运算符

