---
title: Ubuntu16.04 双系统双硬盘安装
date: 2020-05-23 19:12:13
tags: [Ubuntu,Linux]
---

在网络上各种过时教程中摸索出来的成功安装Ubuntu16.04的方法，为了以防自己忘了怎么装双系统，又瞎Google百度CSDN，一顿操作之后还得按电源键重启，还是记录一下安装过程吧。

安装的机型为2018款LG Gram14，没有独立显卡

## 准备工作

- [Rufus](https://rufus.ie/) 用于制作Ubuntu的启动盘
- [Ubuntu16.04镜像](https://releases.ubuntu.com/)
- 一个容量大于4GB的U盘
- 磁盘管理中将按照自己所需，选中还有空余空间的卷，压缩卷，自己分配合适空间，注意不要格式化新的卷。
- Windows电源设置中关闭快速启动

## 制作Ubuntu启动盘

Rufus 是一个可以帮助格式化和创建可引导USB闪存盘的工具，比如 USB 随身碟，记忆棒等等。

在如下场景中会非常有用：

- 你需要把一些可引导的ISO格式的镜像（Windows，Linux，UEFI等）创建成USB安装盘的时候
- 你需要使用一个还没有安装操作系统的设备的时候
- 你需要从DOS系统刷写BIOS或者其他固件的时候
- 你需要运行一个非常底层的工具的时候

这里，我们就需要将下载下来的Ubuntu镜像通过Rufus创建USB安装盘。

![Rufus](/img/Rufus.png)

点击选择来选择需要使用的iso镜像文件，分区类型选择GPT使启动盘可以被UEFI识别，其余默认或者如图这样设置即可。

插入安装盘重启

## Bios设置

 	笔者的Gram为开机时出现LG的Logo时，按下F2进入Bios

1. 关闭Secure boot

2. 开启/选用UEFI模式

3. Boot启动优先顺序，将U盘的优先级置于最高

   （开机时Gram按F10可选择启动项）

4. F10保存配置并退出

如果没有大碍，这里再次重启时应该会载入启动盘的Ubuntu安装引导界面。

## Ubuntu的安装

笔者这里是双硬盘，一块硬盘安装Windows 10，一块硬盘安装Ubuntu16.04。

这里的界面应该识别出Windows Boot Manager

1. 进入安装界面时，不要点有关联网的选项，不然可能拖慢安装速度
2. 到分区的时候，选中自己分配出来的空闲的卷，添加swap, / ,/home分区，均为逻辑分区（好像主分区也问题不大），一般swap分区大小为内存的两倍（内存够大也可以不分swap），/分区类似Windows的C盘，大概分10-20GB.剩下的空间留给/home
3. 启动引导程序选择Windows Boot Manager所在的分区
4. 等待Ubuntu安装程序，泡杯卡布奇诺休息一下

## 尾声

安装完之后重启应该是进入到Ubuntu的启动项可选择Ubuntu或者Windows Boot Manager，即进入Windows，到这里安装应该是完成了。