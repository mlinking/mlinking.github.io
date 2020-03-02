---
title: 记录：筛选写书工具的艰苦经历
date: 2020-03-02 03:00:00
categories:
- 电子书制作
tags:
- Microsoft Word
- E-book
published: true
typora-root-url: ../../mlinking.github.io
---

说起来，很早就想试试制作电子书了：不管是教学讲义，还是生活感悟，都想能够有朝一日变成黑纸白字留下来。不过，在工具的选择和调试中，真心很辛苦！此文算是纪念吧。开始专心完善、完成那些书啦:slightly_smiling_face:

# 早期使用Word - 解决中文期刊Word排版问题

估计大家开始使用电脑，学会使用的就是微软的那一套Office 吧：我知道的现在中学生(小侄子)就要开始学习了。不过，开始学会的技巧一般也就寥寥，也就是不同字体，插入图片、表格之类的。自动编码，参考文献等技巧都是在需要写论文的时候才深切接触的：求学期间是需要写论文的！国外的还好说 - 见后面的$LaTeX$，可是国内的期刊提供的所谓`模板`真心要吐槽下：差不多都是使用Word，但基本上没有啥自动功能。

没有办法，自力更生吧。

在网上查了很多，自己尝试了很多，最终实现了一个[期刊的Word模板](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/JOS.SampleasTemplate.docx)：支持`公式、图、表、参考文献的自动更新`-这可是使用Word 写论文的痛点。

使用起来也很简单：主要是拷贝黏贴，和全选后点击`F9`

- 如果需要增加论文的公式、图、参考文献，在样例文档中找到对应的例子，拷贝到所需要的位置，然后按照需要修改公式、图、参考文献。以插入图片为例：

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Word-Image1.png)

![将图片例子拷贝到新位置，按照需要进行修改 - 替换了图片](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Word-Image2.png)

- 选中全部文档内容(`Ctrl+A`)，然后点击`F9`。图的编号自动完成了更新

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Word-Image3.png)

- 至于公式、图(表)、参考文献的引用，应该知道的吧？

>  颇有点`一法通百法通`的感觉 - 不过，还是仅限于中文期刊的排版。使用Word 写书？没有啥头绪 - 尤其是上千页：平时阅读论文，就想将看多的资料按照书的模式编纂起来。很容易就上千页了。

# $LaTeX $ - 科学论文的不二之选，写书？也可以，不过...

求学期间，也需要努力在国外的会议、期刊发表论文的，这时候$LaTeX$就是不二人选了！关于$LaTeX$的资料网上很多了，最关键的一点是`换装`很容易 - 一个$LaTeX$ 文章套用不同的出版社模板，再按照需要稍作改动就行了。

有一段时间是在Ubuntu Linux 上工作的，不过，回国后还是回到Windows 上来了，依赖的工具主要有：

- TexLive - `http://mirror.ctan.org/systems/texlive/Images/texlive2019.iso`
  - 如果你身处中国大陆，发现下载速度很慢，可以尝试清华大学和中国科技大学的镜像站。
  - `https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/texlive2019.iso`
  - `https://mirrors.ustc.edu.cn/CTAN/systems/texlive/Images/texlive2019.iso`
- TexMaker - `https://www.xm1math.net/texmaker/`
- PPT
- GIMP - `https://www.gimp.org/`

> 有时间再写一下$LaTeX$吧，例如如何使用PPT和GIMP来完成EPS图片文件等技巧。

在使用$LaTeX$的过程中，也进一步学习了如何基于$LaTeX$编纂书籍的技术：博士毕业的论文就有$LaTeX$版本(网上能够找到基于$LaTeX$的博士论文模板)。不过，国内的高校还是没有广泛接受这种方式。

# 还是试试用 Word来写书吧 - 自己制作的其实已经很不错了！

在教学过程中，很需要编写自己的讲义 - 如同`书非借不能读也`，自己讲课的内容编纂一下才能对内容更加圆融。$LaTeX$还是算了吧，还是再次尝试找找使用Word 写书的路子。好在前面解决了`公式、图、表、参考文献`的自动化问题，剩下的就是如何编写超过上千页的问题了。

> 曾经使用Word 编纂超过1000页的文档，很吃内存的，每次修改都要等很长时间！

