---
title: "更新系统"
---

# 更新系统

更新系统是完成安装并登录新系统后应该做的第一件事。

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
[bh@fedora ~]$ sudo dnf config-manager --set-disabled fedora-cisco-openh264
[bh@fedora ~]$ sudo dnf config-manager --set-disabled phracek-PyCharm
[bh@fedora ~]$ sudo dnf config-manager --set-disabled rpmfusion-nonfree-nvidia-driver
[bh@fedora ~]$ sudo dnf config-manager --set-disabled rpmfusion-nonfree-steam
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

 - rpmfusion 提供了大量 Fedora 或 RHEL 官方仓库不能提供的软件包（版权受限或许可证受限），如多媒体解码器、NVIDIA 显卡驱动和其他不符合 Fedora 官方仓库要求规范的软件包。

```
$ sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

然后更新系统

```
$ sudo dnf check-update  #检查可用的更新
$ sudo dnf up -y         #自动确认更新
$ reboot                 #更新完成后，记得重启系统
```

Fedora 不需要特意去使用镜像站，如果你遇到下载缓慢的情况，请先检查网络连接是否通畅或者清空缓存文件让 dnf 重新生成缓存。

```
$ sudo dnf clean all; sudo dnf check-update  #删除全部缓存文件并重新检查可用的更新。
```

## openSUSE

打开 Konsole，运行下列命令：

```
$ sudo systemctl disable packagekit.service --now #屏蔽 Packagekit 服务
```

然后禁用全部的软件源：

```
$ sudo zypper mr -da
```

然后添加镜像源：

```
$ sudo zypper ar -fcg 'https://opentuna.cn/opensuse/tumbleweed/repo/oss/' 'OPEN-TUNA:TW:OSS'
$ sudo zypper ar -fcg 'https://opentuna.cn/opensuse/tumbleweed/repo/non-oss/' 'OPEN-TUNA:TW:NON-OSS'
```

刷新软件源：

```
$ sudo zypper ref
```

更新系统：

```
$ sudo zypper dup -y
```