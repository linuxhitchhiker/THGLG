---
title: "使用 systemctl 管理服务"
comments: true
---

## 简介

`systemd` 是一个 Linux 系统基础组件的集合，提供了一个系统和服务管理器，运行为 `PID 1` 并负责启动其它程序。其功能包括：支持并行化任务、按需启动守护进程、监视进程、支持快照和系统恢复、维护挂载点和自动挂载点等。

## 基本工具

监视和控制 systemd 的主要命令是 `systemctl`。该命令可用于查看系统状态和管理系统及服务。详见 `man systemctl`。

显示系统状态：

```
$ systemctl status
```

输出激活（`enable`）的单元：

```shell
$ systemctl
#或者
$ systemctl list-units
```

输出运行失败的单元：

```
$ systemctl --failed
```

所有可用的单元文件存放在 /usr/lib/systemd/system/ 和 /etc/systemd/system/ 目录（后者优先级更高）。查看所有已安装服务：

```
$ systemctl list-unit-files
```

### 单元

一个单元（`unit`）配置文件可以描述如下内容之一：系统服务（`.service`）、挂载点（`.mount`）、sockets（`.sockets`） 、系统设备（`.device`）、交换分区（`.swap`）、文件路径（`.path`）、启动目标（`.target`）、由 systemd 管理的计时器（`.timer`）。详情参阅 [systemd.unit(5)](https://man.archlinux.org/man/systemd.unit.5)。

使用 systemctl 控制单元时，通常需要使用单元文件的全名，包括扩展名（例如 `sshd.service`）。但是有些单元可以在 systemctl 中使用简写方式。

- 如果无扩展名，systemctl 默认把扩展名当作 `.service`。例如 `netcfg` 和 `netcfg.service` 是等价的。
- 挂载点会自动转化为相应的 `.mount` 单元。例如 `/home` 等价于 `home.mount`。
- 设备会自动转化为相应的 `.device` 单元，所以 `/dev/sda2` 等价于 `dev-sda2.device`。

!!! note
    systemctl命令在 `enable`、`disable` 和 `mask` 子命令中增加了 `--now` 选项，可以实现激活的同时启动服务，取消激活的同时停止服务。  
    下面的大部分命令都可以跟多个单元名, 详细信息参见 [systemctl(1)](https://man.archlinux.org/man/systemctl.1)。

立即激活单元：

```
# systemctl start <单元>
```

立即停止单元：

```
# systemctl stop <单元>
```

重启单元：

```
# systemctl restart <单元>
```

重新加载配置：

```
# systemctl reload <单元>
```

输出单元运行状态：

```
$ systemctl status <单元>
```

检查单元是否配置为自动启动：

```
$ systemctl is-enabled <单元>
```

开机自动激活单元：

```
# systemctl enable <单元>
```

设置单元为自动启动并立即启动这个单元:

```
# systemctl enable --now unit
```

取消开机自动激活单元：

```
# systemctl disable <单元>
```

禁用一个单元（禁用后，间接启动也是不可能的）：

```
# systemctl mask <单元>
```

取消禁用一个单元：

```
# systemctl unmask <单元>
```

显示单元的手册页（必须由单元文件提供）：

```
# systemctl help <单元>
```

重新载入 systemd 系统配置，扫描单元文件的变动。注意这里不会重新加载变更的单元文件。参考上面的 reload 示例。

```
# systemctl daemon-reload
```

## 参考

- [systemd (简体中文) -- ArchLinux Wiki](https://wiki.archlinux.org/title/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))