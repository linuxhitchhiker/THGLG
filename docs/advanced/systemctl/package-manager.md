---
title: 包管理器
---

!!! bug
    本条目还缺少 `apt` 包管理器的使用指南，欢迎补充。

!!! note
    * `repository` 一词的完整原意是软件仓库。但它也可以被翻译成软件源，储存库或仓库。
    * 有关 Flatpak 包管理器的使用详见[此处](./../../solution/software/flatpak-get-start.md)。
    * 有关 rpm 包管理器的使用详见：`$ man rpm` 或 `$ rpm --help`

## 软件包与依赖关系

在 Linux 上，通过统一的软件源分发的应用程序都被打包成软件包（package）的形式。一个完整的应用程序，常常会被拆分成多个小部件，即子包（subpackage），并且有很多软件子包是共享的。

如果将一个功能完整的应用程序类比为一辆汽车，则子包是需要组装在一起的部件（例如车身、引擎、传动等）。如果一个软件包 A 要正常发挥基本功能需要用户安装软件包 B，则我们将软件包 B 称之为软件包 A 的依赖（`dependencies`）或者软件包 A 需要（`require`）软件包 B。例如，汽车要能够跑起来，必然需要发动机正常工作，则发动机是汽车的"依赖"。

如果软件包 A 要发挥额外的功能，需要用户安装软件包 C，则我们称软件包 C 是软件包 A 的推荐依赖（`recommend`）。不安装软件包 C 不影响软件包 A 的正常工作，但会让软件包 A 无法发挥完整的功能。例如，汽车如果没有车载收音机，则用户无法收听交通广播。但没有车载收音机并不影响汽车正常行驶。此时车载收音机就是一种"推荐"安装的部件。

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

