---
title: 商务视角下的数据分析概览
date: 2020-07-12 02:00:00
categories:
- 商务视角下的数据分析
- 原创
- 写书吧
tags:
- 写书吧
- 商务思维
- 数据分析
- 贯通与综合
- 计算广告
- 机器学习
- 人工智能
- 长尾理论
published: true
typora-root-url: ../../mlinking.github.io
---

这学期的"数据分析"课结束了，对"商务视角下的数据分析"的内容又有了新的梳理，在此记录下。

# 商务视角下的数据分析

## 简介

不管是就业还是创业，商务思维对于学生都是非常总要和必要的：就业在公司，职位提升自是你应追求的，而想要提升，单纯技术是不够的；如果创业，不懂商务思维更是凶多吉少 - 据统计，90%以上的创业都是失败的。

![MassEntIno](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/DataAnalyticswithBusiness/MassEntIno.png)

而围绕商务，还是一个很有意义的串接相关数据分析方法的线索，此所以在建设此课程是本人冠之以"商务视角下"的原因。

## Part I: 商务视角篇

### 商务视角概述 – 盈利是核心

商务思维？推荐"褚时健传"读一读，可以通过这本书体会下商务思维并不复杂(了解下这位老人的传奇经历也是会有收获的)。

![CHUShiJian](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/DataAnalyticswithBusiness/CHUShiJian.png)

关于商务思维的总结，可能大家都会想到所谓的MBA (即工商管理硕士，Master of Business Administration)，甚或 EMPA (Executive Master of Public Administration)之类。确实，它们汇总了围绕商务或公共事务管理所需要的决策制定的经验总结(此外还包含限制的内容 - 法律法规，以及职业道德等)，了解一下是会有收获的。不过，终究MBA还是EPMA都是很高大上的 - 毕竟有逼格才能吸引人嘛，课程的数目是很多的！

有感于理解和活用商务思维，跟是否学习过MBA或EMPA没有必然的联系，所以，在本课程中对相关的概念和技巧做简单的提炼，分成两个部分：

- 盈利的简要评估
- 盈利的保障手段

> 怀念 褚时健 老人
>
> ![MissingCHUShiJian](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/DataAnalyticswithBusiness/MissingCHUShiJian.png)

围绕商务，有几个重要的
- 三链分析：生产链，客户链和
- 三张表：资产负债，利润表和现金流量表

### 盈利如何评估

很多指标可用于评估商务的盈利性，此处只是简单地技术：
- 时间价值
- 投资与产出的量与时
- 销售平衡点 

### 盈利如何保障

- 战略



## Part II: 数据分析的历史，优化论和统计学

### 数据分析的历史 – 追寻智慧

![WisdomHis](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/DataAnalyticswithBusiness/WisdomHis.png)

即便是褚时健老人，在管理他所经手的那些企业的时候，也是要做很多数据分析以支持商务决策的，基本的就是利润和成本核算。数据分析往大里说，可体现为人类追寻智慧的过程，简单梳理为三个阶段：

- 计算机出现之前 - 哲学或者说数学，是人这一主体实现思考和计算验证
- 计算机出现之后 到目前为止(应该也包含不短的一段未来时间) - 人这一主体思考，而计算机完成计算验证。集中的体现是AI (Artificial Intelligence, 人工智能)，也有三个发展阶段
  - 早期的逻辑推断(LI - Logic Inference)
  - 其后的知识工程或专家系统 (KE/ES - Knowledge Engineering/Expert System)
  - 当下的机器学习(ML - Machine Learning)
- 未来？ - 机器也能思考？还是人类大脑深度开发？个人觉得生化人是个无奈的选择

![Borg](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/DataAnalyticswithBusiness/Borg.jpg)

### 一点优化论

在进入机器学习阶段，所谓的学习，其实就是人们设定模型结构，然后喂之以数据以得到**最佳的**模型结构的参数。最佳，也就意味着优化，所以，了解下优化有关的概念和技术是有必要的。

