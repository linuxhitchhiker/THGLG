---
title: "多媒体相关"
---

## 图片编辑

[GIMP](https://www.gimp.org/) 是一个功能和 Photoshop 相似的开源图片编辑软件，基于 GTK 开发。

```
sudo dnf in gimp     #在 Fedora 上安装
sudo zypper in gimp  #在 openSUSE 上安装
```

[Krita](https://krita.org/) 是基于 Qt 开放，著名的开源绘画软件，它也支持简单的图片编辑功能。

```
sudo dnf in krita     #在 Fedora 上安装
sudo zypper in krita  #在 openSUSE 上安装
```

## 视频编辑

[Blender](https://www.blender.org/) 是一个集动画电影制作、视觉特效、3D 打印、三维/二维建模、动态图形、交互式 3D 应用和 VR 等多项领域为一体的知名开源软件。

```
sudo dnf in blender
sudo zypper in blender
```

[Shotcut](https://www.shotcut.org/) 是由 [MIT 多媒体框架](https://en.wikipedia.org/wiki/Media_Lovin%27_Toolkit)开发者开发的一款基于 MIT 多媒体框架的非线性视频编辑软件。

```
sudo dnf in shotcut 
sudo zypper in shotcut
```

[Kdenlive](https://kdenlive.org/) 是一个基于 Qt 和 MIT 多媒体框架开发的非线性视频编辑软件。

```
sudo dnf in kdenlive
sudo zypper in kdenlive
```

### 屏幕录制

[OBS](https://obsproject.com/) 是一款用于视频录制和直播推流的开源软件。

```
sudo dnf in obs-studio  
sudo zypper in obs-studio 
```

## 音频编辑

[Audacity](https://www.audacityteam.org/) 是一个用于音频录制与音频编辑的开源软件。

```
sudo dnf in audacity  
sudo zypper in audacity 
```

### 字幕编辑

[Aegisub](https://github.com/Aegisub/Aegisub) 是一个跨平台的高级字幕编辑工具。

```
sudo dnf in aegisub 
sudo zypper in aegisub  
```

## 视频播放器

[MPV](https://mpv.io/) 是一个备受 Linux 用户欢迎，高度可定制的多媒体播放器。它同时是很多播放器的后端。

```
sudo dnf in mpv
sudo zypper in mpv
```

[VLC](https://www.videolan.org/vlc/) 是另一个广为流行，跨平台，兼容几乎绝大部分多媒体格式（不仅仅是视频）的开源多媒体播放器。

```
sudo dnf in vlc
sudo zypper in vlc
```

[SMplayer](https://www.smplayer.info/en/downloads) 是一个基于 mpv 的视频播放器，它简单化了 mpv 的复杂配置，并提供一个良好的开箱即用体验。

```
sudo dnf in smplayer smplayer-themes  #安装播放器本体及播放器的扩展皮肤包
sudo zypper in smplayer smplayer-themes
```

## 音频播放器

[Deadbeef](https://deadbeef.sourceforge.io/) 是一个在 HiFi 社区中流行，可自定义的开源音频播放器。

```
sudo dnf in deadbeef
sudo zypper in deadbeef
```

[Audacious](https://audacious-media-player.org/) 是一个开源的音频播放器。

```
sudo dnf in audacious
sudo zypper in audacious
```

### 流媒体播放器

开源的 Apple Music 播放器：

```
flatpak install flathub sh.cider.Cider
```

网易云音乐：

```
flatpak install flathub com.netease.CloudMusic
```

网易云音乐 GTK 版：

```
flatpak install flathub com.github.gmg137.netease-cloud-music-gtk
```

QQ 音乐：

```
flatpak install flathub com.qq.QQmusic
```

Sportily：

```
flatpak install flathub com.spotify.Client
```

Google Play Music：

```
flatpak install flathub com.googleplaymusicdesktopplayer.GPMDP
```