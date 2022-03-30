---
title: "Xfce4 美化"
---

## 将 Xfce4 外观现代化

!!! quote
    Xfce4 的一个问题就是，默认的主题显得十分具有年代感，似乎这是一件古董（虽然 Xfce4 确实是最早出现的桌面环境之一）。

[Xfce4](https://xfce.org/) 也可以深度美化，但 Xfce 不适合进行大量自定义美化（这是 KDE 擅长的事情），保持简洁即可。更值得做的事情是让 xfce4 外观现代化。

如果你想要美化 Xfce，需要的做的应该是寻找一个你觉得**耐看**且美观的 GTK 主题，一套你喜欢的图标包和鼠标主题包；然后再将窗口主题也修改一下，最后再安装一些必要的面板插件。另外，openSUSE 官方仓库内有一些 gtk 主题（如 `metatheme-arc-common`, `metatheme-matcha-common`），你可以使用 `zypper se metatheme` 获取更多信息。

- Xfce 的外观设置页面可以添加本地的主题包，图标包同理。
- 鼠标主题包请先解压到 `~/.icons` 文件夹中，然后在鼠标和触摸板设置中替换刚刚下载的鼠标主题包。
- 相关：  
    - [Xfce Look - Eyecandy for your XFCE-DESKTOP](https://www.xfce-look.org/)
    - [Gnome Look - Eyecandy for your GNOME-DESKTOP](https://www.gnome-look.org/)

如果你希望其他用户也能使用你的主题和图标包，你需要将已解压的文件夹放置到以下目录：

|文件夹|用途|
|---|----|
|`/usr/share/icons`|共享的应用图标/鼠标光标主题文件夹|
|`/usr/share/themes`|共享的 GTK 主题文件夹|
|`/usr/share/wallpapaers`|共享的壁纸文件|
 
!!! note
    - 如果你希望 xfce4 的锁屏能够正确显示你指定的壁纸图片，那你需要将壁纸文件放置到无限制访问权限的 `/usr/share/wallpapaers` 中，这样相关的程序才能正确地读取壁纸文件。  
    - 要编辑锁屏界面，你需要额外安装一个 lightdm 编辑器：`lightdm-gtk-greeter-settings`

## xfce4 面板插件

默认安装好的 Xfce 可能会缺少一些相关的组件（如剪切板，CPU 频率表），你可以阅读 xfce 官方的[插件使用手册](https://docs.xfce.org/panel-plugins/start)获得更多信息（包含简易的使用指南）。

openSUSE 预装的 xfce4 桌面环境没有安装完整的 xfce4 插件。以下是一些推荐的扩展：

```
sudo zypper in xfce4-clipman-plugin #安装剪贴板插件
sudo zypper in xfce4-netload-plugin #安装网络负载监视器
```

## dock 栏

一篇介绍流行的 dock 栏应用的文章：[Top 10 Best Linux Docks That You MUST Try in 2020 -- Journaldev](https://www.journaldev.com/36769/top-best-linux-docks-2020)

```
sudo zypper in plank #一个简约，美观的 dock 栏
```

你可以使用 xfce4 官方开发的 docker 栏：打开面板首选项，在**备份和恢复**中选择其他的预制方案，如 `Xfce 16.4`（包含一个顶栏和一个用于快速启动程序的底栏）确认变更即可。