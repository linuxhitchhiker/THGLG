---
title: 包管理器
---

!!! note
    `repository` 一词的完整原意是软件仓库。但它也可以被翻译成软件源，储存库或仓库。

## DNF

!!! note
    官方手册详见[此处](https://docs.fedoraproject.org/en-US/fedora/latest/)。

DNF 是 Fedora 项目包管理器，它能用于管理软件包，软件源和更新系统。

### 检查更新

```
dnf upgrade #检查系统更新
```

注意，dnf 只会安装可用的更新，存在问题（如被锁定、依赖存在问题等）的软件包会被自动跳过。

你可以使用 `dnf check-update` 检查当前可用的更新包

```
~]# dnf check-update
Using metadata from Mon Apr 20 16:34:10 2015 (2:42:10 hours old)

python.x86_64                     2.7.9-6.fc22          updates
python-cryptography.x86_64        0.8.2-1.fc22          updates
python-libs.x86_64                2.7.9-6.fc22          updates
```

如上，可更新的软件包都会被列举出来，其中：

- `python` 是软件包的名称
- `x86_64` 是软件包构建的 CPU 架构类型  
    * `noarch` 表示软件包没有为特定的 CPU 架构进行构建  
- `2.7.9` 是软件包的版本
- `6.fc22` 是软件包的更新版本
- `updates` 是软件包所属的软件源

### 更新软件包

你可以使用 `dnf upgrade` 命令更新软件包。或者将某个软件包的名称作为参数放置到末尾，让 dnf 更新特定的某个软件包。

```
# dnf upgrade package_name
```

在更新过程中，dnf 会询问你一些问题（比如是否接受更新），如果你熟悉 dnf 的工作流程，你可以将 `-y` 作为选项放置到命令的默认，提示 dnf 自动接受所有问题的默认值。

### 查找软件包

你可以使用 `dnf search` 检索相关软件包名称和概述。

```
dnf search <关键字>
```

搜索的关键字支持元字符，比如 `dnf search *nvidia*` 可以检索任何匹配 `nvidia` 字符的软件包。

### 列举软件包

`dnf list` 和相关的命令可以列举软件包、软件包组（package groups）和软件源（repositories）。

```
dnf list <关键字>
```

上述命令可以列举匹配关键字的软件包

```
dnf list all
```

上述命令可以列举出所有已安装和可用的软件包。

```
dnf list installed <关键字>
```

上述命令可以列举匹配关键字，已安装的软件包。

```
dnf list available <关键字>
```

上述命令可以列举出所有已启用的软件仓库中，匹配关键字的，可获得的软件包。

```
dnf group list
```

上述命令可以列举出所有的软件包组（一个软件包组包含了用于某一特定目的的全部软件包）

```
~]# dnf repolist
Last metadata expiration check performed 0:48:29 ago on Mon May 25 23:38:13 2015.
repo id                             repo name                           status
*fedora                             Fedora 22 - x86_64                  44,762
*updates                            Fedora 22 - x86_64 - Updates             0
```

上述命令可以列举出**已启用**的仓库的 ID、名称和提供的软件包数量。


```
dnf repository-packages repo_id list [option]
```

上述命令的默认行为是列举出特定的软件仓库的软件包。你需要将 `repo_id` 替换成特定软件仓库的 ID。可用的选项是 `available` 和 `installed`，用于提示 dnf 应该列举哪种软件包（已安装还是可获得）。

### 显示软件包的信息

```
dnf info <软件包包名>
```

上述命令可以显示指定的软件包的详细信息（包名、架构、版本、开发者链接、许可证信息等内容）。

```
dnf repoquery <软件包包名> --info
```

要显示有关所有可用软件包的信息，包括已安装的和可从存储库获得的，请使用如上命令。

更多帮助信息请使用：

```
$ dnf repoquery -h
```

### 安装软件包

```
dnf install <软件包包名>
```

上述命令可以安装匹配指定包名的软件包。你也可以一次性安装多个软件包，比如 `$ sudo dnf in smplayer smplayer-themes deadbeef`。软件包包名是 `dnf in` 的选项，而这个命令支持元字符和 glob 表达式。

软件包组和单一的软件包很相似，你无法单独使用软件包组的某一个软件包，它们需要全部安装后才能正常工作。如果你尝试安装其中的一个软件包，dnf 会自动安装同一个组内的其他软件包。每一个软件包组都有一个组名称（group_name）和组 ID（groupid, GID）。`dnf group list -v` 命令可以列举出所有的软件包组的名称和它们的 GID

```
# dnf -v group list kde\*
cachedir: /var/cache/dnf/x86_64/22
Loaded plugins: builddep, config-manager, copr, playground, debuginfo-install, download, generate_completion_cache, kickstart, needs-restarting, noroot, protected_packages, Query, reposync, langpacks
initialized Langpacks plugin
DNF version: 0.6.5
repo: using cache for: fedora
not found deltainfo for: Fedora 22 - x86_64
not found updateinfo for: Fedora 22 - x86_64
repo: using cache for: updates-testing
repo: using cache for: updates
not found updateinfo for: Fedora 22 - x86_64 - Updates
Using metadata from Thu Apr 16 13:41:45 2015 (4:37:51 hours old)
Available environment groups:
   KDE Plasma Workspaces (kde-desktop-environment)
```

比如 KDE 相关的软件包组叫 `KDE Plasma Workspaces`，它的 GID 是 `kde-desktop-environment`。

你可以使用下列命令安装某个软件包组：

```
dnf group install group_name
dnf group install groupid
dnf install @group
```

!!! note
    并不建议使用在同一个系统上安装多个桌面环境，这可能会造成一些未知的问题，以及大量难以清理的依赖软件包。

对于软件包组名称存在多个单词的软件包组，你需要使用引号将其包裹起来，比如

```
# dnf group install "KDE Plasma Workspaces"
# dnf group install kde-desktop-environment
# dnf install @kde-desktop-environment
```

### 移除软件包

你可以使用下列命令删除特定的软件包。相似地，你可以同时删除多个软件包：

```
# dnf remove package_name
```

```
dnf group remove group
dnf remove @group
```

上述命令可以删除某一个软件包组。

### 使用事务历史

dnf history 命令允许用户查看有关 DNF 事务（Transaction）的时间线、它们发生的日期和时间、受影响的包数、事务是成功还是中止以及事务之间是否更改了 RPM 数据库的信息。此外，此命令可用于撤消或重做某些事务。

```
# dnf history list
```

上述命令可以列出全部的事务历史（transaction history）。

```
dnf history list start_id..end_id
```

上述命令可以指定显示特定范围的事务历史。

你还可以仅列出有关特定软件包或软件包的事务历史。为此，请使用带有软件包包名或 glob 表达式的命令：

```
dnf history list <选项>
```

```
~]# dnf history list 1..4
Using metadata from Thu Apr 16 13:41:45 2015 (5:47:31 hours old)
ID     | Login user               | Date a | Action | Altere
-------------------------------------------------------------------------------
     4 | root <root>              | 2015-04-16 18:35 | Erase          |    1
     3 | root <root>              | 2015-04-16 18:34 | Install        |    1
     2 | root <root>              | 2015-04-16 17:53 | Install        |    1
     1 | System <unset>           | 2015-04-16 14:14 | Install        |  668 E
```

dnf history list 命令生成表格输出，每行由以下列组成：

- `ID` —— 标识特定事务的整数值。
- `Login user` —— 启动事务的用户的用户名，此信息通常以 *`Full Name <username>`* 形式显示，但有时会显示用于执行事务的命令。 对于不是由用户发出的事务（例如自动系统更新），使用 `System <unset>` 代替。
- `Date and time` —— 事务的发生日期和时间。
- `Action(s)` —— 事务期间执行的操作列表，如操作字段的可能值中所述。
- `Altered` —— 受事务影响的软件包数量，后面可能还有其他信息。

Action(s) 字段的可能值如下：

|Action|缩写|描述|
|---|---|---|
|`Downgrade`|`D`|至少有一个软件包已降级为旧版本。|
|`Erase`|`E`|至少一个包裹已被移除。|
|`Install`|`I`|至少安装了一个新软件包。|
|`Obsoleting`|`O`|至少有一个软件包被标记为过时。|
|`Reinstall`|`R`|至少已重新安装一个软件包。|
|`Update`|`U`|至少有一个软件包已更新到较新的版本。|

#### 还原和重复事务

除了查看事务历史，`dnf history` 命令还提供了撤销或重复选定事务的方法。请在 shell 提示符下以 `root` 身份键入以下内容：

```
dnf history undo id #撤销某个事务
dnf history redo id #重复某个事务
```

!!! note
    请注意，`dnf history undo` 和 `dnf history redo` 命令都只是撤销或重复在事务期间执行的步骤，如果所需的包不可用，则会失败。例如，如果事务安装了一个新包，`dnf history undo` 命令将卸载它并尝试将所有更新的包降级到以前的版本，但如果所需的包不可用，该命令将失败。

这两个命令都支持使用 `last` 作为参数，来撤销或重复最新一次的事务。

### DNF 配置文件

有关 dnf 配置文件和 dnf 仓库的指南信息，请阅读[官方指南](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/package-management/DNF/#sec-Configuring_DNF_and_DNF_Repositories)。

### 管理软件仓库

`dnf config-manager` 命令可以用于添加、启用/禁用和移除软件仓库。

!!! note
    记录有仓库信息和配置的文件都存放在 `/etc/yum.repos.d` 文件夹中。在禁用了仓库后，你可以手动删除一些弃用仓库的配置文件。

使用下述命令添加新仓库：

```
dnf config-manager --add-repo repository_url
```

`repository_url` 应该包含 `.repo` 文件或者指向 `.repo` 文件。

使用下述命令启用仓库：

!!! note
    此处的 repository 指的是仓库的 repository ID

```
dnf config-manager --set-enabled repository
```

使用下述命令禁用仓库：

```
dnf config-manager --set-disabled repository
```

### 额外信息

- `dnf(8)` — DNF 命令参考手册页。
- `dnf.conf(8)` — DNF 配置参考手册页。

## Zypper