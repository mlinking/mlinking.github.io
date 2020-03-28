---
title: 使用R BookDown 来写书 - PDF, EPUB和Web版。还是算了吧！
date: 2020-03-28 00:00:00
categories:
- 电子书制作
tags:
- Jupyter NoteBook
- Jupyter Book
- R
- RStudio
- Bookdown
- PageDown
published: true
typora-root-url: ../../mlinking.github.io
---

前面一文[记录：筛选写书工具的艰苦经历](http://www.kukoo.online/2020-03/Slashie-My-experience-to-produce-e-books/)简要记录的自己尝试几种工具的艰苦努力，最后的结论是"Word + Calibre" 制造常用的电子书(DOCX, PDF, EPUB，MOBI和AZW3等)还是够用的。

如果想要制作 Web 书，甚至是需要算法的动态展示？[自己制作本地的Jupyter Book](http://www.kukoo.online/2020-03/Get-Web-Jupyter-Book/)简单介绍了如何使用 Jupyter Book `create` 和 `build` 生成Web 书。在那里也提到了我感兴趣的支持数据分析不错的工具 - R 和 RStudio，围绕R也有创建Web 书的技术。

# R BookDown 编纂Web 书

在[自己制作本地的Jupyter Book](http://www.kukoo.online/2020-03/Get-Web-Jupyter-Book/)中展示了几本谢益辉(YiHui Xie)[[GitHub](https://github.com/yihui),[Web](https://yihui.org/)]编纂的围绕R制作 PDF, EPUB和Web书的几本书，想着自己也有计划完成基于R的数据分析册子，所以，就搜罗资料实践了下如何基于 R BookDown 生成书的技巧。

## R Studio 编纂 BookDown 书就够了 (不依赖*nix 操作系统环境)

意思是，虽然R语言包是RStudio 的底层技术，不过，有了 RStudio，其实就是够了：不管是使用R来编程，还是使用BookDown 来写R语言交互的书。

之所以点出来这一点，是因为我在R Project 的代码里加载了所需要的包，但是，R语言包和RStudio 的R语言包二者是相互独立的。

## 一些依赖的包还是换成国内源吧

一如很多开源软件的安装，访问国外是很耗时的，还是换成国内的源吧。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-ChinaSource.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-ChinaSourceShanghai.png)

## 在 RStudio 中创建 Bookdown project 很简单

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BookProject.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BookProjectDemo.png)



## 只是编译(Build All)的时候，有些包要依赖 – `rmarkdown`, `caTools`等。而这些包还依赖 R 的版本

### 我最开始安装的是 R3.5.2，在`Build All` 时就出现需要 `caTools 1.14`。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BuildAllErrorcaTools.png)

### 查了下，caTools 有要求R的版本高 – 只好重新安装最新的 R 3.6.3

### 须重启 RStudio (会自动换成R 3.6.3环境) – 安装那些包即可

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BuildAllInstallPackages.png)

安装了` rmarkdown `后，就少了很多包

```{R}
> install.packages('rmarkdown')
also installing the dependencies ‘highr’, ‘markdown’, ‘digest’, ‘Rcpp’, ‘rlang’, ‘glue’, ‘magrittr’, ‘stringi’, ‘knitr’, ‘yaml’, ‘htmltools’, ‘evaluate’, ‘base64enc’, ‘jsonlite’, ‘mime’, ‘tinytex’, ‘xfun’, ‘stringr’
```

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BuildAllInstallPackages2.png)

按照提示，在 RStudio 的 Console 里安装相应的包即可

```{R}
install.packages('caTools')
install.packages('bitops')
install.packages('rprojroot')
install.packages('bookdown')
```

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BuildAllInstallPackages3.png)

### 再次build All 就可以了

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BookProjectDemoOK.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BookProjectDemoOutput.png)

### 生成了 HTML, PDF 和 EPUB。效果还是不错的。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BookProjectDemoPDFEPUB.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BookProjectDemoPDF.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BookProjectDemoEPUB.png)

### 对照Rmd文本和生成的页面，看出，页面中有Rmd中嵌入的R代码的结果图

**01-intro.Rmd**

```{R}
# Introduction {#intro}

You can label chapter and section titles using `{#label}` after them, e.g., we can reference Chapter \@ref(intro). If you do not manually label them, there will be automatic labels anyway, e.g., Chapter \@ref(methods).

Figures and tables with captions will be placed in `figure` and `table` environments, respectively.

​```{r nice-fig, fig.cap='Here is a nice figure!', out.width='80%', fig.asp=.75, fig.align='center'}
par(mar = c(4, 4, .1, .1))
plot(pressure, type = 'b', pch = 19)
​```

Reference a figure by its code chunk label with the `fig:` prefix, e.g., see Figure \@ref(fig:nice-fig). Similarly, you can reference tables generated from `knitr::kable()`, e.g., see Table \@ref(tab:nice-tab).

​```{r nice-tab, tidy=FALSE}
knitr::kable(
  head(iris, 20), caption = 'Here is a nice table!',
  booktabs = TRUE
)
​```

You can write citations, too. For example, we are using the **bookdown** package [@R-bookdown] in this sample book, which was built on top of R Markdown and **knitr** [@xie2015].

```

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BookProjectDemowithResult.png)

在Web 版上也能显示。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/RStudio-BookProjectDemowithResultWeb.png)

## 不过，Bookdown 生成的HTML确实不能交互了 – Jupyter Book 则借助 Jupyter Notebook 而能交互

# Build 一本实际的R BookDown书的经历 - 麻烦程度绝对不比$LaTeX$ 写书低

想榜样学习，应该算是`捷径`吧。就想着找一个 R BookDown 写的书的源代码，然后自己Build 一下：既能通过阅读源代码而学习如何使用R BookDown 编纂实际的书的技巧；又能真实体验一下使用R Bookdown的麻烦程度。还真能找到这样的书。

## R Bookdown的书站：`https://bookdown.org/`

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/BookdownHub.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/BookdownHubBooks.png)

