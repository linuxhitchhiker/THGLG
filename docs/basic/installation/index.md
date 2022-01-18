---
title: 下载与写入镜像
---

## 下载镜像

不少 Linux 发行版的网页服务器搭建在国外，从大陆地区访问可能会遇到网络问题。我们建议读者使用国内的镜像源下载，推荐使用 [OpenTUNA](https://opentuna.cn/)（清华大学源的姊妹站）或者 [USTC](https://mirrors.ustc.edu.cn/)（中国科学技术大学）镜像软件源。以 OpenTUNA 源为例，下载的方法如下：

1. 打开 [OpenTUNA](https://opentuna.cn/) 页面。点击页面右侧的”获取下载链接“。

2. 选择你要下载的镜像文件。

3. 点击对应链接直接下载或者右键另存为。也可以右键复制链接用迅雷之类的下载器下载。

!!! attention "注意"
    部分 Linux 发行版会有多种不同的镜像。这些镜像会针对不同的 CPU 或者带有不同的软件，同时也有一种专门用于试用的 Live 镜像。请按照自己的需求下载；如果你不知道自己需要哪个，请参阅本文档对应发行版的说明。

## 创建可启动镜像

你可以使用 [Rufus](https://rufus.ie/zh/) 或 [balenaEtcher](https://www.balena.io/etcher/) 制作安装镜像。

- Rufus  
  将你的 U 盘插入电脑，打开 Rufus，它会自动选择可用的移动存储设备。点击“**选择**”打开要刻录的镜像文件。请确认选择正确的设备，然后点击底端的“**开始**”等待刻录自动完成。
- balenaEtcher  
  将你的 U 盘插入电脑，打开 balenaEtcher，点击最左侧的加号下面的“Flash from file”，选择要写入的ISO镜像。点击中间的磁盘图标下面的“Select target”，选择要写入的设备。点击最右边的“Flash!”按钮，开始写入。等待刻录自动完成。