上述命令可以安装匹配指定包名的软件包。你也可以一次性安装多个软件包，比如 `$ sudo dnf in smplayer smplayer-themes deadbeef`。软件包包名是 `dnf in` 的选项，而这个命令支持元字符和 [glob 表达式](https://rgb-24bit.github.io/blog/2018/glob.html)。

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

!!! note
    完整的使用指南详见[此处](https://doc.opensuse.org/documentation/leap/reference/html/book-reference/cha-sw-cl.html)。

zypper 是 openSUSE 默认的软件包管理器，可以用于管理软件包、软件仓库和升级更新系统。

### 管理软件包

#### 一般使用

zypper 的命令格式如下：

```
zypper [--global-options] COMMAND  [--command-options] [arguments]
```

使用 `[]` 包围起来的部分不是必须使用的。你可以键入 `$ zypper --help` 查看通用选项（`--global-options`）和命令（`COMMAND`）的完整列表。你也可以使用 `$ zypper help COMMAND` 查看特定的命令的帮助信息。

- Zypper command  
    执行 zypper 最简单的方式是直接键入命令的名字，例如应用全部可用的更新补丁：  
    ```
    sudo zypper patch
    ```
- 全局选项（`--global-options`）  
    你可以在 zypper 后直接添加一个或多个选项，来实现额外的功能，例如：  
    ```
    sudo zypper --non-interactive patch
    ```
    如上，`--non-interactive` 选项表示命令会直接运行而不询问用户的意见（即自动以默认的答案回答命令执行过程中出现的问题）。注意，如果你不清楚 zypper 的工作流程和相关的默认配置，请不要跳过手动处理阶段。  
- 命令特定选项（`--command-options`）   
    要使用命令特定的选项，你需要将这些选项直接放置在命令的后面，例如：  
    ```
    sudo zypper patch --auto-agree-with-licenses
    ```
    如上，`--auto-agree-with-licenses` 选项会自动确认并接受补丁包的许可证信息。如果你没有添加该选项，你需要阅读并接受许可证（比如 NVIDIA 私有驱动的最终用户使用协议）。    
- 参数（`Arguments`）  
    一些命令需要用户提供一个或多个参数。例如，使用 zypper 安装软件包时，你需要声明要安装哪些软件包，如下：  
    ```
    sudo zypper install smplayer
    ```
    有些命令特定选项也需要额外的参数，例如列出全部已知的模组：  
    ```
    sudo zypper search -t pattern
    ```

你也可以将上面的用法同时堆叠在一起，写出一个很长的命令。例如，下列命令会从 `factory` 仓库安装 `vim` 和 `mc` 软件包，并显示冗余信息：

```
sudo zypper -v install --from factory mc vim
```

如果没有特别声明，`--from` 选项默认从全部已启用的软件仓库检索软件包。你也可以使用 `--repo` ，她是 `--from` 的别名。

大多数 zypper 命令都具有 `dry-run` 选项，可以模拟运行给定的命令。该选项可以用于测试用途。例如：

```
sudo zypper remove --dry-run MozillaFirefox
```

#### 搜索软件包

你可以使用下述命令查询符合关键字的软件包：

!!! note
    更多信息详见：[2.1.7 Querying repositories and packages with Zypper](https://doc.opensuse.org/documentation/leap/reference/html/book-reference/cha-sw-cl.html#sec-zypper-query)

```
zypper search <关键字>
```

要查询某个软件包的信息，请使用：

```
zypper info <软件包包名>
```

#### 安装，删除软件包

你可以使用下列命令安装或移除特定的软件包（参数是软件包包名 `PACKAGE_NAME`）：

!!! warning
    请不要使用 zypper 删除重要的系统软件包（比如 `glic`、`zypper` 和 `kernel` 等软件包），这可能会导致系统崩溃。

```
sudo zypper install PACKAGE_NAME
sudo zypper remove PACKAGE_NAME
```

!!! note
    关于 `zypper install` 和 `zypper remove` 命令更多详细用法，详见 [2.1.3 Installing and removing software with Zypper](https://doc.opensuse.org/documentation/leap/reference/html/book-reference/cha-sw-cl.html#sec-zypper-softman)。

#### 更新软件包

你可以使用下列命令更新软件包：

```
sudo zypper dup                  #更新全部的软件包，即更新系统
sudo zypper update PACKAGE_NAME  #更新特定的软件包
```

你可以使用下述命令查看当前系统需要更新的软件包：

!!! note
    * 这个命令只能列举出没有发生供应商变更的软件包的更新版本。即已安装的软件包和要安装的新版本必须来自于同一个软件源。
    * 要安装的软件包所属的仓库的优先级必须与已安装的软件包所属的仓库的优先级至少相同。  
    * 必须可安装。（满足所有的依赖关系）

你可以使用下述命令查看全部可获得的软件包更新（不论是否可安装）：

```
sudo zypper list-updates --all
```

要查看某个软件包不能安装的原因，你可以使用 `zypper install` 或 `zypper update` 命令查看详细信息。

#### 识别孤立包

当你删除某些仓库或者升级你的系统后，某些软件包可能进入 `orphaned`（孤立）状态。这些孤立包不属于任何已启用的软件仓库。你可以使用下列命令查看这些软件包：

```
sudo zypper packages --orphaned
```

#### 识别使用已删除文件的进程或程序

你可以使用下列命令输出仍然在使用已删除文件的进程或程序的 PID、UID、所属的用户和命令等相关信息。

!!! note
    详细信息详见：[2.1.5 Identifying processes and services using deleted files](https://doc.opensuse.org/documentation/leap/reference/html/book-reference/cha-sw-cl.html#sec-zypper-ps)

```
zypper ps-s
```

在更新后，你需要手动重启这些程序或进程以应用更新，但你可以直接重启系统。

### 管理软件仓库

zypper 可以用于管理软件仓库：

键入以下命令查看你当前使用的软件仓库概况，例如：

```
bh@c004-h0:~> zypper repos
软件源优先级已生效：                                                                               (细节请参考 'zypper lr -P')
      90 (更高的优先级) :  1 个软件源
      99 (默认优先级)   :  6 个软件源

#  | Alias                    | Name                        | Enab-> | GPG Ch-> | Re->
---+--------------------------+-----------------------------+--------+----------+-----
 1 | NVIDIA                   | NVIDIA                      | 是     | (r ) 是  | 是
 2 | OPEN-TUNA:TW:NON-OSS     | OPEN-TUNA:TW:NON-OSS        | 是     | (r ) 是  | 是
 3 | OPEN-TUNA:TW:OSS         | OPEN-TUNA:TW:OSS            | 是     | (r ) 是  | 是
 4 | code                     | Visual Studio Code          | 是     | (r ) 是  | 是
 5 | google-chrome            | google-chrome               | 是     | (r ) 是  | 是
 6 | home_fusionfuture_office | home:fusionfuture:office    | 是     | (r ) 是  | 是
 7 | packman                  | packman                     | 是     | (r ) 是  | 是
 8 | repo-debug               | openSUSE-Tumbleweed-Debug   | 否     | ----     | ----
 9 | repo-non-oss             | openSUSE-Tumbleweed-Non-Oss | 否     | ----     | ----
10 | repo-oss                 | openSUSE-Tumbleweed-Oss     | 否     | ----     | ----
11 | repo-source              | openSUSE-Tumbleweed-Source  | 否     | ----     | ----
12 | repo-update              | openSUSE-Tumbleweed-Update  | 否     | ----     | ----
```

如上，这是一个禁用了官方软件源，使用镜像源和多个第三方软件源的 tumbleweed 系统。在与软件仓库相关的一系列命令和选项中，建议使用使用仓库的别名 `Alias` 作为参数。

#### 添加软件仓库

要添加一个新的软件仓库，你使用下列命令：

```
sudo zypper addrepo URL ALIAS
```

URL 是仓库的地址，ALIAS 是仓库的别名。你可以随意指定仓库的别名，但是请保持新添加的仓库的别名是独有的，不与其他已有的仓库别名重复。

#### 刷新软件仓库

你可以使用下列命令刷新软件仓库:

!!! note
    一些命令会自动刷新软件仓库，你不需要特意去执行这个命令。

```
sudo zypper refresh
```

#### 移除软件仓库

你可以使用下列命令移除匹配指定的仓库别名的仓库：

```
sudo zypper removerepo REPO_ALIAS
```

#### 编辑仓库

你可以使用 `zypper modifyrepo` 命令编辑仓库的属性。

|选项|用途|
|---|---|
|-e|启用已禁用的软件源。|
|-d|禁用但不移除软件源。|
|-a|应用修改到全部软件源。|
|-F|禁用软件源的自动刷新。|
|-p|设置软件源的优先级。|

要查看完整的选项信息，你可以键入 `$ sudo zypper help modifyrepo`。

### zypper 配置

Zypper 现在附带一个配置文件，允许你永久更改 Zypper 的行为（系统范围或用户特定）。 对于系统范围的更改，编辑 `/etc/zypp/zypper.conf`。对于特定于用户的更改，请编辑 `~/.zypper.conf`。如果 `~/.zypper.conf` 尚不存在，你可以使用 `/etc/zypp/zypper.conf` 作为模板，将其复制到 `~/.zypper.conf` 并根据自己的喜好进行调整。 有关可用选项的帮助，请参阅文件中的注释。

### 更多信息

更多信息详见 `zypper help` 和 `zypper help COMMAND` 或者 `man zypper(8)`

- https://en.opensuse.org/SDB:Zypper_usage
- https://en.opensuse.org/openSUSE:Zypper_versions