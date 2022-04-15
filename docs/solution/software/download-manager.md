---
title: "下载器"
---

## 通用下载器

`wget` 是许多 Linux 系统内置的一个下载工具，你可以使用下列命令查阅使用手册：

```
$ wget --help
```

[Aria2](https://aria2.github.io/)

```
sudo dnf in aria2
sudo zypper in aria2
```

[Motrix](https://motrix.app/) 是一个基于 aria2 开发通用下载器，支持 HTTP、FTP 和 BT 磁力链等下载内容。除了 Flatpak 安装方式，motrix 也有提供 appimage 供下载使用。

```
flatpak install flathub net.agalwood.Motrix
```

## BT 下载器

[qBittorrent](https://www.qbittorrent.org/) 是一个流行的 bt 下载做种工具。

!!! note
    - 如果你对于反吸血，屏蔽迅雷有需求，可以试试 [qBittorrent-enhanced-edition](https://github.com/c0re100/qBittorrent-Enhanced-Edition/releases)。  
    - 适用于 openSUSE 的 qBittorrent-enhanced-edition 的 OBS 仓库详见[此处](https://build.opensuse.org/package/show/home:opensuse_zh/qBittorrent-Enhanced-Edition)。

```
sudo dnf in qbittorrent
sudo zypper in qbittorrent
```

[Transmission](https://transmissionbt.com/) 是一个历史悠久的 bt 下载工具

```
sudo dnf in transmission
sudo zypper in transmission
```

### Tracker

有关如何使用 tracker 加速 BT 下载的指南详见[此处](https://trackerslist.com/)。

## 其他