---
title: "网络浏览器"
---

绝大多数桌面发行版都会将 Firefox 作为默认的网络浏览器。本节也会阐述如何安装其他的浏览器。

## Firefox 分支版本

你可以在 Firefox 的官方[下载页面](https://www.mozilla.org/en-US/firefox/all/#product-desktop-release)中找到任意版本，任意语言和地区的安装包或压缩包文件。

在将文件下载至本地后（例如将文件下载至 `~/Download`），你可以根据[官方指南](https://support.mozilla.org/en-US/kb/install-firefox-linux)执行以下操作：

1. 移动到下载文件夹，并将压缩包解压：  
    ```
    cd ~/Downloads && tar xjf firefox-*.tar.bz2
    ```
2. 然后将解压好的文件夹移动到 `/opt` 目录下：  
    ```
    mv firefox /opt
    ```
3. 创建一个符号链接：  
    ```
    ln -s /opt/firefox/firefox /usr/local/bin/firefox
    ```
4. 下载一个 Desktop 文件用于在图形界面中创建程序启动按钮：  
    ```
    wget https://raw.githubusercontent.com/mozilla/sumo-kb/main/install-firefox-linux/firefox.desktop -P /usr/local/share/applications
    ```

## Chrome

!!! note
    如果你需要使用 Chrome 的非稳定版版，你需要将 `google-chrome-stable` 替换为 `google-chrome-unstable` （金丝雀版）或者 `google-chrome-beta`（beta 版）

在 openSUSE 上安装谷歌 chrome：

1. 添加仓库：  
    ```
    sudo zypper ar http://dl.google.com/linux/chrome/rpm/stable/x86_64 google-chrome
    ```
2. 获取公钥：  
    ```
    wget https://dl.google.com/linux/linux_signing_key.pub
    ```
3. 导入公钥：  
    ```
    sudo rpm --import linux_signing_key.pub
    ```
4. 安装 Google chrome 稳定版。
    ```
    sudo zypper ref && sudo zypper in google-chrome-stable
    ```

在 Fedora 上安装谷歌 chrome：

1. 添加第三方仓库：
    ```
    sudo dnf install fedora-workstation-repositories
    ```
2. 激活 Google Chrome 仓库：
    ```
    sudo dnf config-manager --set-enabled google-chrome
    ```
3. 安装 chrome 稳定版：
    ```
    sudo dnf install google-chrome-stable
    ```

### Chromium

!!! note
    - 由于版权限制，openSUSE 和 Fedora 不能分发存在版权争议的内容。如果你需要浏览器支持一些闭源格式（如 H.264、AAC 或其他 DRM 保护内容），你需要手动安装闭源组件。
    - RPMfusion 已经提供一个包含完整组件的 `chromium-freeworld`。
!!! warning
    - 谷歌已经禁止 chromium 和基于 chromium 的第三方浏览器读取谷歌的数据，所以 chromium 不能同步你原有的谷歌浏览器数据。

Chrome 是基于开源浏览器 chromium 而搭建的闭源浏览器。如果你需要使用 Chromium，请依照一下步骤进行操作：

在 openSUSE 上安装 chromium：

```
sudo zypper in chromium 
```

安装闭源组件（可选）：

```
sudo zypper in chromium-bsu chromium-ffmpeg-extra chromium-plugin-widevinecdm
```

在 Fedora 上安装 chromium：

```
sudo dnf in chromium
```

安装由 RPMFusion 提供，适用于 Fedora 的完整版 chromium（可选）：

```
sudo dnf in chromium-freeworld
```

### Flatpak 版

你可以通过 Flatpak 安装 chrome/chromium：

安装谷歌浏览器：

```
flatpak install flathub com.google.Chrome #谷歌浏览器稳定版
```

```
flatpak install flathub com.google.ChromeDev #谷歌浏览器开发版
```

安装 chromium：

```
flatpak install flathub org.chromium.Chromium
```

安装 ungoogled-chromium：

!!! note
    ungoogled-chromium 是一个由社区维护，默认禁用谷歌隐私追踪的开源浏览器。详细说明、修改内容以及潜在性问题详见[此处](https://github.com/Eloston/ungoogled-chromium/blob/master/README.md)。

```
flatpak install flathub com.github.Eloston.UngoogledChromium
```

## Brave 浏览器

通过 Flatpak 安装：

```
flatpak install flathub com.brave.Browser
```

### 通过官方源安装

在 Fedora 上安装 Brave：

```
sudo dnf install dnf-plugins-core

sudo dnf config-manager --add-repo https://brave-browser-rpm-release.s3.brave.com/x86_64/

sudo rpm --import https://brave-browser-rpm-release.s3.brave.com/brave-core.asc

sudo dnf install brave-browser
```

在 openSUSE 上安装 Brave：

```
sudo zypper install curl

sudo rpm --import https://brave-browser-rpm-release.s3.brave.com/brave-core.asc

sudo zypper addrepo https://brave-browser-rpm-release.s3.brave.com/x86_64/ brave-browser

sudo zypper install brave-browser
```

## Vivaldi 浏览器

在 Fedora 上安装：

```
sudo dnf install dnf-utils

sudo dnf config-manager --add-repo https://repo.vivaldi.com/archive/vivaldi-fedora.repo

sudo dnf install vivaldi-stable
```

在 openSUSE 上安装：

```
sudo zypper ar https://repo.vivaldi.com/archive/vivaldi-suse.repo

sudo rpm --import https://repo.vivaldi.com/archive/linux_signing_key.pub

sudo zypper refresh && sudo zypper in vivaldi-stable
```

你也可以在 Vivaldi 官网[下载页面](https://vivaldi.com/zh-hans/download/)直接下载 rpm 软件包。

## Tor 浏览器

通过 Flatpak 安装：

```
flatpak install flathub com.github.micahflee.torbrowser-launcher
```

在 Fedora 上安装：

```
sudo dnf install torbrowser-launcher
```

在 openSUSE 上安装：

```
sudo zypper install torbrowser-launcher
```