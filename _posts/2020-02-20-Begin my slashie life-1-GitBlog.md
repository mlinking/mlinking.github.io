---
title: 基于Github搭建自己的博客
date: 2020-02-20 01:00:00
categories:
- 原创
- 实用技巧
- Github
- 自媒体生活
- 斜杠生活
tags:
- 自媒体
- 博客
- Github
- Emoji
- Markdown
- Typora
published: true
---

# 简单粗暴的方法构建Github 博客

网上浏览过很多关于如何基于Github搭建自己的博客的文章(比较知名的就是2012年[阮一峰的那篇](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)了)，陆陆续续看下来，总是不太满意：还是有些麻烦！`是的，虽然有很多模板，但是，很多时候还是需要自己仔细地集成不同的样式`前天看到一个比较满意的基于Github的博客(再次感谢"[青柠学术](https://iseex.github.io/)")：基于Jekyll 的Next模板。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/iseex.png)

想着，自己的博客如果是这样也不错。

想着，既然Github支持Reposityory 的Fork，那么，我应该可以在Fork之后直接基于TA的文档修改即可：`避免了耗时的细致配置，不过，也降低了学习的乐趣`。**以后如有需要再学习吧：个人体会，很快就有一个原型，会大大提升自己学习的兴趣的**

试了下，是可行的，简记如下。

## Fork "[青柠学术](https://iseex.github.io/)"的Repository

不赘述。

## 将Fork来的Repository 重命名为`xxx.github.io`

其中的 `xxx`是你的Github 的用户名 - 这是Github的规定。

前面的"[青柠学术](https://iseex.github.io/)"的博客访问路径就是如此。

## 等一会，就可以按照`https://xxx.github.io`来访问你的博客了 - 完全与Forked 一样

很简单吧？！就是这么粗暴:jack_o_lantern:

## 如何修改呢？ - Github Desktop 即可

自己的博客跟别人的一样自然是不允许的！如何修改呢？网上很多资料都要是有 Github 的 Cli 方式 - 命令行呢！不过，人家也提供了Desktop 版，为什么不用呢？

### Github Desktop 的下载与安装请自行检索

### 将 `xxx.github.io`克隆(Clone)至本地

![克隆至本地](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/GithubDesktop-Clone.png)


### 使用你喜欢的MD编辑器 - 我喜欢 [Typora](https://www.typora.io/):`所见即所得嘛`

![Typora 是所见即所得的MD编辑器](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Typora-WYSWYG.png)

想要查看MD 的源代码也很简单 - `Ctrl+/`即可。

![在Typora中查看MD源代码也很简单](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Typora-MDSrCode.png)

