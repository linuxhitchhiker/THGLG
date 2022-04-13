# 慢速开始 1

!!! note
    年轻的读者呦，慢慢来，心急吃不了热豆腐。

## 前置条件

### 英语

如上，你需要大约中学英语的水平来阅读一些原始文档和指南。或者你可以使用谷歌翻译或其他的在线翻译引擎翻译原始文档。

### Linux

- 了解 Shell 的基本用法和简单的概念。
- 了解 Linux 和其他一些知识（比如 ffmpeg 解码和编码方法，你要写文章总得先有东西可写吧）。

### 代理服务

我们默认贡献者已经配置了代理服务，并可以正常访问 https://www.google.com

### Markdown

掌握 Markdown 语法规则。

- [Markdown 中文教程](https://markdown.com.cn/)

### Git

了解 Git 的基本概念，基本工作原理。

!!! note
    不求精通 git，记住各种 git 命令。但你起码得知道 git 是怎么一回事。

- [ProGit 2nd Edition (2014) 中文版](http://git-scm.com/book/zh/v2)  
    * 关于《ProGit》，你至少需要看完前三章以及第六章的内容。

### GitHub 账户

你可以参考《ProGit》第六章，注册一个 GitHub 账户，然后将 [THGLG](https://github.com/linuxhitchhiker/THGLG/) fork 到自己的账户中，再 clone 到本地。

### 文档排版规范

建议阅读以下内容：

- [Copywriting - 中文文案排版指北（简体中文版）](https://mazhuang.org/wiki/chinese-copywriting-guidelines/)

## 工具

### git

git 已经在 openSUSE 和 Fedora 的官方软件源之中，你可以直接安装：

```
$ sudo zypper in git-core #在 openSUSE 上安装 git
$ sudo dnf in git-core #在 Fedora 上安装 git
```

### VScode

推荐使用 [vscode](https://code.visualstudio.com/)。它是一个功能丰富，易于使用的文本编辑器。而且有丰富的扩展（其中包括图形化的 git 管理工具）。

- 在 Fedora 上安装：  
    添加软件源：
    ```
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    ```
    然后检查更新，并安装 vscode：
    ```
    sudo dnf check-update && sudo dnf install code
    ```
- 在 openSUSE 上安装：  
    添加软件源：
    ```
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
    ```
    刷新软件源，并安装 vscode：  
    ```
    sudo zypper ref && sudo zypper in code
    ```

### Python

建议根据官方指南，使用 python 安装 `mkdocs` 和 `mkdocs-material`。

### 扩展语法和配置文件

Mkdocs-material 支持许多实用的 markdown 扩展语法：

- [Reference - mkdocs-material](https://squidfunk.github.io/mkdocs-material/reference/)

你还需要了解一下 Mdkocs 的一些配置信息，以方便将你的文档和链接添加到合适的位置：

- **[Mkdocs User Guide](https://www.mkdocs.org/user-guide/)**