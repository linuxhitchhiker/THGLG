---
title: "使用 systemctl 管理服务"
---

## 简介

`systemd` 是一个 Linux 系统基础组件的集合，提供了一个系统和服务管理器，运行为 `PID 1` 并负责启动其它程序。其功能包括：支持并行化任务、按需启动守护进程、监视进程、支持快照和系统恢复、维护挂载点和自动挂载点等[^1]。

## 基本工具

监视和控制 systemd 的主要命令是 `systemctl`。该命令可用于查看系统状态和管理系统及服务。详见 `man systemctl`。



[^1]: 本文的大部分内容参考 [systemd (简体中文) -- ArchLinux Wiki](https://wiki.archlinux.org/title/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))