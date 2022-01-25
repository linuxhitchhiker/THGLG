---
title: "管理运行进程"
---

# 管理运行进程

## 理解进程

Linux 是一个多用户系统，支持许多程序同时运行。

进程（process）是命令的运行实例。例如，系统上可能有一个 `nano` 命令。但如果 `nano` 当前由 15 个不同的用户运行，则该命令由 15 个不同的运行进程表示。

每一个的进程都会有一个独一无二的 PID（进程标识符，process ID），Linux 使用 PID 识别进程，并将同一程序的不同进程进行区分。当进程结束后，PID 就会被系统回收，分配给新的进程。

除了 PID，一个进程还会具有其他的属性，如，进程所属的用户和用户组，这将决定系统如何为一个进程分配系统资源。管理进程是 Linux 系统管理员的重要技能之一。

## 列举进程

### 使用 ps 列出进程

在命令行界面中，最常用于列出运行进程的命令行工具是 `ps`。使用该命令即可查看正在运行的进程。

```
bh@localhost:~> ps u
USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
bh         2400  0.0  0.1   9968  6372 pts/1    Ss   15:55   0:00 /bin/bash
bh         2447  100  0.0  10520  3676 pts/1    R+   15:55   0:00 ps u
```

如上，`u` 或 `-u` 选项用于显示用户名和其他信息，如进程开始的时间、与归属于当前用户的进程的 CPU 和内存使用情况。上述显示的进程均和当前的终端（`tty1`）关联在一起。在图形化界面未发明之前，人们都是通过字符终端控制系统，一个终端通常就代表一个用户。如今，通过在桌面上打开多个虚拟终端或终端窗口，你可以在一个屏幕上拥有多个“终端”。如上终端设备 `tty1` 正在用于登录会话。

`USER` 列显示了启动该进程的用户名。`PID` 列显示进程的 PID。你可以通过将 PID 作为参数指定进程管理命令对使用该 PID 的进程发送相关的信号（如，重启、结束或挂起）。`%CPU` 和 `%MEM` 列显示了进程使用的 CPU 资源和 RAM 资源（按百分比计算）。

`VSZ`（虚拟集大小）显示图像进程（image process）的大小（以千字节 kb 为单位），`RSS`（驻留集大小）显示进程占用物理内存的大小。`VSZ` 和 `RSS` 的大小可能不同，因为 `VSZ` 是为进程分配的内存量，而 `RSS` 是实际使用的内存量。`RSS` 内存表示不能交换的物理内存。

`STAT` 列代表了进程的状态，`R` 表示正在运行，`S` 表示该进程已经睡眠。`START` 显示了进程开始运行的时间，`TIME` 显示进程累积使用的系统时间（许多命令消耗的 CPU 时间非常短暂，所以 TIME 为 00:00）。

除了以上的这些进程，Linux 系统还有很多不关联终端的进程。这些在后台运行的进程处理着大量事务（比如发现新设备、启动时唤醒图形界面和管理系统资源）。它们随着系统的启动而运行，随着系统关闭或用户注销（部分后台进程不会因为用户注销而停止）而停止。

要以当前用户的身份查看 Linux 系统上运行的所有进程，键入：

```
$ ps ux | less
```

要查看所有的进程，键入：

```
$ ps aux | less
```

你可以使用 `-o` 选项和 `--sort` 选项对 ps 的输出结果进行修改和排序。如：

```
bh@localhost:~> ps -eo pid,user,uid,group,gid,vsz,rss,comm | less
   PID USER       UID GROUP      GID    VSZ   RSS COMMAND
     1 root         0 root         0 167048 14080 systemd
     2 root         0 root         0      0     0 kthreadd
     3 root         0 root         0      0     0 rcu_gp
     4 root         0 root         0      0     0 rcu_par_gp
     6 root         0 root         0      0     0 kworker/0:0H-events_highpri
... ...
bh@localhost:~> ps -eo pid,user,group,gid,vsz,rss,comm --sort=-vsz | head
   PID USER     GROUP      GID    VSZ   RSS COMMAND
  1543 bh       bh        1000 268746444 32796 baloo_file
  1773 bh       bh        1000 25530864 191624 cfw
  1577 bh       bh        1000 21425924 152472 cfw
... ...
```

如上，`-e` 选项能列出全部的进程，`--sort=-vsz` 选项将输出按 `VSZ` 进行降序排列。

是不是看着很繁琐，且你无法查看实时运行情况？

### 使用 top 列出和更改进程