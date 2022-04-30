---
#template: home.html
title: 欢迎
toc_depth: 0
---

<script type="text/javascript">
    (function(){
    t = document.getElementsByClassName("md-sidebar__inner");
    t[1].innerHTML="";
    t[0].innerHTML="";
    })();
</script>

<style>
    @media screen and (min-width: 60em) {
        .md-sidebar {
            //display: none !important;
        }
    }
    .headerlink {
        display: none !important;
    }
    .feat-block {
        /* display: none; */
        clear:both;
        text-align: center;
        padding: 1em 0em 1em 0em; 
    }
    .feat-head {
        text-align: center;
    }
    .md-content__button {
        display: none;
    }
    @media screen and (min-width: 60em) {
        .feat-block img {
            max-width: 240px;
            max-height: 160px;
            }
        .feat-block--left img {
            float:left;
            margin: 0em 1em 0em 0em;
            }
        .feat-block--right img {
            float:right;
            margin: 0em 0em 0em 1em;
            }
    }
</style>

<div markdown class="feat-head">

# Linux 银河漫游指南

面向普通桌面用户的、开源的、人类可读的 Linux 桌面文档。

<div markdown>

[开始阅读](intro.md){ .md-button  .md-button--primary }

</div>

以 CC-BY-SA 协议开源于 GitHub。

</div>

---

!!! bug
    您阅读是文档的早期版本，本文档还在建设当中，许多内容并不完全，敬请留意。

<div markdown class="feat-block feat-block--left">

![Image title](assets/images/Freedesktop-logo-for-template.svg)

## 符合标准

Linux 桌面以 Freedesktop.Org 标准为核心，所有的桌面环境都在这一标准下工作。跟随这一标准能让我们惠及更多用户。

</div>

<div markdown class="feat-block feat-block--right">

![Image title](assets/images/Distro.webp)

## 跨发行版

统一的、通用的文档在一定程度上可以广泛适用于遵循 Freedesktop.Org 标准的 Linux 桌面。

</div>

<div markdown class="feat-block feat-block--left">

![Image title](assets/images/Flatpak-truck.webp)

## 容器化

Flatpak、Toolbx 等容器化技术弱化了发行版之间的鸿沟，为应用程序提供一定程度上的隔离与防护，从而限制第三方或闭源应用的行为。

</div>

<div markdown class="feat-block feat-block--right">

![Linux DE](assets/images/linux-de.webp)

## 易于理解

本文档面向所有桌面用户，致力于提高可读性与可操作性，以降低 Linux 桌面使用门槛。

</div>

<div markdown class="feat-block feat-block--left">

## 实用主义

与各发行版的 Wiki 不同，我们不会把讨论技术细节作为重点，而是强调过程与结果，最终使普通 Linux 桌面用户获益。

</div>

<div markdown class="feat-block feat-block--right">

## 真正开源

本文档采用 CC-BY-SA 开源协议发布。

</div>
