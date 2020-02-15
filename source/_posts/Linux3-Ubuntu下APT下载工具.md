---
title: Linux3-Ubuntu下APT下载工具
date: 2019-11-24 22:42:00
tags:
- Linux

categories:
- Embedded system
---

# APT下载工具简介
Ubuntu下我们常使用的下载工具就是：APT下载工具，APT 下载工具可以实现软件自动下载、配置、安装二进制或者源码的功能。 APT 下载工具和我们前面讲解的“install”命令结合在一起构成了 Ubuntu 下最常用的下载和安装软件方法。它解决了 Linux 平台下一安装软件的一个缺陷，即软件之间相互依赖。
APT 采用的 C/S 模式，也就是客户端/服务器模式，我们的 PC 机作为客户端，当需要下载软件的时候就向服务器请求，因此我们需要知道服务器的地址，也叫做安装源或者更新源。

## 1.更新本地数据库
如果想查看本地哪些软件可以更新的话可以使用如下命令：

```
sudo apt-get update
```



## 2.检查依赖关系
有时候本地某些软件可能存在依赖关系，所谓依赖关系就是 A 软件依赖于 B 软件。通过如下命令可以查看依赖关系，如果存在依赖关系的话 APT 会提出解决方案：

```
sudo apt-get check
```
## 3.软件安装
软件安装使用如下命令：
```
sudo apt-get install package-name
```
可以看出上述命令是由“apt-get”和“install”组合在一起的，“package-name”就是要安装的软件名字，“apt-get”负责下载软件，“install”负责安装软件。比如我们要安装软件 Ubuntu 下的串口工具“minicom”，我们就可以使用如下命令：
```
sudo apt-get install minicom
```
执行以上命令以后就会自动下载和安装minicom软件。

安装 minicom 这个软件的过程，会有如下所示询问：
```
您希望继续执行吗？ [Y/n]
```
如果希望继续执行的话就输入 y，如果不希望继续执行的话就输入 n。安装完成以后我们直接在终端输入如下命令打开 minicom 这个串口软件：
```
minicom -s
```
关于 minicom 的使用大家可以上网搜索一下，这里就不详细讲解了，要退出 minicom 可以直接按下 ESC 键。

## 4.软件更新
更新软件的话使用如下命令：
```
sudo apt-get upgrade package-name
```
其中 package-name 为要升级的软件名字，比如我们升级刚刚安装的 minicom 这个软件，输入如下命令：
```
sudo apt-get upgrade minicom
```

## 5.卸载软件
卸载软件使用如下命令：
```
sudo apt-get remove package-name
```
其中package-name是要卸载的软件，比如卸载前面安装的minicom软件。



以上为Ubuntu下的APT下载工具的大部分使用命令了。