**更详细的完善技巧请参看后面的[完善博客的一些技巧](#完善博客的一些技巧)**。

### 本地的任何修改都会在Desktop 中体现

![本地的所有变化都会在Desktop有体现](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/GithubDesktop-Changes.png)

### 一定要注意！同步至Github需要两步！！

在完成了本地的修改后，自然需要同步至你的Github网站。不过，要小心，使用Desktop 进行同步需要两步：

1. `Commit to master` 只是将修改在本地做了更新

![`Commit to master` 只是将修改在本地做了更新](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Typora-CommitToMaster.png)

2. 只有运行`Repository ->Push`才最终同步至Github

![只有运行`Repository ->Push`才最终同步至Github](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Typora-Push.png)

## 遇到改错了怎么办？

我就有这样的经历：在本地使用微软的`笔记本`修改了`_config.yml`，应该是`笔记本`修改了编码格式，当同步后，Github 的`xxx.github.io` 的Repository 会显示有一个Build 错误，并提示是哪个文件。还是很让人害怕的：毕竟只是`简单粗暴`地使用了别人的样例构建的博客。

好在Github提供的历史版本，即`History`那个按钮，点击后会显示`xxx.github.io`中所有文件的历史版本。挑一个`Verified`的历史版本下载下来，然后将不通过的删除掉，在将旧的替换上即可。当然，希望你修改的不多 :smile:

# 完善博客的一些技巧



## Markdown - 基础的就不提了，网上很多

### 页内跳转链接 

Markdown会自动给每一个h1~h6标题生成一个锚，其id就是标题内容。目录树中的每一项都是一个跳转链接，点击后就会跳转到其对应的锚点（即标题所在位置）。

如果需要在目录树之外还要增加跳转到某个标题的链接，可以 `使用Markdown的语法来增加跳转链接：“[名称](#id)”`。

其中的`名称`可以随便填写，`id`需要填写跳转到的标题的内容。

例如，如果想要增加一个到本文档`简单粗暴的方法构建Github 博客`标题的跳转链接，则需要这么写：

`[使用Markdown语法增加的跳转到“简单粗暴的方法构建Github 博客”的链接](#简单粗暴的方法构建Github 博客)`

效果：

[使用Markdown语法增加的跳转到“简单粗暴的方法构建Github 博客”的链接](#简单粗暴的方法构建Github 博客)

### 使用第三方存储保存图片 - (参看[分发](http://www.kukoo.online/2020-02/Begin-my-slashie-life-3-FenFa/))

### 插入数学公式 -  (参看[分发](http://www.kukoo.online/2020-02/Begin-my-slashie-life-3-FenFa/))


## [EMOJI](https://www.webfx.com/tools/emoji-cheat-sheet/)

有了emoji，大大增加了网页的趣味，自然也是很多使用MD的平台所支持的。

将对应emoji表情的符号码复制后输入你的Markdown文本即可显示emoji表情。 如`:blush:`，显示为:blush:

> 甚至有基于EMOJI的研究论文呢！[网文来源](https://2018yfb1004800.cn/new/meetings-2019-5-18/)
>
> > 2019年5月17日下午，在美国旧金山举行的第28届国际万维网大会会议（World Wide Web，简称WWW）上，项目组成员陈震鹏为第一作者的论文“基于互联网普适语言“绘文字”的跨语言情感分析表征学习方法 (Emoji-Powered Representation Learning for Cross-Lingual Sentiment Classification)”获得了最佳论文奖。
> >
> > > WWW大会是计算机和互联网领域历史最为悠久同时也最为权威的顶级学术会议之一，被中国计算机学会列为A类推荐学术会议

## 使用Gitalk 评论

注意到`_config.yml`配置文件中是包含此选项的，但是，在ISEEX 中是关闭了。打开即可

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Gitalk.png)

需要自己去Gitalk 网站申请账号，将获得的`ClientID`和`ClientSecret`填上即可。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Gitalk-OAuth.png)

不过，在Github重新编译后，访问页面遇到了一个小错误：

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Gitalk-Err.png)

解决办法也简单，就是在`xxx.github.io`的`Settings`中将`Issues` 项选中即可

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Gitalk-Issues.png)

## 拼音声调

在网上浏览网文，有时候会遇到不会发音的字，自然希望有拼音就好了。例如`{魑魅魍魉|Chī Mèi Wǎng Liǎng}`

如果你用的是搜狗拼音输入法、智能ABC输入法、中文全拼输入法和双拼输入法，一般都会有一个软键盘，用鼠标点右键单击软键盘，就会出现一个对话框，然后找到`拼音字母`一栏，再用鼠标点左键单击`拼音字母`将其打开即可执行。

![点击小键盘，选择`特殊符号`](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Pinyin-Sogo.png)

![里面有很多选择 - 包括`拼音`](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Pinyin-Sogo2.png)

# 还是需要个域名吧 - 便于`记忆+纪念` - 万网

学习了网络课程的人，都知道域名的重要性。现在申请一个域名还是很便利的 - 阿里系的万网，和腾讯云 都支持域名：当然，都是要收费的！

## 在万网购买域名服务 - 设计个有趣又价格低的域名

我的是`kukoo.online`：`kukoo`来自家里的小东西特别喜欢学`布谷鸟`的叫声，可惜在`万网`上查`Cuckoo`，已经有注册了，还挺贵。所以，自己设计了谐音的域名:hatched_chick:

## 设定域名解析 - 一个域名可以有多个解析 - 不要浪费了

在万网同意了你的域名申请后(还是很快的 - 不到一天就回复了)，就需要基于域名进行解析了：可以设定多个。

![有多种设定解析记录的方式 - CNAME就可以](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Aliyun-DNS.png)

![一条CNAME记录的`主机记录`是WWW,记录值就是你想要导向的目的地 - `xxx.github.io`](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Aliyun-DNS-WWW.png)

> **注意**：通过设定不同的解析记录，可以指向不同的目标机器的。也就意味着你花钱申请了的DNS可以帮助你搭建多个可被人们访问的网站。不要浪费了:heavy_exclamation_mark::heavy_exclamation_mark:

## 绑定你的Github 博客 - 还要回到`xxx.github.io`

在你的`xxx.github.io`的`Settings`里面绑定你前面的`www.kukoo.online`

![在`Custom domain`里输入即可](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Beginmyslashielife/Aliyun-DNS-WWW+Git.png)

# 到此为止，搭建自己的Github博客就可以了！怎么样？是不是很`简单粗暴`？！

# 觉得有趣，就打个赏吧:blush:

