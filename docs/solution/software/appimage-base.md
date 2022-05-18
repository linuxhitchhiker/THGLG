---
title: "使用 Appimage"
---

## 简介

[AppImage](https://appimage.org/) 是一种在 Linux 系统中用于分发便携式软件而不需要超级用户权限来安装它们的格式。它还试图允许 Linux 的上游开发者来分发他们的程序而不用考虑不同 Linux 发行版间的区别。AppImage 的核心思想是一个文件即一个应用程序。每个 AppImage 都包含应用程序以及应用程序运行所需的所有文件。换句话说，除了操作系统本身的基础组件，Appimage 无需依赖即可运行。类似于 Windows 平台常见的便携版软件。[^1]

## 快捷工具

为了更便捷地管理 appimage 应用程序，你可以借助 [AppImageLauncher](https://github.com/TheAssassin/AppImageLauncher)。一键将 AppImages 集成到你的应用程序启动器，并从那里管理、更新和删除它们。

### 使用

1. 从 [GitHub Release](https://github.com/TheAssassin/AppImageLauncher/releases) 下载 `appimagelauncher-lite-*.AppImage` 
2. 打开终端，移动到 AppImageLauncher 的下载目录，运行 `$ ./<文件名>.AppImage install` 即可安装 AppImageLauncher。
3. 打开应用程序启动器，打开 `AppImageLauncher Settings`，点击 `appImageLauncherd`，添加你常用于存放 appimage 文件的目录。默认的目录是 `~/Applications`。
4. AppImageLauncher 会自动识别存放在指定目录的 appimage 文件，然后将它们添加到应用程序启动器中。

## 快捷使用

如果你没有使用 AppImageLauncher，你只使用 `chmod` 命令为文件添加可执行权限即可，例如：

```
$ wget http://example.com/download/appimage.appimage #下载
$ chmod +x appimage.appimage #添加可执行权限
$ ./appimage.appimage #运行
```

## 注意事项

!!! attention
    因为 appimage 文件不受任意 Linux 发行版的官方仓库维护者或安全团队的审查。**所以，用户必须自行承当安全风险，并请时刻保持小心。**

和从源码安装、使用预编译的二进制文件等方法一样，**Appimage 应当是一种获取应用程序的候选方案。**只有当你在 Linux 发行版官方软件仓库、已验证的第三方仓库（如 [packman](https://zh.opensuse.org/Packman)、[rpmfusion](https://rpmfusion.org/)）中找不到软件时，才建议使用 appimage。

并且如果在上述范围内找不到可用的软件包，也请尽量使用上游软件开发者自行打包好的 appimage、rpm、deb、flatpak 或预编译的二进制文件。

如果你要使用第三方打包 appimage 文件，请确保这是你信赖的维护者/打包者。

### 与 Flatpak 相比

Appimage 会假定用户已经安装了一些核心系统软件包（并且假定你安装的版本和依赖是正确），这意味着有些时候你下载获得的 Appimage 未必就能正常运行。而 Flatpak 使用同一的运行环境，规避了这些依赖问题。

此外，Appimage 需要额外的应用程序辅助才能集成到桌面环境之中，并且需要手动检查，下载更新包。相比于 Flatpak 而言，多出了一些额外的维护步骤。而 flatpak 的沙盒化特性有时候也会造成一些问题（比如不遵循系统的主题，与容器外的程序通讯存在问题等）

当然，要选择何种方式作为补充软件源，具体取决于你的需求，你也可以混合使用 appimage 和 flatpak。

## 外部链接

- [AppImageHub](https://appimage.github.io/)
- [AppImage 文档](https://docs.appimage.org/)
- [AppImage 论坛](https://discourse.appimage.org/)

[^1]: https://zh.wikipedia.org/wiki/AppImage