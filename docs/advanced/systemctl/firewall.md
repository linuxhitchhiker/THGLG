---
title: 防火墙
---

## 简介

!!! note
    官方文档详见[此处](https://firewalld.org/documentation/)。

Firewalld 提供了一个动态管理的防火墙，支持使用区域来标识网络连接/接口的可信等级。支持 IPv4、IPv6 防火墙设置、以太网桥接和 IP sets。使用分离的运行时配置和永久设置。也提供了一个接口用来直接为服务或应用添加防火墙规则[^1]。

## 准备工作

一般而言，openSUSE 和 Fedora 都已经预装了 firewalld。使用下列命令检查 firewalld 的状态:

```
sudo systemctl status firewalld
```

如果 firewalld 正在运行并开机启动，则会有如下的输出：

```
bh@c004-h0:~> sudo systemctl status firewalld
[sudo] root 的密码：
● firewalld.service - firewalld - dynamic firewall daemon
     Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: disabled)
     Active: active (running) since Mon 2022-04-25 17:00:52 CST; 1h 47min ago
       Docs: man:firewalld(1)
   Main PID: 963 (firewalld)
      Tasks: 2 (limit: 4915)
        CPU: 535ms
     CGroup: /system.slice/firewalld.service
             └─963 /usr/bin/python3 /usr/sbin/firewalld --nofork --nopid

4月 25 17:00:51 c004-h0 systemd[1]: Starting firewalld - dynamic firewall daemon...
4月 25 17:00:52 c004-h0 systemd[1]: Started firewalld - dynamic firewall daemon.
```

如上，`Loaded` 中指明文件位置（`/usr/lib/systemd/system/firewalld.service`）的部分后面的 `enabled` 表示 firewalld 已经支持开机启动了。下一行则表示 firewalld 服务正在运行（`active`）

你可以使用下列命令启动 firewalld 并启用开机启动：

```shell
sudo systemctl enable firewalld --now
#或者
sudo systemctl start firewalld #启动防火墙
sudo systemctl enable firewalld #将防火墙设置为开机启动
```

要停止运行 firewalld 和禁用 firewalld 开机启动，请使用如下命令：

```
sudo systemctl stop firewalld
sudo systemctl disable firewalld
```

## 基本概念

!!! note
    每次你编辑 firewalld 的配置的时候，你都需要重新加载防火墙程序以载入新设置。  
    编辑防火墙规则需要管理员权限（root 权限或者 `wheel` 用户组）。

`firewall-cmd` 是 firewalld 的主要命令行工具。它可以用来获取 firewalld 的状态信息，获取运行时和永久环境的防火墙配置，也可以用来修改这些配置。根据所选择的策略，你需要通过认证才能访问或更改 firewalld 的配置。它只有在 firewalld 运行的情况下才能使用。这个工具也被一些服务用来从使用iptables调用有一个简单的迁移路径。

检查防火墙是否正在运行：

```
sudo firewall-cmd --state
```

### 区域（zone）

firewalld 将所有的网络数据流量划分为多个区域，再根据数据包的源IP地址或传入网络接口等条件，将数据流量转入相应区域的防火墙规则中。

!!! note
    下表罗列了 firewalld 默认的区域。用户可以自行创建新的自定义区域。  
    Fedora Workstation 默认的区域是 `workstation`。  

|名称|描述|
|---|---|
|block|拒绝所有传入的网络连接。只有从系统内部发起的网络连接才可能有效。|
|dmz|隔离区域也称为非军事化区域，为您的局域网提供有限的访问权限，并且只允许选定的传入端口。|
|drop|终止所有传入链接，只允许传出的链接。|
|external|对路由器类型的连接很有用。你需要局域网和广域网的接口来进行伪装（NAT）才能正常工作。|
|home|适用于家庭电脑，如局域网内的笔记本电脑和台式机，您可以信任其他电脑。只允许选定的 TCP/IP 端口|
|internal|用于内部网络，当你几乎信任局域网内的其他服务器或计算机时。|
|public（系统默认值）|适用于始终处于公共区域的云服务器或托管在您处的服务器。您不信任网络上的任何其他计算机和服务器。您只允许使用所需的端口和服务。|
|trusted|允许任何的网络链接。|
|work|适用于您信任您的同事和其他服务器的工作场所。|

查看所有区域

```
firewall-cmd --get-zones
```

查看默认区域

```
firewall-cmd --get-default-zone
```

当 NetworkManager 添加新的网络联接接口（如 `eth0` 或 `ens3`）时，它们将被连接到默认的区域。通过运行以下命令进行验证：

!!! note
    你可以使用 `$ ip link show` 命令查看当前所联接的全部网络接口的详细信息。

```
firewall-cmd --get-active-zones
```

### 服务（services）

服务是一个包含了本地端口、协议、源端口、目的地和防火墙帮助模块 (firewall helper modules) 的列表。

查询与 public 相关的防火墙规则或服务：

```
sudo firewall-cmd --list-all --zone=public
```

示例输出如下：

```
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: wlp3s0
  sources: 
  services: dhcpv6-client samba
  ports: 
  protocols: 
  forward: yes
  masquerade: no
  forward-ports: 
  source-ports: 
  icmp-blocks: 
  rich rules:
```

在该查询结果中，默认区域是 `public`，允许的服务是 `dhcpv6-client` 和 `samba`。假设你需要删除 `dhcpv6-client`，那么你应该运行如下指令：

```
$ sudo firewall-cmd --remove-service=dhcpv6-client --zone=public
$ sudo firewall-cmd --reload ## 重载防火墙
#或者使用 sudo systemctl restart firewalld
$ sudo firewall-cmd --list-services ## 列出所有服务
```

运行下列指令查询特定区域允许的服务列表：

```
$ sudo firewall-cmd --list-services ## 查询当前区域允许的服务
$ sudo firewall-cmd --list-services --zone=* ## 将 * 替换成你所需要查询服务的区域
$ sudo firewall-cmd --list-all-zones ## 查询全部区域的服务或防火墙规则
```

### 运行时和永久规则

如果不加以声明，你对 firewalld 配置更改都是临时性的，当你重新启动系统或 firewalld 时，它们就会消失。这些被称之为运行时规则。

你可以在使用 `firewall-cmd` 调整配置时，使用 `--permanent` 选项，将更改设置为永久规则。例如：

```
$ sudo firewall-cmd --zone=public --add-service=http ## 运行时规则
$ sudo firewall-cmd --zone=public --add-service=http --permanent ## 永久规则
$ sudo firewall-cmd --reload ## 重启防火墙让规则生效。
```

检查规则是否生效：

```
$ sudo firewall-cmd --list-services
$ sudo firewall-cmd --list-services --permanent
```

查询 firewalld 支持的服务列表：

```
$ sudo firewall-cmd --get-services
```

### 一些简单规则

添加 DNS 服务（TCP/UDP 端口：53，区域为 public，永久性规则）：

```
$ sudo firewall-cmd --zone=public --add-service=dns --permanent
```

!!! note
    当 firewalld 的区域是 public 的时候，绝大多数端口是默认禁用的。

删除某个服务（例如 VNC 服务器服务，TCP 端口：5900-5903，区域为 public，永久性规则）：

```
$ sudo firewall-cmd --zone=public --remove-service=vnc-server --permanent
```

永久开放特定的端口（TCP/UDP），例如开放 TCP/UDP 端口：55527：

```
$ sudo firewall-cmd --zone=public --add-port=55527/tcp --permanent
$ sudo firewall-cmd --zone=public --add-port=55527/udp --permanent
```

查看已开放的端口：

```
$ sudo firewall-cmd --zone=public --list-ports
$ sudo firewall-cmd --zone=public --list-ports --permanent
```

拒绝/禁用特定端口：

```
$ sudo firewall-cmd --zone=public --remove-port=23/tcp
```

### 图形化前端

Firewalld 有图形化管理界面。你可以使用下列命令安装：

```
sudo dnf install firewall-config  #openSUSE 也有 firewall-config 这个软件包。
```

openSUSE YaST 工具集里面有一个图形化防火墙管理前端（打开 YaST，启动防火墙）。

[^1]: [Firewalld - ArchLinux Wiki](https://wiki.archlinux.org/title/Firewalld_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))