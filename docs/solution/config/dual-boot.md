# 双系统启动

双系统启动（在同一台机器上安装多个操作系统）适合于对于 Windows 仍然有依赖需求（比如 Adobe 全家桶）的用户。

## EFI

不论是 openSUSE、Fedora 还是 Windows 10。它们的默认安装器的默认配置方案都会优先将系统的 EFI 挂载到硬盘中已经存在的 EFI 系统分区（ESP）。所以，建议先安装 Windows 10，再安装 Linux，这样 grub 引导加载器就能直接扫描到 Windows 10 系统，并将其添加到启动界面中。

除非硬盘上已经存在的 ESP 分区大于或等于 512MB，否则建议在安装 Linux 的时候，手动创建一个供当前系统使用的 EFI 分区。以出现防止 Windows 更新损坏 Linux 的引导文件或者 ESP 分区空间不足等故障。

### 分区相对大小

这方面的内容依赖于实际工作环境和个人需求，因人而异。

可参考 [双引导启动 -- openSUSE wiki](https://zh.opensuse.org/SDB:DVD_%E5%AE%89%E8%A3%85%E6%96%B9%E5%BC%8F#.E5.8F.8C.E5.BC.95.E5.AF.BC.E5.90.AF.E5.8A.A8)

## 重新生成 grub

!!! note
    openSUSE YaST 中有一个名为**引导加载器**的组件可以编辑配置 grub（YaST/引导加载器/引导加载程序选项/默认引导选项）。

在设置多系统引导前，请确保你已经安装了 `os-prober`：

```
sudo dnf in os-prober
sudo zypper in os-prober
```

然后确认 `/etc/default/grub` 文件存在下列行：

```
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=false #该项的默认值是 False，有些系统的配置文件可能不会有该行。
```

如果你是先安装 Linux 再安装 Windows，则需要重新生成 grub 配置。Windows 10 会自动把自己设置为优先引导启动的系统。使用下述命令重新生成 grub 配置文件：

```
# grub2-mkconfig -o /boot/grub2/grub.cfg
```

然后将 grub2 安装到你的硬盘的主分区（仅对使用 MBR 分区的用户）：

```
# grub2-install /dev/sda
```

### 重新设置优先启动条目

`grub2-mkconfig` 只会刷新配置文件，不会设置优先启动的系统。

列出所有可用的菜单条目：

```
sudo grep -P "^menuentry" /boot/grub2/grub.cfg | cut -d "'" -f2
```

然后选择其中一个选项，并将其作为参数设置为默认的菜单条目：

```
sudo grub2-set-default <menuentry>
```

然后使用下述命令查看默认的菜单条目：

```
sudo grub2-editenv list
```

然后再重新生成一遍 grub 配置即可。

例如：

```
bh@c004-h0:~> sudo grep -P "^menuentry" /boot/grub2/grub.cfg | cut -d "'" -f2
openSUSE Tumbleweed
Windows Boot Manager (on /dev/nvme0n1p4)
UEFI Firmware Settings
bh@c004-h0:~> sudo grub2-set-default "openSUSE Tumbleweed"
bh@c004-h0:~> sudo grub2-editenv list
env_block=512+1
saved_entry=openSUSE Tumbleweed
bh@c004-h0:~> sudo grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
Found theme: /boot/grub2/themes/openSUSE/theme.txt
Found linux image: /boot/vmlinuz-5.17.2-1-default
Found initrd image: /boot/initrd-5.17.2-1-default
Found linux image: /boot/vmlinuz-5.17.1-1-default
Found initrd image: /boot/initrd-5.17.1-1-default
Warning: os-prober will be executed to detect other bootable partitions.
Its output will be used to detect bootable binaries on them and create new boot entries.
Found Windows Boot Manager on /dev/nvme0n1p4@/EFI/Microsoft/Boot/bootmgfw.efi
Adding boot menu entry for UEFI Firmware Settings ...
done
```