在此要感谢[Beate网站](https://www.beautebook.com/)，那时候(2013年呢)它们还提供了几个免费的基于Word 的书籍模板(今天去看了下，似乎找不到免费的模板了 :smirk:)，排版、字体还是比较美观的。不过一个问题就是模板也是单个Word文件。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/GeauteBook.png)

那么，剩下的问题就是如何使用Word 编纂超过1000页的文件了。在网上查了下，是可以使用**Word 的大纲模式**来解决这个问题。

![Image Retrieval 书的组织结构](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Word-OutlineDir1.png)

![书籍的章节单独一个文档](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Word-OutlineDir2.png)

![主文档中嵌入了章节的那些文档](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Word-OutlineExpand.png)

![近3000页的书籍文档也是没有问题！](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Word-OutlineMorePages.png)

这样的方式好处很明显 - 跟$LaTeX$编纂博士论文(书籍)一样：不需要每次都展开书籍的全部内容，而是可以一章一章地修改、完善。最后成稿时在组合在一起即可。

> 在解决了写排版还不错的论文(Word 和 $LaTeX$)和编纂书籍(Word)后，"得陇望蜀"地想将编纂的文章能分享到网上。虽然自己会制作网站，甚至也尝试过奖Word文档发布到某易的博客，可是，终究不方面：自己维护网站很麻烦，而某易的博客很快就不再支持了。
>
> 虽然很早就知道Github以及了解过基于Github构建自己的博客(阮一峰的那篇文章很早就看过了)，可是，正如[简单粗暴的方法构建Github 博客](`http://www.kukoo.online/2020-02/Begin-my-slashie-life-1-GitBlog/`)文中所述，那些繁琐的配置让我没啥兴趣。不过，在找到有趣的博客后，似乎解决了这个(文档分享)问题，也进一步有兴趣了解下Markdown。


# Markdown - 科技工作者的人文情怀 - 适合网络写作。写书？还是不方便呀

按照前面的叙述，我对MD的期望也是类似的：**文章**(此文章是指网文)，**书籍**(PDF, EPUB, MOBI等)和**网上分享**。在文章和网上分享方面，Markdown 还是不错的 - 毕竟其受追捧也在于此。

在尝试编纂书籍时，GitBook是不错的选择，不过，那仍然不是自己掌握。而要自动动手，又是那么繁琐！尤其是将MD组织的文档转换为PDF，看网上，是依赖于LaTeX的，需要自己设定模板(Template)等。本来MD是解放人们不用陷入繁琐的排版的，而将MD转换为PDF却是开倒车 - 我很有`削足适履`的感受。

甚至网上有文给出了所谓的生成PDF的捷径：*使用Pandoc 生成Word 文档，然后将那些Word文档集成为一个Word文件，再经过细心的(`繁琐地`)格式调整后，使用Word 软件生成PDF*。这就有些*GX*了：那还不如直接使用Word编纂书籍。

所以就形成了现在的格局：

- Word 用于编纂书籍，并生成不同种类的电子书(Word自己导出 PDF 很不错了！EPUB，MOBI，AZW3等)
- 会议、期刊论文，还是Word (中文)和 $LaTeX$ (外文)
- 网文的写作和分发，就是Markdown了

# Word + Calibre - 个人用来制作电子书还是够的

## Word 本身就能很好地支持PDF 的导出

在使用Word 编纂好书籍后，也就是最后输出一个Word文件：

![大纲视图中选中那些链接的文档，选择`取消链接`](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Word-Outline-MergeAll.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Word-Outline-MergedAll.png)

然后就可以直接使用Word中的`另存为`PDF即可，你还可以选择创建`书签`

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/WordtoPDF.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/WordtoPDF-TOC.png)

生成的PDF还是很完美的

## 封面

网上找找即可。我建议在 PDF 后再加入制作的封面即可。当然，你也可以在Word中嵌入制作的封面。这都不影响后面电子书的制作 - 在Calibre 中替换封面即可。

> 使用 Canva 在线图形设计工具和 Pixabay 网站提供的免费图快速和容易地创建一个免费的专业品质书籍封面。 你所需要的只是一个网页浏览器，在 10 分钟内就能完成一本书的封面。 我展示的过程中，利用免费的 Canva 的 Kindle 书籍封面主题和来自 Pixabay 的免费图片 ，快速创建专业品质的书籍封面。
>
> 来自 `https://softnshare.market/amazon-self-publishing-free-canva-book-cover-marketing/`

## 借助Calibre 导出其他格式的电子书 - EPUB,AZW3, MOBI等

使用Calibre Management 打开DOCX文档，默认会自动从DOCX中提取一个图片作为封面。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Calibre-Default.png)

DOCX导入到Calibre 中后，就可以使用 `书籍转换`来生成电子书籍了。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/ToWritePaperAndBook/WordAndCalibre/Calibre-Convert-Config.png)

从上图右上角看出，Calibre 支持很多不同的电子书格式 - EPUB, MOBI, AZW3等。

剩下的就是耐心等待下了...倒是都成功了!


# 最后是一些资料

- [The Not So Short Introduction to LaTeX] `http://tug.ctan.org/info/lshort/english/lshort.pdf`
- [一份其实很短的 LaTeX 入门文档] `https://liam.page/2014/09/08/latex-introduction/`
- [How to Design Your Book Cover Free] 
- [How to Create a Kindle Book Cover in 15 minutes] `https://www.youtube.com/watch?v=ujX9-slHquw`
