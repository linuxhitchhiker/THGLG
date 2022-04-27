---
title: 虚拟机
---

!!! note
    本文中罗列的虚拟机的 Linux 版和 Windows 版的使用方法区别不大。

## KVM

!!! note
    KVM 不支持 Windows 系统。

KVM，Kernel-based Virtual Machine，是一种内置于 Linux 内核中的管理程序。它的目的类似于 Xen，但运行起来要简单得多。与原生 QEMU 使用仿真不同，KVM 是 QEMU 的一种特殊运行模式，它通过内核模块使用 CPU 扩展（HVM）进行虚拟化。

!!! note
    openSUSE 有一份十分详细的[虚拟化文档](https://doc.opensuse.org/documentation/leap/virtualization/html/book-virtualization/index.html)，涵盖在 openSUSE 上使用 KVM/Xen 的方方面面。

首先，检查你当前的设备是否支持虚拟化：

```
sudo LC_ALL=C lscpu | grep Virtualization
```

对于 Intel 处理器来输出结果说是 VT-x ，对于 AMD 处理器来说是 AMD-V ；否则你的机器不支持虚拟化。

对于 openSUSE 用户，你只需要打开 YaST ，点击**虚拟化**，再点击**安装 Hypervisor 和工具**。勾选 **KVM 工具**和 **KVM 服务器**。之后你只需要等待 YaST 自动安装并校验所有包；如果你已经安装了 KVM 相关组件，那相应的选项会变成不可点击的灰色。

对于 Fedora 用户，Fedora 软件包仓库里提供了「虚拟化」软件包组，里面就包含了我们所需的全部软件包，你可以直接安装：

```
sudo dnf install @virtualization
```

最后，你还需要加入 libvirtd 用户组，并启用 libvirtd：

```
sudo usermod -aG libvirt $USER
sudo systemctl enable libvirtd --now
```

完成上述步骤后，重启系统即可。

有关 KVM 的使用指南，除了 openSUSE 官方文档，你还可以阅读来自 openSUSE wiki 的[词条](https://zh.opensuse.org/KVM)。

## VirtualBox

### 安装

VirtualBox 是另一个流行的虚拟机软件。你可以运行下列命令直接安装：

```
sudo zypper in virtualbox
sudo dnf in virtualbox
```

然后加入用户组：

```
sudo usermod -aG vboxusers $USER
```

注销再登陆即可。

### 安装扩展包

扩展包主要提供了 USB 驱动和 3D 加速驱动等版权内容。

1. 下载 [VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads)。
2. 打开 VirtualBox ，点击 **管理** ，再点击 **全局设定** ，再点击 **扩展** ，再点击右侧的 **添加新包** 的小图标，安装你刚刚下载保持的扩展包文件。
3. 首次打开 VirtualBox 会提示用户是否启用 USB 功能（这可能会带来安全风险，但是它带来的便利值得这么做），个人建议可以使用该功能。

有关 virtualbox 的使用，可以参考 [VirtualBox#通用步骤 -- openSUSE Wiki](https://zh.opensuse.org/Virtualbox#.E9.80.9A.E7.94.A8.E6.AD.A5.E9.AA.A4)

## VMware Plyaer&Workstation