> 虽然"**凸优化**"是一个重要的寻求最佳参数的方式，但是，也要记住还有很多优化的方式是被归纳为"**运筹学**" 领域的，甚至，有两个国际的奖项：
>
> ![OptimizationPrizes](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/DataAnalyticswithBusiness/OptimizationPrizes.png)

### 统计学 – 基于分布的推断是核心
在商务决策的方法中，很多的概念和技术是归纳在统计学里的。而统计学的基本内容有两个方面：基于样本估计总体的分布；基于分布进行推断。其核心的计算是基于分布得到所谓的置信区间。

> "多元统计分析" 和 "多元变量分析" 也值得去了解一下
>
> 再就是可以扩展看看 "计量经济学"

## Part III: 数据分析概览 

### 基础篇
- 基础思想 - 距离，空间 和 隐含量 (EM方法)
- 聚类 - K-means 和 DBScan 
- 关联规则 - Apriori 算法
- 分类 之 决策树, … 
- 神经网络 之 早期

### 深入篇

- 聚类 之 GMM/EM
- 分类 之 SVM
- 神经网络 之 Deep Learning
- 强化学习 - MDP, 和 RL

### 大规模篇
- 从von Neumann 计算机到超级计算机 (MPP 和 Cluster)
- 数据管理工具演化: 从File 到 Big Data
- 并行算法
- 大数据

## Part IV: 创业篇

### 互联网+ 和 长尾

时代发展到现在，互联网已经成为吸纳全球人口的媒介，也因此，借助互联网改造甚或创造新的经济运作方式，已成为广泛的共识。涌现出大量的成功的模式，如Google，FaceBook, Twitter，Tencent，Amazon, Alibaba, 京东，拼多多等。

在中国，体现为2015年国务院总理[李克强](https://zh.wikipedia.org/wiki/李克强)率先提出的“互联网+”。

集中在电子商务(按现在的理解，也就是"互联网+商务")，亚马逊，阿里巴巴，京东等令人羡慕，也因此有学者对这类公司的成功做了分析和总结，比较有意思的是所谓的长尾理论的解释。

![LongTail](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/DataAnalyticswithBusiness/LongTail.png)

> 网络公司的员工，现在有35岁天花板的无奈；但是，因为他们有大规模数据处理的实践经验，所以，一个比较好的出路就是进入国有大公司，因为，SOE往往需要大数据处理但是缺乏技术积累。

### 计算广告那点事

不管在什么时代，盈利模式是公司的核心价值。在互联网+时代，计算广告是必要的：长尾理论的一个分析那些公司能够成功的一个因素就是，它们能够向巨量的用户提供近乎无限的商品，那么，就需要在二者之间提供精准匹配的机制。这里面涉及到的算法也是很多的，值得去了解一下。

![ComputingAdv](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/DataAnalyticswithBusiness/ComputingAdv.png)

### 创业吧

- 企划书和公司申请
- 借助网络就可以开公司

![gs.aliyun.com](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/DataAnalyticswithBusiness/gs.aliyun.com.png)

## 几本书

- 褚时健传
- *八次危机*
- The Personal MBA: Master the Art of Business (在家就能读MBA) by Josh Kaufman
- Statistical Methods for the Social Sciences (4th ed) by Alan Agresti, Barbara Finlay
- *计量经济学*
- *Artificial Intelligence: A modern approach by Stuart Russell, Peter Norvig*
- *Convex Optimization by Stephen Boyd and Lieven Vandenberghe*
- *运筹学*
- 统计学习方法
- *Introduction to Data Mining By Pang-Ning Tan, Michael Steinbach, Vipin Kumar*
- *Deep Learning by Ian Goodfellow, Yoshua Bengio, Aaron Courville*
- 并行算法设计
- *科学计算*
- *CUDA编程*
- 大数据
- 长尾理论
- *推荐系统实践*
- 深度学习和推荐系统
- 项目融资商业计划书（2014版）编制技巧及重点说明

## 几个视频

- 早期Andrew Ng 的"机器学习"课程录像(时间长)
- 陆吾生先生的优化论视频
- "凸优化"的视频(很难懂)
- 一些培训机构的机器学习视频：七月邹博的(后来换了单位) 
