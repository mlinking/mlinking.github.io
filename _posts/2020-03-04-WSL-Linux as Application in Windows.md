---
title: Windows 里的Linux 程序
date: 2020-03-04 03:00:00
categories:
- Windows 技巧
- Linux as application in Windows
tags:
- Ubuntu
- WSL
published: false
typora-root-url: ../../mlinking.github.io
---

最近几天在尝试使用Markdown 编写书籍 - 参看[`记录：筛选写书工具的艰苦经历`](http://www.kukoo.online/2020-03/Slashie-My-experience-to-produce-e-books/)，找到的一些Markdown 书籍的例子基本上都是基于 Linux 调试的：本想在Windows 10 上来支持Linux 的那些指令，没有成功。有趣的是，知道Windows 10 现在支持 Linux 作为一个 Windows 的应用(不是笨重的双系统)，虽然最后还是放弃了(实在是繁琐)，将那些经历记录下来也不错。

\*: 不过，*现在 Docker 这么火，Windows 也支持，所以，基于 Docker 的Linux 完成调试应该是不错的*

# Windows 10 支持 Linux 作为一个应用啦



## 修改Windows 10 中的配置

![](/../imagesforCOSLater/WLS/WLS-DeveloperMode.png)

![](/../imagesforCOSLater/WLS/WLS-WindowsFeatures.png)

![](/../imagesforCOSLater/WLS/WLS-WindowsFeatures2.png)

![](/../imagesforCOSLater/WLS/WLS-WindowsFeatures3.png)




## 在 微软商店中安装 Ubuntu

![](/../imagesforCOSLater/WLS/WLS-Ubuntu1.png)

![](/../imagesforCOSLater/WLS/WLS-Ubuntu2.png)



## 剩下的就跟使用Linux 一样了



### 一定要设置国内的 Ubuntu 备份！否则，网速太受限！

因为Linux子系统的apt源使用的是官方源，需要连接到国外的服务器。所以安装一些软件时下载会很慢，我们可以改用国内的镜像apt源。 国内的镜像源主要有：

- 阿里源

```cpp
deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse 
deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
```

- 科大源

```cpp
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
```

- 网易源

```cpp
deb http://mirrors.163.com/ubuntu/ wily main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ wily-security main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ wily-updates main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ wily-proposed main restricted universe multiverse
deb http://mirrors.163.com/ubuntu/ wily-backports main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ wily main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ wily-security main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ wily-updates main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ wily-proposed main restricted universe multiverse
deb-src http://mirrors.163.com/ubuntu/ wily-backports main restricted universe multiverse
```

可以直接使用vim对 /etc/apt/sources.list文件进行修改。
 先进行一下备份。

```cpp
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

然后

```cpp
sudo vim  /etc/apt/sources.list
```
加到文件最前面或直接替换掉原文件。
保存后运行
```csharp
sudo apt-get update
```

### 安装 TexLive

![](/../imagesforCOSLater/WLS/WLS-TexLive.png)

![](/../imagesforCOSLater/WLS/WLS-TexLive2.png)

### 甚至可以安装可视化

参看[2]

# 基于WLS 的Ubuntu 自制 Markdown 书

以后再说吧



# 删除也很简单

因为WLS安装的Ubuntu就像Windows 中的一个应用，卸载它也就像卸载一个应用一眼搞得。



# 慎重起见，别忘了将之前的配置恢复



# 参考资料

1. `https://www.windowscentral.com/install-windows-subsystem-linux-windows-10`
2. [史上最全win10下Linux子系统的安装及优化方案] `https://www.jianshu.com/p/dc32a75e2de4`
3. `https://www.cnblogs.com/Jimc/p/10214081.html`
4. [gnuwin32]`https://sourceforge.mirrorservice.org/g/gn/gnuwin32/`
5. [markdown一步生成电子书: 支持PDF、Mobi、EPUB格式] `https://github.com/phodal/ebook-boilerplate`
6. [GitHub 漫游指南] `https://github.com/phodal/github`








