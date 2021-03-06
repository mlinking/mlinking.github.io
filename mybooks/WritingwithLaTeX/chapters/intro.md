---
title: 导读
date: 2020-03-05 04:00:00
categories:
- Operating System
tags:
- Operating System
published: true
---

# 导读

> 操作系统(OS: Operating System)，编译原理(Compiler Theory)，数据库管理系统(DBMS: Database Management System)，现在还要再加上大数据(Big Data)生态软件(Hadoop, Spark等)，它们的设计与实现，是所有想提升自己编程能力的人都应该好好学习的。
>
> -- 著者言

身处IT时代，计算机所代表的那堆硬件（打印机，摄像头，网络等）是必不可少的，而想要使用那些硬件，就需要操作系统。也因为操作系统如此重要，所以，关于它的概念和技术的书已经很多了！那么，为什么还要写一本呢？“极简”便是了。

> 单一功能的操作系统不在此列，如嵌入式操作系统

## 现代操作系统的挑战

凡是使用过计算机的人，都知道操作系统的重要性：没有它，你根本不能使用那些硬件设备。

那就直接切入正题，先了解下现代操作系统的核心功能。其实，很简单明了，那就是“**以有限的资源支持多道程序进程的并发运行**”。

所谓的有限资源，就是冯•诺依曼架构[[1\]](#_ftn1)：一个CPU (中央处理单元：Central Processing Unit)，有限的内存空间，和有限的外存空间。

所谓的多道程序/进程(Stored Programs)，和并发运行(Concurent Execution)，单纯看书面的定义，有些雾里看花。在这里先给出一个现在使用Windows 操作系统都熟悉的场景，即，**似乎计算机“同时”在运行多个程序**：你在听着从计算机中传来的好定的音乐，同时，你编好的程序正在完成者复杂的运算，而在程序运行的同时你想着编辑下要发表的论文，甚至还可以在看个技术视频。图 0‑1就是本人使用笔记本的一个截图，能看出来有很多在运行的程序。

![似乎计算机“同时”在运行多个程序](D:\MyGitbook\imagesforCOSLater\AShortOS\intro-SnapshotofManyP.png)

这背后的支撑概念就是多道程序/进程和并发运行。所谓多道程序/进程是指在内存中可以存放多个程序的代码(或片段)，以及程序执行所需要的资源信息。而并发运行，是在多道程序/进程的基础上，这些程序能够在一个CPU上快速切换，看上去它们是在同时运行。

一方面是有限的资源，另一方面是要支持很多程序的并发运行，这就存在着资源紧缺的挑战，主要分为如下三种情况：

**单一资源**的竞争：

1. CPU - 一个 CPU 和 多程序运行的矛盾

在冯•诺依曼架构中有云，CPU是程序指令执行的核心部件，也就是说，你的程序最终是在CPU中逐条指令执行的。那么，前面的场景中似乎同时运行着多个程序的效果，就在于CPU可以在多个相关程序(也包括操作系统内部的程序)间快速进行切换。想要了解如何切换，就需要计算机架构的知识；而选择哪个程序获得CPU以执行其指令，则是操作系统关注的内容。对此进行阐述的章节是第 1 章。

2. 内存 - 小内存 和 大程序的矛盾

现在流行的内存大小是8GB (1GB = 230Bytes)，可很多程序的尺寸都比8GB大。我的小侄子喜欢的刺客信条(Assassin's Creed)游戏的大小就比8GB大，但是，我仍然可以运行它；即便是高等级的服务器，虽然可能配备大容量的内存，可是，在同时给很多用户提供服务的时候，并发运行的多个程序的大小也很容易超过内存的大小。这就是“小内存 v.s 大程序”的矛盾。

3. 可虚拟化的资源 – 如SPOOLING技术

按照这种方式使用的资源的例子就是打印机。有些计算机系统会作为服务器想很多用户提供服务 – 计算，和打印等。如果该计算机只连接有一台打印机，而同时有多个用户想打印资料，此时，每一个用户绝对不希望TA打印出来的资料里夹杂有别人的东西，即打印被别人中断。那么，这就会导致排在后面的只能等待，这就造成了巨大的浪费。SPOOLING(外部设备联机并行操作，Simultaneous Peripheral Operations On-Line)技术就是针对此问题的解决方案。参见后面0.2的简述。

需要说明的是，SPOOLING技术背后隐藏的编程思想，即将资源虚拟化以对多应用提供服务的方式，在软件开发，尤其是高性能服务软件的开发，有着广泛的应用，如邮件服务系统，消息队列系统等。

 

**协作中的Broker资源**的竞争：

4. 协作中的Broker资源

在现代操作系统中，进程间的协作还是比较常见的，如IPC(Inter-Process Communication)机制。即便是在SPOOLING也需要这样的技术，即SPOOLING Daemon 程序需要借助暂存接受到的来自多个应用的打印任务，然后将它们逐个打印。这里的“暂存”可算是Broker资源，其使用需要遵循一定的规则。

![](D:\MyGitbook\imagesforCOSLater\AShortOS\OS-DataInconsistency1.png)

![程序协同带来的数据不一致性风险](D:\MyGitbook\imagesforCOSLater\AShortOS\OS-DataInconsistency2.png)

还有一个例子就是银行系统中的共享账号这样的Broker资源。上图给出了使用这种资源的一种风险情况，图中有两个角色 – Son 和 Papa，他们共享一个银行账号((a)中标注了100)。(b) 表示某一时刻Son和Papa都想向这一账号存钱，为此，他们需要读取当前账号中的钱数到他们各自的空间；(c) 和(d)展示了Son 完成存钱50并写回账号的过程，更新后的账号钱数是150；(e)和(f)展示了Papa存100元进账号的过程，这一过程是在Son操作之后完成的，所以，账号的钱数是200元。可是，Son 和 Papa一共存了150，共享账号正确的结果应该是250,。这就是数据不一致性的风险。



**有限资源分配**的风险：

5. 死锁

![资源分配不当就会造成所谓的死锁现象](D:\MyGitbook\imagesforCOSLater\AShortOS\OS-Deadlock.png)







此外，现代操作系统还需要考虑很多其他的挑战，如安全，GUI(Graphic User Interface)，网络，甚或对分布式的支持。不过这些就不在此“精简”版本中覆盖了。





------

[[1\]](#_ftnref1) [https://zh.wikipedia.org/zh-hans/冯•诺伊曼结构](https://zh.wikipedia.org/zh-hans/冯·诺伊曼结构)