## R For Data Science 书 - 感谢Garrett Grolemund, Hadley Wickham

在 Google 中输入 "R For Data Science Github"，幸运地找到这本书的源码。

`https://github.com/hadley/r4ds`

`https://r4ds.had.co.nz/`是此书的Web 版本。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Git.png)

## Build 此书 - 痛苦也就开始了！

类似前面的叙述，在RStudio 中`Build All` 此书。遇到了很多的问题，到最后也没有成功！痛苦不堪！

### 缺包问题很多，不过解决也简单 - `install.packages(xxx)`即可

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-LostPackages.png)

在右上的Build 标签页中能看出是缺少`dplyr`，那么，在左下的Console 中`install.packages('dplyr')`即可：*当然，在国内的话还是修改为国内源为宜*。

### 在 Build 消息框里面的汉字显示有问题，不过，可以定位到相应的代码处，点击红色方框中的小绿三角，就运行了那个代码。在Console 中就显示了错误信息的中文

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-Chinese.png)

### 还有一个 typo  - “var1able”:应该是“variable”

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-Typo.png)

### 过程中有一次生成了 HTML页面 – 虽然是分在两个目录（还没有整个合在一起），不过，已经可以在HTML中正确嵌入图片了。不过，整个生成过程不成功的（前面bookdown 例子，生成了 PDF, HTML 和EPUB的）。<u>*最终，也不清楚为什么不行，为什么不成功*</u>

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-Output.png)

将 HTML页面和那些包含图片的目录手工合在一起，然后查看HTML – 正确嵌入了 图片。

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-OutputHTML.png)

### 即便是安装了那些包，以及改了typo，还是不能生产PDF，也并没有 EPUB (应该是EPUB的build 在 PDF之后，所以，PDF不过，后面的 EPUB也没有了) – <u>说是 GHC 的问题</u>

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHC.png)

#### 开始以为是 pandoc.exe 的问题，将错误信息在Google 搜索，没有效果

\-     Pandoc.exe internal error closure type xxxx

\-     GHC version 8.6.5 for x86_64_unknown_mingw32

#### 下一个错误我开始以为是mingW32 的问题，找了很多mingW32 的工具包（RTools, 专门的mingw32, R和RStudio 自带的 mingW32等等），都没有用

#### 还按照 GHC信息找到关联的 Haskell，安装并PATH中添加了路径，也没有用

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCHaskell.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCHaskellNoUse.png)

#### 最后，确定还真是 没有 GHC 8.6.5 程序的问题！

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCOk.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCBin.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCMingW.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCMingWBin.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCPATH.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHC-v.png)

#### 要重新启动 RStudio，GHC才有效

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCRStudio.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCRStudioBuild.png)

### 可还是不行 – 导出的$LaTeX$ 有问题！

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCRStudioBuildLaTeX.png)

#### 查看 _main.log文件：不明所以

#### 甚至想试试 TexMaker 使用XeLaTeX调试一下 _main.tex，更是一头雾水！

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCRStudioBuildTexMaker.png)

#### 甚至试了 更改 RStudio 中的 LaTeX 配置，没有用的

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCRStudioBuildTexConf.png)

### 虽然没顺利结束，其实生成了 HTML 和 PDF 了 – EPUB 因为在PDF之后就被挡住了

#### HTML

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCHTML.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCHTML2.png)

#### PDF

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCPDF.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCPDF2.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCPDF4.png)

### PDF看上去也还不错，不过。。。排版问题还是很多！图的大小，很多warning

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCPDFBad.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCPDFBad2.png)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/R4DS-Build-GHCPDFBad3.png)

# 算是总结吧

到目前为止，写书和论文的工具真是用了很多了，有如下的总结：

## 写书 - PDF, EPUB, AZW3, MOBI

我觉得还是 Word + Calibre 就可以了。

- 活用 Word 的**大纲**模式，就能够编纂页数很多的书(我编纂过仅2000页的书，没有问题)
- 要解决很多自动问题：图、表和公式的自动编码和引用，参考文献的自动引用等(已解决，另文撰述)
- Word 本身对PDF 的支持就很不错。
- 使用Calibre 导入 Word 文档，经过一些简单的设置就能够导出格式不错的EPUB，AZW3, MOBI等(参看)

不足的就是不能生成算法交互的Web。

## 写书 - 算法交互的Web书

觉得 Jupyter NoteBook 就可以了：能够支持很多语言。要做的就是讲对应语言的Kernel 加载进 Jupyter Notebook。

## 论文 - Word + LaTeX

- 中文论文，还是使用Word 吧。主要的挑战就是要解决图、表、公式的自动编号和引用，以及参考文献的格式和引用。
- 英文论文，自然是 $LaTeX$ 不可。

想要算法交互展示？那还是使用 Jupyter NoteBook吧。

# 其他


## Jupyter 也支持 R 语言(另文)

## R PageDown就算了吧(想试试的自己去试试吧)


## 再次推荐去看看谢益辉(YiHui XIE)的博客吧

- [GitHub](https://github.com/yihui)
- [Web](https://yihui.org/)

![](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/BuildWebBook/XIEYiHuiWeb.png)
