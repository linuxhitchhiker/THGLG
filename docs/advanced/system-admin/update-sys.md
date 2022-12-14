---
title: "更新系统"
comments: true
---

# 更新系统

**更新系统是完成安装并登录新系统后必须做的第一件事。**

建议每周更新一次 openSUSE Tumbleweed 和 Fedora。过高（每日一次）或过低（每月一次）的更新频率是不推荐的。

## Fedora

登录系统后，直接请直接打开终端：

### 调整软件源

运行下列指令：

```
[bh@fedora ~]$ sudo dnf repolist
仓库 id                         仓库名称
fedora                          Fedora 35 - x86_64
fedora-cisco-openh264           Fedora 35 openh264 (From Cisco) - x86_64
fedora-modular                  Fedora Modular 35 - x86_64
google-chrome                   google-chrome
phracek-PyCharm                 Copr repo for PyCharm owned by phracek
rpmfusion-nonfree-nvidia-driver RPM Fusion for Fedora 35 - Nonfree - NVIDIA Driver
rpmfusion-nonfree-steam         RPM Fusion for Fedora 35 - Nonfree - Steam
updates                         Fedora 35 - x86_64 - Updates
updates-modular                 Fedora Modular 35 - x86_64 - Updates
```

然后你就会看到两列文字，左边是仓库/软件源的名字，右边是仓库的描述。使用以下命令禁用多余的仓库：

```
sudo dnf config-manager --set-disabled fedora-cisco-openh264
```
```
sudo dnf config-manager --set-disabled phracek-PyCharm
```
```
sudo dnf config-manager --set-disabled rpmfusion-nonfree-nvidia-driver
```
```
sudo dnf config-manager --set-disabled rpmfusion-nonfree-steam
```

如果你不需要使用 Chrome 浏览器，也可以将 `google-chrome` 源禁用。然后再次运行 `$ sudo dnf repolist`，如下：

```
[bh@fedora ~]$ sudo dnf repolist
仓库 id                      仓库名称
fedora                       Fedora 35 - x86_64
fedora-modular               Fedora Modular 35 - x86_64
updates                      Fedora 35 - x86_64 - Updates
updates-modular              Fedora Modular 35 - x86_64 - Updates
```

**请确保至少启用以上四个基础仓库**（请不要禁用 update 类别的软件源）。然后添加完整版的 rpmfusion：

!!! note
    rpmfusion 提供了大量 Fedora 或 RHEL 官方仓库不能提供的软件包（版权受限或许可证受限），如多媒体解码器、NVIDIA 显卡驱动和其他不符合 Fedora 官方仓库要求规范的软件包。

```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

然后更新系统

```
$ sudo dnf check-update  #检查可用的更新
$ sudo dnf up -y         #自动确认更新
$ reboot                 #更新完成后，记得重启系统
```

Fedora 不需要特意去使用镜像站，如果你遇到下载缓慢的情况，请先检查网络连接是否通畅或者清空缓存文件让 dnf 重新生成缓存。

```
sudo dnf clean all; sudo dnf check-update  #删除全部缓存文件并重新检查可用的更新。
```

## openSUSE

打开 Konsole，运行下列命令：

```
sudo systemctl disable packagekit.service --now #屏蔽 Packagekit 服务
```

然后禁用全部的软件源：

!!! note
    - 关于为什么要禁用官方源：  
    因为 openSUSE 在更新系统的时候，会先访问 openSUSE 的主软件源来下载缓存数据。而 openSUSE 的主源位于欧洲。因此中国大陆的用户能不能正常访问 openSUSE 主源是很大的问题。后面添加 NVIDIA 软件源的时候，我们会要求中国大陆用户使用代理加速下载驱动。如果不变更软件源，则更系统时 zypper 会根据你的代理 IP 给你指定一些更慢的软件源。而 fedora 没有这种问题，因为 fedora 会将一份镜像站列表放在用户的系统中，让用户自行选择下载服务器。
    - 关于为什么不使用 update 源：  
    Tumbleweed 的更新频率很高，而且 update 源是用于推送紧急安全补丁，平时没有什么内容。整体来说用处不大而且国内的镜像站均不支持 update 源，新安全补丁很快就会在新的快照中发布。  

```
sudo zypper mr -da
```

然后添加镜像源：

```
sudo zypper ar -fcg 'https://opentuna.cn/opensuse/tumbleweed/repo/oss/' 'OPEN-TUNA:TW:OSS'
```
```
sudo zypper ar -fcg 'https://opentuna.cn/opensuse/tumbleweed/repo/non-oss/' 'OPEN-TUNA:TW:NON-OSS'
```

刷新软件源：

```
sudo zypper ref
```

更新系统：

```
sudo zypper dup -y
```

## 多媒体解码器

为了正常使用多媒体应用程序，你需要安装完整的多媒体解码器。

### Fedora

!!! note
    安装多媒体解码器前，请确保已经启用了 RPMFusion

安装多媒体解码器：

```
sudo dnf install gstreamer1-plugins-{bad-\*,good-\*,base} gstreamer1-plugin-openh264 gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel
```
```
sudo dnf install lame\* --exclude=lame-devel
```
```
sudo dnf group upgrade --with-optional Multimedia
```

### openSUSE

添加 Packman 源：

```
sudo zypper ar -cfp 90 https://mirrors.ustc.edu.cn/packman/suse/openSUSE_Tumbleweed/ packman
```
!!! note
    如果你不使用 [vlc](https://www.videolan.org/vlc/) 作为多媒体播放器，你可以删除第三条命令末尾的 `vlc-codecs`。

更新并安装多媒体解码器：

```
sudo zypper refresh
```
```
sudo zypper dist-upgrade --from packman --allow-vendor-change
```
```
sudo zypper install --from packman ffmpeg gstreamer-plugins-{good,bad,ugly,libav} libavcodec-full vlc-codecs
```