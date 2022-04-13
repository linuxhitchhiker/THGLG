# 慢速开始 2

本文主要描述一些不会出现在官方文档上，但有必要执行的额外步骤。

## git

!!! note
    注意，在 fork 后，如果需要提交新内容，请创建一个新的分支（branch），然后通过这个分支向上游提交 PR。等上游合并后，再切换到主分支 `main` 合并上游的 commit。如此往复。

因为存在网络阻断，git 无法直接向 GitHub 提交数据。GitHub 也禁止用户直接使用账户和密码提交更改。所以你需要为 git 配置代理并使用 SSL 或者 token 连接到 GitHub。

### 为 git 配置代理

为 git 配置 http 代理

```
git config --global http.proxy protocol://127.0.0.1:port
```

注意：`--glboal` 选项指的是修改 Git 的全局配置文件 `~/.gitconfig`，而非各个 Git 仓库里的配置文件 `.git/config`。`protocol` 指的是代理的协议，如 `http`，`https` 或 `socks5` 等。`port` 则为端口号[^1]。

### 使用 gh-cli 托管 git

gh-cli 是由 GitHub 开发的命令行工具。功能和 [GitHub desktop](https://desktop.github.com/) 相似。

```
sudo zypper in gh  #在 openSUSE 上安装 gh-cli
sudo dnf in gh  #在 Fedora 上安装 gh-cli
```

然后你需要前往 GitHub 官网，在[设置](https://github.com/settings/tokens) 中生成一个新个人访问令牌（token）。这个 token 必须具有对 `workflow`、`read:org` 和 `repo` 三个区域的访问权限。

然后登陆 GitHub：

```
$ gh auth login
```

在登陆的时候，gh-cli 会询问你是否托管 git，建议选择 `yes`。授权方式建议选择 `Paste an authentication token`。官方文档详见[此处](https://cli.github.com/manual/)。

## Python 的必要配置

一般而言，Linux 都会将 python 的某个版本作为依赖预装。

查看你当前的 python3 版本：

```
bh@c004-h0:~> python3 --version
Python 3.8.13
bh@c004-h0:~> pip --version
pip 22.0.4 from /usr/lib/python3.8/site-packages/pip (python 3.8)
```

如果找不到相关信息，你需要安装 python3。

```
sudo zypper in python310 #在 openSUSE 上安装 python 3.10
sudo dnf in python310 #在 Fedora 上安装 python 3.10
```

### 镜像站

在你的用户目录下新建以下配置文件：

```
bh@c004-h0:~> cat ~/.pip/pip.conf
[global]
index-url = http://mirrors.aliyun.com/pypi/simple/
[install]
trusted-host=mirrors.aliyun.com
```

上述操作可以将 pip 使用的站点切换至国内镜像站。

### 安装依赖

```
$ git clone https://github.com/linuxhitchhiker/THGLG.git    #首先将仓库克隆至本地
$ cd THGLG && python3 -m pip install -r requirements.txt    #根据描述文件安装全部的依赖
$ python3 -m pip mkdocs server    #在本地启动实例
```

原始的命令比较长，你可以使用 `alias` 命令设置一个较短的命令。

```
$ alias mkdocs="python3 -m pip mkdocs"
```

## VScode 插件

推荐安装的扩展有

- Chinese (Simplified) (简体中文) Language Pack for Visual Studio Code - Microsoft
- GitLens — Git supercharged - GitKraken  
    多合一的 git 工具箱  
- Markdown All in One - Yu Zhang  
    多合一的 md 文档插件  
- Material Icon Theme - Philipp Kief  
    显示效果更清晰的图标主题  
    ![01](./images/icon-themes.png)
- Project Manager - Alessandro Fragnani  
    git 项目管理器（便捷地在多个 git 项目间切换） 

## 常见故障

<待补充>

[^1]: [一文让你了解如何为 Git 设置代理](https://ericclose.github.io/git-proxy-config.html)