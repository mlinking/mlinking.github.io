---
title: 自己制作本地的Jupyter Book
date: 2020-03-23 00:00:00
categories:
- 电子书制作
tags:
- Anaconda
- Jupyter NoteBook
- Python
published: true
typora-root-url: ../../mlinking.github.io
---

前面一文[记录：筛选写书工具的艰苦经历]()简要记录的自己尝试几种工具的艰苦努力，最后的结论是"Word + Calibre" 制造常用的电子书(DOCX, PDF, EPUB，MOBI和azw3等)还是够用的。不过，还是觉得要写一本使用Python 完成编程的书(近期的计划是**商务视角下的数据分析**，和**高性能计算**)​，能够编纂配套的代码展示也是有必要的，所以，又了解了下使用Jupyter NoteBook 编写Python 代码书的技巧，汇总于此。

# 关于 Jupyter Notebook

Jupyter notebook 由 Fernando Perez 在 2001 发起。它的目标是提供 "Tools for the entire life cycle of research computing." 如果说 Python 是数据科学操作的引擎，那么 IPython 就是交互式的控制面板。

![The guy at left is Fernando Perez](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/Fernando_Perez_and_Richard_Stallman_-_2012_FSF_Award.jpg)

- IPython 只是为 NumPy、Scipy、Pandas、Matplotlib 等包提供一个交互式接口。其本身并不提供科学计算的功能。这些工具组合在一起，形成了可以匹敌如 Matlab、Mathmatic 这些复杂工具的科学计算框架。
- IPython 是一种交互式 shell，与普通的 Python shell 相似，但具有一些很好的功能（例如语法高亮显示和代码补全）。notebook 的工作方式是：你通过浏览器连接到该服务器，而 notebook 呈现为 Web 应用。你在 Web 应用中编写的代码（你在浏览器中看到的 notebook）通过该服务器发送给内核 IPython 内核（在后台运行的 IPython 应用程序），内核运行代码，并将结果发送回该服务器。之后，任何输出都会返回到浏览器中。
- Jupyter Notebook（Jupyter命名是取自Julia语言，Python语言，R语言，曾用名iPython Notebook）原来也叫iPython Notebook，顾名思义，它和Python关系紧密。Jupyter Notebook 是一个开源的 Web 应用程序，便于创建和共享文学化程序文档，支持40多种编程语言，支持实时代码、数学方程、可视化和 Markdown，其用途包括数据清理和转换、数值模拟、统计建模、机器学习等等。目前，数据挖掘领域中最热门的比赛 Kaggle 里的资料都是 Jupyter 格式。
- 对于机器学习和数据科学的工作者来说，如果都应该使用或必须使用一种工具，那毫无疑问，它就是Jupyter Notebook；数据科学家可以在上面创建和共享自己的文档，从实现代码到全面报告，Jupyter Notebook大大简化了开发者的工作流程，帮助他们实现更高的生产力和更简单的多人协作。也正是因为如此，它一直以来都是数据科学家们最喜欢的工具之一。




# Jupyter Book 所需要的工具 - Anaconda 的Jupyter NoteBook就不错



官方在文档中强烈建议新用户用Anaconda打包安装Python和Anaconda——所谓懒人方法，小白必备。其实除了提到的两个工具，Anaconda还包含数据科学和机器学习中经常需要用到的各种软件包，只需下载、解压、安装，所有工具就都一步到位了。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/JupyterNotebookwithAnaconda.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/JN-CLI.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/JN-Web.png)

其中，"C:\Users\86150"就是默认的根目录。

# Jupyter Book 生成Demo Book - 很简单的指令



在安装好Jupyter NoteBook 后，创建一个Jupyter Book 的Demo 是很简单的事。

## 管理员身份打开 Anaconda Prompt 

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/AnacondaPrompt.png)

## 创建目录，在Prompt 中定位置该目录，执行`jupyter-book create mybookname --demo`

会自动生成Jupyter Book 的目录。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/JB-Demo.png)

## 使用Jupyter NoteBook 编辑 MD, ipynb等 - 另文叙述

## 执行 `jupyter-book build mybookname`会自动Build 相应的HTML

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/JB-DemoBuild.png)

