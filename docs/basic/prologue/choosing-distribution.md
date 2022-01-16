---
title: "选择发行版"
---

## 什么是发行版

根据 [Wikpedia](https://zh.wikipedia.org/wiki/Linux%E5%8F%91%E8%A1%8C%E7%89%88)：

>Linux 发行版（英语：Linux distribution，也被叫做 GNU/Linux 发行版），为一般用户预先集成好的 Linux 操作系统及各种应用软件。一般用户不需要重新编译，在直接安装之后，只需要小幅度更改设置就可以使用，通常以软件包管理系统来进行应用软件的管理。Linux 发行版通常包含了包括桌面环境、办公包、媒体播放器、数据库等应用软件。现在有超过 300 个 Linux 发行版（详见 Linux 发行版列表）。大部分都正处于活跃的开发中，不断地改进。
>
>由于大多数软件包是自由软件和开源软件，所以 Linux 发行版的形式多种多样——从功能齐全的桌面系统以及服务器系统到小型系统（通常在嵌入式设备，或者启动软盘）。除了一些定制软件（如安装和配置工具），发行版通常只是将特定的应用软件安装在一堆函数库和内核上，以满足特定用户的需求。 

## 主流发行版

Linux 当前的主流/根发行版有：[Debian](https://www.debian.org/)、[Ubuntu](https://ubuntu.com/)、[RHEL](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux)/[Fedora](https://getfedora.org/)、[SLES](https://www.suse.com/products/server/)/[openSUSE](https://www.opensuse.org/)、[Arch](https://archlinux.org/)、[Gentoo](https://www.gentoo.org/)、[Slackware](http://www.slackware.com/) 和 [Linux From Scratch](https://www.linuxfromscratch.org/)。

这些发行版可以分为商业发行版，比如 Ubuntu、Red Hat Enterprise Linux 和 SUSE Linux Enterpise；和社区发行版，它们由自由和开源软件社区提供支持，如 Debian、Fedora、Arch、openSUSE 和 Gentoo。

### 各自优缺点

请依照你的实际需求，选择合适的发行版。没有糟糕的发行版，只有糟糕的需求与供给搭配。

|名称|优点|缺点|适用人群|
|---|---|---|---|
|Debian|使用人数最多，可用软件包数量最多，稳定可靠，有着丰富的文档。|官方仓库软件包版本老旧，时常会给软件加补丁。|Linux 初学者、专家和服务器运营者|
|Ubuntu|使用人数很多，是众多 Linux 桌面发行版的上游。|官方有窃取用户隐私的黑历史。|Linux 初学者、桌面用户、专家和服务器运营者|
|RHEL|具有最为广泛的商业支持的商业发行版，稳定可靠安全。|服务收费，软件包版本略为老旧|Linux 初学者、专家和服务器运营者|
|Fedora|RHEL 的上游，是 Linux 新兴技术的公测平台，贴近上游而不会过分激进。|不适合求稳定的用户，技术变更频繁。|Linux 初学者、桌面用户、专家和服务器运营者|
|SLES|另一个知名的，系统管理员友好的 Linux 发行版，稳定可靠|服务收费，软件包版本略为老旧|Linux 初学者、专家、系统管理员和服务器运营者|
|openSUSE|SLES 的上游，也是 SUSE 的新技术测评平台，贴近上游，对新技术采用不及 Fedora 激进，稳定可靠。|所受支持程度不及 Fedora|Linux 初学者、桌面用户、专家、系统管理员和服务器运营者|
|Arch|一个激进，以“保持简单，且一目了然”为哲学的激进发行版。具有高度可定制性。社区很活跃，用户也很多。Arch 用户拥有地球上最强大的 Wiki 文档库。|软件包版本是上游的最新版本；不适合新手、无经验者和不愿意折腾系统的人|具有中等及以上 Linux 技能水平，有时间有精力的用户|
|Gentoo|一个从源码逐步构建起来的 Linux，可定制系统的方方面面。|不适合新手、无经验者和不愿意折腾系统的人|具有中等及以上 Linux 技能水平，有时间有精力的用户|

- 像 Slackware 和 Linux From Scratch 这类维护难度高于 Gentoo 的 Linux 发行版就不作介绍了，有兴趣的读者可自行查阅相关资料。
- 除此之外还有其他很多优秀知名的 Linux 发行版，但由于本文只描述主流和根发行版（其他发行版的上游发行版），所以不做介绍。

### 一些误解

- Fedora 是红帽的小白鼠</p>
        众多 Linux 的新兴技术都是首先在 Fedora 上实验，然后推广到下游发行版或其他发行版。Fedora 本身是一个非常贴近上游技术方向的发行版，为 Linux 社区的发展做出了很多广受认可的贡献。将 Fedora 比作红帽的实验小白鼠是很片面的说法。