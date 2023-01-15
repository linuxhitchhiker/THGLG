---
title: "文书工作"
---

## 纯文本文档与标记语言

**纯文本文档**[^1]是一种没有任何附加信息（例如语言标识符、字体大小、颜色、超文本链接等），只记录文本字符本身，不存储文本格式，人类可直接阅读的文本表现形式。最为常见的是以 `.txt` 为后缀名的各种文本文件。

**标记语言**[^2]是一种将文本以及文本相关的其他信息（例如语言标识符、字体大小、颜色、超文本链接等）结合起来，展现出关于文档结构和数据处理细节的电脑文字编码。最常见的标记语言是 [HTML](https://en.wikipedia.org/wiki/HTML)。

相比于最为原始的纯文本文档，标记语言可以表达更为丰富的内容，同时兼具纯文文档大部分优点。

## 为什么要使用纯文本文档 + 标记语言？

1. 相较于 `docx`、`xlsx` 等商业文档格式，纯文本能做的事情实在是太少了，它甚至无法完成一些对于商业文档文件轻而易举的事情（例如插入图片、绘制表格）。
2. 标记语言使用特定的符号、语法、书写约定弥补了纯文本的缺陷。但它仍然是纯文本文档的一种，并具备人类直接可读性。
3. 商业公司兜售的各种办公软件、笔记软件本质是一种服务，这些文档大多数是（与[开放文档标准](https://www.libreoffice.org/discover/what-is-opendocument/)不兼容）私有格式或半开放格式；如果你选择使用他们的产品，你必然需要为此付出一笔不菲的授权费用（参考 Microsoft office 动辄数百元的年费）。
4. 上述的软件使用的文档格式大部分不会把跨系统兼容作为优先事项，甚至他们自身的客户端也不是跨平台或跨平台体验不佳（参考 Microsoft office for mac 以及 Microsoft office 至今没有一个可用的 Linux 客户端）。
5. 商业公司不在乎你的文档能不能在数十年后仍然可读。尽管他们会不懈余力地宣传自己的办公产品各种优异性能，但实现这一切的默认前提是文档的接收者必须和你使用一样的产品，可谓是一种有限的产品内兼容。他们也不在乎你是否能够真正与其他用户无缝交流，他们只在乎能不能将你和他们的产品绑定在一起，从而实现对你进行收费或挖掘个人隐私数据等盈利目的。
6. 时至今日，任何的电脑，手机和任意的操作系统都原生支持纯文本文件。纯文本文件依靠自身就实现了诸多商业软件难以搞定的跨平台支持。  
    * 它足够简单，允许你基于纯文本文档添加各种顶层结构（比如 markdown 语法和 git 项目管理工具）；  
    * 它足够自由，你不必担忧未来出现你无法读取你的文档或者有人宣布你的文档格式不受支持的情况；  
    * 它足够开放，有大量的工具支持编辑纯文本文件，可以提供远比微软 notepad 之类的元老级文本编辑器更好的使用体验；  
    * 它不需要授权收费，不需要网络连接，不依赖特定的软件平台。

## 我不想使用标记语言

使用标记语言书写文档需要你首先去熟悉标记语言的语法，挑选一个趁手的文本编辑器，这是一件需要时间和精力的事情。如果你只想要一个开箱即用的方案，请参考如下解决办法：

### WPS

WPS 是目前已知的，对 Microsoft office 兼容性最好的办公软件套件。

你可以直接在 [WPS For Linux 官网](https://www.wps.com/office/linux/)下载适用于 Fedora 的 rpm 安装包，然使用 `rpm`  命令安装 WPS:

```
sudo rpm -i wps-office-*.rpm
```

或通过 Flatpak 安装 WPS：

!!! bug "中文语言支持"

    现有的 Flatpak 版是 wps 国际版，不包含中文语言包。

```
flatpak install flathub com.wps.Office
```

openSUSE 用户可通过 OBS 仓库安装：

```
sudo zypper addrepo https://download.opensuse.org/repositories/home:fusionfuture:office/openSUSE_Tumbleweed/home:fusionfuture:office.repo
```
```
sudo zypper refresh && sudo zypper install wps-office
```

由于许可证的原因，WPS 不能携带一些 windows 字体，你需要自行去搜索下载相关的字体文件。你可以在 [BannedPatriot/ttf-wps-fonts](https://github.com/BannedPatriot/ttf-wps-fonts) 下载缺失的字体。

### Libreoffice

除了 WPS，[Libreoffice](https://zh-cn.libreoffice.org/) 也是一个知名的开源软件办公套件。

- LibreOffice 是一款功能强大的办公软件，默认使用开放文档格式 (OpenDocument Format, ODF), 并支持 `.docx`、`.xlsx`、`.pptx` 等其他格式。
- 它包含了 Writer、Calc、Impress、Draw、Base 以及 Math 等组件，可用于处理文本文档、电子表格、演示文稿、绘图以及公式编辑。
- 它可以运行于 Windows, GNU/Linux 以及 macOS 等操作系统上，并具有一致的用户体验。

- [用户文档](https://documentation.libreoffice.org/zh-cn/docs)
- [Libreoffice 中文社区](https://www.libreofficechina.org/)

你可以直接安装它：

```
sudo zypper in libreoffice
sudo dnf in libreoffice
```

----

## 有哪些推荐的标记语言与工具？

!!! warning "文本编码"

    使用标记语言的时候，注意将文本文件的编码设置为 [UTF-8](https://zh.wikipedia.org/wiki/UTF-8)。

这里主要推荐两种标记语言、一种版本控制工具和一种文本编辑器。

当然，标记语言和文本编辑器的可选项是非常丰富的，仅 GitHub 就[支持七种不同的标记语言](https://github.com/github/markup#markups)。功能强大的文本编辑器更是数不胜数。

### Markdown

Markdown 是目前最为流行的标记语言，它的语法很简单，可以快速上手。

快速开始：

- [Markdown 中文教程](https://markdown.com.cn/)

!!! tip "一些建议"

    - 不必过于纠结于使用何种 Markdown 方言，他们大体上是相同的，只是某些细节略有差异。  
    - 当你根据上文的连接初步了解了 markdown 语法以后，基本就可以开始使用 markdown 书写 md 文档了。
    - 如果你需要使用 GitHub，那么你应该去了解一下 GitHub 的语法规范；如果你需要使用 pandoc，那了解一下 pandoc 的语法规范是不错的选择。

但 Markdown 由于其设计者的缘故，并未存在一种标准的语法规范，导致目前各种 markdown 方言纷繁复杂。其中较为广泛使用的有三种：

- [GitHub Flavored Markdown Spec](https://github.github.com/gfm/)  
    - GitHub 的 markdown 语法规范。  
- [CommonMark Spec](https://spec.commonmark.org/)  
    - [CommonMark](https://commonmark.org/) 致力于为 markdown 提供一套标准的、明确的语法规范、以及一套综合测试来根据该规范验证 Markdown 实现。
- [Pandoc’s Markdown](https://pandoc.org/MANUAL.html#pandocs-markdown)  
    - 这是由功能极其强大的文档万向转换器 [Pandoc](https://pandoc.org/index.html) 所支持的一种 markdown 规范，它定义了许多原始 markdown 规范所缺少的部分，也是一种广为使用的 markdown 方言。

markdown 适合于小型文档或排版简单的文档。如果文档很复杂，需要精细化排版，markdown 就不是一个合适的选择了。

有些时候，为了实现一些效果，你可能需要额外了解一些 [HTML](https://www.runoob.com/html/html-tutorial.html) 或 [CSS](https://www.runoob.com/css/css-tutorial.html) 语法

### AsciiDoc

[AsciiDoc](https://asciidoc.org/) 是 markdown 的许多替代品之一。

AsciiDoc 相比 Markdown 有如下优势：

- 几乎在所有情况下，与 Markdown 相比，AsciiDoc 使用相同数量或更少的标记字符；
- AsciiDoc 使用一致的格式化方案（即，它具有一致的模式）；
- AsciiDoc 可以处理嵌套内联（和块）格式的所有排列，而 Markdown 经常失败；
- AsciiDoc 处理 Markdown 不处理的情况，例如内字标记、源代码块和块级图像的正确方法。

如果你打算使用 AsciiDoc 创作文档、文章或电子书，你可以先阅读：

- [AsciiDoc Writer’s Guide](https://asciidoctor.org/docs/asciidoc-writers-guide/)
- [AsciiDoc Syntax Quick Reference](https://docs.asciidoctor.org/asciidoc/latest/syntax-quick-reference/)

### git

[git](https://git-scm.com/) 是一种应用广泛，开源的版本控制工具。git 可以帮助用户对包括但不限于纯文本文件在内的文件进行备份、恢复、变更内容比较和多人协作等一系列[版本控制](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%85%B3%E4%BA%8E%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6)任务。

推荐阅读：

- [ProGit 2nd Edition (2014) - 中文版](https://git-scm.com/book/zh/v2)

要安装 git，请执行：

```
sudo zypper in git-core
sudo dnf in git-core
```

### VS code

[Visual Studio Code](https://code.visualstudio.com/) 简称为 VS Code，是由微软开发，源代码开源的一款源代码编辑器。该软件支持语法高亮、代码自动补全、代码重构功能，并且内置了命令行工具和 Git 版本控制系统。用户可以更改主题和键盘快捷方式实现个性化设置，也可以通过内置的扩展程序商店安装扩展以拓展软件功能[^3]。

> 在 2019 年的 [Stack Overflow](https://zh.wikipedia.org/wiki/Stack_Overflow) 组织的开发者调查中，Visual Studio Code 被认为是最受开发者欢迎的开发环境。据调查，87317 名受访者中有 50.7% 的受访者声称正在使用 Visual Studio Code[^4]。

你可以执行以下步骤安装 vscode：

对于 fedora 用户：

```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
```

```
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
```

```
sudo dnf check-update && sudo dnf install code
```

对于 openSUSE 用户：

```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
```

```
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
```

```
sudo zypper refresh && sudo zypper install code
```

### 为什么推荐 VS code

如你所见，你在此站点所看到的大部分内容都是使用本文所列举的（除了 libreoffice 和 wps 之外的）工具编写出来的。

当然这并不意味着其他的文本编辑器就不如 VS code，VS code 也有着它属于它自己的不足[^5]和争议[^6]。

你也可以将所有主流的文本编辑器都试一遍，然后挑出合适自己的即可。

### 插件

VS code 有着丰富的扩展插件可供用户选择，这也是它的魅力之一。

一些推荐的基础插件：

- [Chinese (Simplified) (简体中文) Language Pack for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hans)
- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)
- [AsciiDoc](https://marketplace.visualstudio.com/items?itemName=asciidoctor.asciidoctor-vscode)
- [Project Manager](https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager)
- [GitLens — Git supercharged](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
- [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)
- [Photonica](https://marketplace.visualstudio.com/items?itemName=ConAntares.Photonica)
- [Dynamic Theme](https://marketplace.visualstudio.com/items?itemName=guangzan.dynamic-theme)

----

## E-mail

[Thunderbird](https://www.thunderbird.net/en-US/) 和 [evolution](https://wiki.gnome.org/Apps/Evolution) 都是流行的 Linux 邮件客户端。你可以任选一个安装至你的电脑。

!!! note
    如果你使用 `evolution` ，请再安装 `evolution-ews` 插件。

在 openSUSE 上安装邮件客户端：

```
sudo zypper in MozillaThunderbird 
sudo zypper in evolution
```

在 Fedora 上安装邮件客户端：

```
sudo dnf in MozillaThunderbird 
sudo dnf in evolution
```

或者你可以使用浏览器使用在线的网页邮件客户端。

## 思维导图

开源的在线思维导图工具：[draw.io](https://app.diagrams.net/#)。draw.io 还支持 Linux 平台。

## 字典

[Goldendict](http://goldendict.org/) 是一个功能强大，支持诸多字典格式的字典查词软件。

```
sudo zypper in goldendict goldendict-lang
sudo dnf in goldendict
```

- [FreeMdict Forum](https://forum.freemdict.com/) 是一个聚焦于各类字典与使用的爱好者论坛。

[欧陆词典](https://dict.eudic.net/) 也是一个流行的字典软件，但 Linux 版不支持屏幕取词。

[Bing 在线词典](https://www4.bing.com/dict?FORM=HDRSC6) 是一个简单易用的在线网络词典。

[DeepL](https://www.deepl.com/translator)：免费的在线翻译引擎，由人工神经网络驱动。


[^1]: 更为详细的介绍，另见：[纯文本 - Wikipedia](https://en.wikipedia.org/wiki/Plain_text)  
[^2]: 更为详细的介绍，另见：[标记语言 - Wikipedia](https://en.wikipedia.org/wiki/Markup_language)  
[^3]: 原文节选自：[Visual Studio Code - Wikipedia](https://zh.wikipedia.org/wiki/Visual_Studio_Code)  
[^4]: [Development Environments and Tools - Developer Survey Results 2019](https://insights.stackoverflow.com/survey/2019#development-environments-and-tools)  
[^5]: 有人认为 VS code 过于臃肿，已经脱离了源码编辑器的范畴，成为了一个[集成开发环境](https://en.wikipedia.org/wiki/Integrated_development_environment)（IDE）。  
[^6]: 例如，微软将源码开源，分发的二进制文件闭源并嵌入自己的私有模块的做法饱受社区诟病，催生了 [VScodium](https://flathub.org/apps/details/com.vscodium.codium) 的诞生。  