## 不过，那些HTML在浏览器直接打开是乱的

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/JB-DemoWrong.png)

## 说是可以推送到 Git Pages，借助GP 的 Jekyll 来得到 – 后面有本地构建Jupyter 书 对应的 Web Site的方法

# 想要像 Git Pages 那样网页显示 Jupyter Book，需要 Ruby, Jekyll，Gem 和 Bundle – 一定要使用国内的源！

要构建Jupyter Book 本地的Web site，需要类似 Git Hub 的环境，即 Ruby 和 Jekyll。

## 安装 Ruby

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/RubyInstaller.png)

## 得安装 Jekyll – Gem 和 Bundle还是要国内的源



### `gem install jekyll`

安装 Jekyll 的指令很简单，就是`gem install jekyll`，但是，该指令默认是访问国外的网站，那速度是不能忍受的。所以，必须换成国内的源。

#### 先换国内的源

```
$ gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
$ gem sources -l
https://gems.ruby-china.com
# 确保只有 gems.ruby-china.com
```

> 上面的`gems.ruby-china.com`只是举例(我安装时倒是测试通过了)，也还有其他国内的源可用的。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/InstallJekyll.png)

再install Jekyll 就飞快了！

#### `gem install jekyll-paginate`

### gem install bundle

#### 在没换国内源前，虽然也能成功，但是，jekyll -v 就失败了 – 缺很多东西！

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/InstallJekyllWrong.png)

即便是安装`MSYS2 and MINGW development toolchain` – `Jekyll -v` 还是失败。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/InstallMSYS2andMINGW.png)

虽然似乎可以按照错误提示安装对应的包，但是，太过麻烦！

#### 还是使用Bundle 来的方便：能将所依赖的资源自动安装完成 – 也要国内的源

```
$ bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```

换成国内的源然后就是飞快！- `bundle install`

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/BundleInstallJelyll.png)

### 遇到的问题

#### 因为之前安装了 concurrent-ruby 1.1.6，而依赖的是1.1.5，还是不能显示`Jekyll -v`

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/JekyllVError.png)

#### `bundle exec jekyll -v`就可以了 – 成功！

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/JekyllVErrorPass.png)

## 此时在Jupyter Book 的目录下运行`bundle exec jekyll serve`就生成类似GP的Web Book 了！

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/JekyllServe.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/JekyllServeWeb.png)

# 其他

## 遗留的需求

要是能使用Jupyter Book 生成PDF就好了。可是，据现有的资料知道，只支持Web 形式的Book。

## Jupyter Book 是想模仿国人YiHui XIE 的 R BookDown 

> `https://jupyterbook.org/intro.html`
>
> Jupyter Books lets you build an online book using a collection of Jupyter Notebooks and Markdown files. Its output is similar to the excellent [Bookdown](https://bookdown.org/yihui/bookdown/) tool, and adds extra functionality for people running a Jupyter stack.

`https://bookdown.org/yihui/bookdown/`

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/BookDownCover.jpg)

`https://bookdown.org/yihui/rmarkdown/`

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/RMarkdownCover.png)

`https://bookdown.org/yihui/blogdown/`

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/BookDownCover.jpg)

## 几本Jupyter Book 例子



### 1. `jupyterbook.org`自带的样例书，并本地构建

- 将 `book_template`拷贝到一个目录，改了名字(目录名字一定不要有空格)。
- 就直接 `jupyter book build xxx [目录名]`
- 有所修改后，再次运行`jupyter book build xxx [目录名] --overwrite`
- 进入书籍目录，运行`bundle exec jekyll serve`

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/TemplateBook.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/TemplateBookUpdatedWeb.png)

### 2. 不错的`The Riemann Problems for Hyperbolic PDEs` - 还有视频

`https://github.com/clawpack/riemann_book`

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBook/TemplateRiemannPDEs.png)



## JupyterLab，号称`极其强大的下一代notebook`！- 感兴趣就自己找找吧



## 一些资料

### Dan Toomey 的几本书

- [Learning Jupyter] 
- [Jupyter Cookbook] 
- [Jupyter for Data Science] 

