---
title: "运用文本文件"
---

# 运用文本文件

与 Windows 不同，你可以通过编辑储存于特定目录（比如 `/etc`）的纯文本文件来实现对于系统配置的修改和管理系统。

## 使用文本编辑器编辑文件

Linux 终端常用的文本编辑器有很多，其中比较知名的有 [Vim](https://www.vim.org)、[Emacs](https://www.gnu.org/software/emacs/) 和 [Nano](https://www.nano-editor.org/)

流行的图形化的文本编辑器还有：[KDE Kate](https://apps.kde.org/kate/)、[Gnome Gedit](https://wiki.gnome.org/Apps/Gedit)、[Xfce Mousepad](https://docs.xfce.org/apps/mousepad/start) 和微软的 [Visual Studio Code](https://code.visualstudio.com/)。前三者分别是各个主流桌面环境内置的默认文本编辑器，VScode 则是近年来由微软开发，广受开发人员好评的一个富文本编辑器。

如果你想要深入了解如何在命令行界面中工作，Emacs 和 Vim 是两个功能强大，扩展丰富，值得信赖的专业工具集。

如果你只是偶尔用用命令行界面，你可以简单学习以下如何使用 Nano 编辑文件。

### 使用 Nano

Nano 一般已经安装到你的 Linux 中，打开终端，输入 `$ nano`

![Nano](./assets/nano_editor.png)

如上图所示，Nano 是一个功能简单，界面友好的轻量级编辑器。底部有快捷键提示。要查询更多信息，按下 `Ctrl + G` 即可打开用户手册，按 `q` 即可退出手册页。

你可以使用方向键控制光标的位置，同时使用鼠标进行辅助（如选中内容，上下翻页）。快捷键组合中的 `^` 是指 `Ctrl` 键。编辑完文件后，注意保存（Ctrl + O）然后再退出编辑器（Ctrl + X）。

你可以使用 nano 编辑指定路径的文件，如 `$ nano ~/.bashrc`，如果你编写的文件并不存在，Nano 会在你保存后创建该文件。

## 搜索文件