---
title: Jupyter Book 支持 R:做的还不够呀
date: 2020-03-28 01:00:00
categories:
- 电子书制作
tags:
- Jupyter NoteBook
- Jupyter Book
- R
- R Bookdown
published: true
typora-root-url: ../../mlinking.github.io
---

[记录：筛选写书工具的艰苦经历]()简要记录的自己尝试几种工具的艰苦努力，最后的结论是"Word + Calibre" 制造常用的电子书(DOCX, PDF, EPUB，MOBI和AWZ3等)还是够用的。

[自己制作本地的Jupyter Book](http://www.kukoo.online/2020-03/Get-Web-Jupyter-Book/)简单介绍了如何使用 Jupyter Book `create` 和 `build` 生成Web 书(当时是以 Python 语言为例)。

[使用R BookDown 来写书 - PDF, EPUB和Web版。还是算了吧!](http://www.kukoo.online/2020-03/Build-Web-version-Book/)记录了使用 R Bookdown 制作 PDF, EPUB和Web 书的经历。不过，R Bookdown 生成的 Web 书不支持交互式算法展示 - PageDown 想完成这一点。调试过程中的麻烦真是不能忍受 - 绝对不比$LaTeX$写书得麻烦来的少！

想着 看到过 Jupyter Notebook 支持很多语言，所以，进一步试一试 Jupyter NoteBook 如何支持R。

# 需要设置Jupyter Notebook 以包含 R kernel

## 需要提前安装好 R 和 R Studio
## 建议将Conda 包源改成国内的源

## 在Conda Prompt 中`conda install -c r r-irkernel`安装 R Kernel

![CondaInstallRKernel](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/CondaInstallRKernel.png)

## 进入 R CLI，运行`IRkernel::installspec(user=FALSE)`以设定全部用户可用

![RKernelforAll](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelforAll.png)

## 运行 Jupyter NoteBook，可以看到有了R Kernel 的支持

![RKernelwithR](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelwithR.png)

## 试试，支持了 R 代码 – 简单的可以

![RKernelwithROk4Simple](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelwithROk4Simple.png)

## 但是，调用library 就不行了

## 试了很多方式，不是前面没安装好，其实就是没有那些library而已

![RKernelwithRNotOk4Library](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelwithRNotOk4Library.png)

### 在 R Console 里走一遍那些命令

#### `install.packages(c('repr', 'IRdisplay', 'evaluate', 'crayon', 'pbdZMQ', 'devtools', 'uuid', 'digest'))`

![RInstallPackages](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RInstallPackages.png)

##### 过程中弹出个窗口让你选择mirror – 我选了lanzhou。然后，很快就安装完了

![RInstallPackagesDone](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RInstallPackagesDone.png)

#### devtools::install_github('IRkernel/IRkernel') – 依赖Git 程序

##### 安装完“Git-2.25.0-64-bit.exe”，再运行此命令就可以了

![RInstallPackagesGithub](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RInstallPackagesGithub.png)

#### `IRkernel::installspec()` 和` IRkernel::installspec(user = FALSE) `都没成 – 就算了

### 简单的R 命令没问题，加载包就不行了。

#### 开始还以为是加载 R Kernel 进 Jupyter Notebook

`https://www.jianshu.com/p/8b90c2f12856`

```{R}
library("ggplot2")
ggplot(data = mtcars, aes(x = wt, y = mpg, color = cyl)) + geom_point() +
geom_smooth(method="lm") +
 labs(main="Regression of MPG on Weight",
 xlab="Weight", ylab="Miles per Gallon")
```

![RLibraryNotOk](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RLibraryNotOk.png)

#### 调用 `library()`，弹出了已安装的包，里面确实没有 `ggplot2`

![RLibraryNotOkNoGGplot2](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RLibraryNotOkNoGGplot2.png)

##### 倒是有 datasets 包

![RLibraryOkDatasets](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RLibraryOkDatasets.png)

![RLibraryOkDatasetsIris](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RLibraryOkDatasetsIris.png)

##### 在 Jupyter NoteBook 中试下library(datasets) head(iris) – 可以的

![RKernelinJupyterOkDatasetsIris](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelinJupyterOkDatasetsIris.png)

### 也就是在 R 中能运行的，在Jupyter Notebook 的 R kernel 中也能正常运行

#### 查看R 支持的包是关键。那么，怎么添加一下包呢？

![RKernelLibraries](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelLibraries.png)

![RKernelLibrariesSources](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelLibrariesSources.png)

### Data.table 和 Ggplot2 的问题的解决 – 就是没有安装那些包而已

#### `install.packages('data.table')`

#### `install.packages('scorecard')` 就顺带安装了`ggplot2`

![RKernelLibrariesscorecard](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelLibrariesscorecard.png)

![RKernelLibrariesscorecardwithggplot2](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelLibrariesscorecardwithggplot2.png)

## 不过，上面是在R 程序里加载了 ggplot2, data.table等，还需要在 Anaconda 的 Jupyter 中的 R kernel 中也加载

### 在 R 程序加载了scorecard包后，Jupyter 的 R kernel 中是没有 的

![RKernelNoDataTable](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelNoDataTable.png)

### 还得在 Anaconda Jupter 中也加载一遍

![RKernelNoDataTableOk2](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelNoDataTableOk2.png)

![RKernelNoDataTableOk](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelNoDataTableOk.png)

![RKernelNoDataTableOk4](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelNoDataTableOk4.png)

### 然后，不用再启动 Jupyter 就能使用那些包了

![RKernelNoDataTableOkJupyter](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelNoDataTableOkJupyter.png)

### 我按照前面最开始安装的 R Kernel 是 3.6.1 版本。而由上面的截图看，data.table 是 R 3.6.3 的。不过，仍然可行

```{R}
library(data.table)
head(iris)
summary(iris)
```

![RKernelNoDataTableOkJupyterIris](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/RKernelNoDataTableOkJupyterIris.png)




# 试试 Jupyter Book 来写R编程书 - 静态Web书没问题；交互？够呛！

## 开始应该还是 Jupyter Book 生成Demo

## 然后修改其中的配置和ipynb文件 - 不过，这时ipynb要`New R Notebook` - 然后执行一遍

![JN-ExecRCells](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/JN-ExecRCells.png)

## `Jupyter Book Build` ，进而 `bundle exec jekyll serve` - 生成的静态Web还是不错的(跟Notebook的效果一致)

![JB-RCellsStaticHTMLOk](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/JB-RCellsStaticHTMLOk.png)

## 但是，R代码交互就不成了 - "Waiting for kernel" ...

![JB-RCellsInteractMode](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/JB-RCellsInteractMode.png)

![JB-RCellsInteractModeRun](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/JB-RCellsInteractModeRun.png)

![JB-RCellsInteractModeWaiting](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/JB-RCellsInteractModeWaiting.png)

### 应该是 Jupyter Book 默认只是连接Python kernel. R Kernel? 不知道呢！

![JB-RCellsInteract-LostRKernel](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/JB-RCellsInteract-LostRKernel.png)

## 查了很久，没有找到解决办法，觉得有必要提交给Jupyter Book 的开发人员 - 不过，不确定是否人家解决了

### 了解到: 有将ipynb提交至在线Jupyter Notebook Hub 或第三方的方案，不过，毕竟还是效率很低

### 问题1: 前面的 `open(xxx,'rb')`解决中文问题

### 问题2: 就是前面指出的"Jupyter Book不能使用R Kernel"

# Jupyter Notebook 甚至支持同一个ipynb文件有不同语言的代码运行 - `rpy2` - 备存

## rpy2

`https://cloud.google.com/ai-platform/notebooks/docs/r-python-same-notebook`

### Create a notebook for use with R and Python

**To use rpy2 to work with both R and Python in the same notebook, create a Python 3 notebook**. To create the notebook:

1. Go to the **AI Platform Notebooks** page in the Google Cloud Console.

   [Go to the AI Platform Notebooks page](https://console.cloud.google.com/ai-platform/notebooks/instances)

2. Select **Open JupyterLab** for the R instance that you want to open.

3. Select **File** -> **New** -> **Notebook**. Select the Python 3 kernel for your new notebook.

   Select **File** -> **Rename notebook** and change the name of the untitled notebook to something meaningful, such as "rpy2.ipynb."

   The notebook is ready for you to import rpy2 and use R and Python in the same workbook.

### Use rpy2 to import R objects

To import R objects with rpy2:

1. In the notebook's first code cell, enter the following: `import rpy2.robjects as robjects`.

   ![Enter the import statement in the first cell](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/rpy2-0.png)

2. Click the run button. Python imports rpy2's functions for accessing and manipulating R objects.

   ![The run button](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/rpy2-2.png)

3. To add a code cell to the notebook, click the notebook's + button.

   ![The + button](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/JupyterBookForR/rpy2-1.png)

4. In the new code cell, enter the following: `pi = robjects.r['pi']`.

5. Click the run button. Python stores an R pi object.

6. To print the value of pi, in a new code cell, enter `pi[0]` and click the run button.

   ```{R}
   pi = robjects.r['pi']
   pi[0]
   ```

## Example

`https://stackoverflow.com/questions/39008069/r-and-python-in-one-jupyter-notebook`

Yes, it is possible! Use rpy2.

You can install rpy2 with: `pip install rpy2`

Then run `%load_ext rpy2.ipython` in one of your cells. (You only have to run this once.)

Now you can do the following:

Python cell:

```py
# enables the %%R magic, not necessary if you've already done this
%load_ext rpy2.ipython

import pandas as pd
df = pd.DataFrame({
    'cups_of_coffee': [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
    'productivity': [2, 5, 6, 8, 9, 8, 0, 1, 0, -1]
})
```

R cell:

```
%%R -i df -w 5 -h 5 --units in -r 200
# import df from global environment
# make default figure size 5 by 5 inches with 200 dpi resolution

install.packages("ggplot2", repos='http://cran.us.r-project.org', quiet=TRUE)
library(ggplot2)
ggplot(df, aes(x=cups_of_coffee, y=productivity)) + geom_line()
```

And you'll get your pretty figure plotting data from a python Pandas DataFrame.

# 小结

## R, RStudio 和 Jupyter R Kernel 是相互独立的

## 安装完毕后，Jupyter Notebook 对R的支持跟R Project 是一样的

## 使用 Jupyter Book 写 R 算法书：

### 静态Web版 - 跟Jupyter Notebook是一致的

### 但是，不能运行Web上嵌入的R代码 - 而嵌入Python时是可以的，虽然花的时间长些

## 关于写书和写论文

到目前为止，写书和论文的工具真是用了很多了，有如下的总结：

### 写书 - PDF, EPUB, AZW3, MOBI

我觉得还是 Word + Calibre 就可以了。

- 活用 Word 的**大纲**模式，就能够编纂页数很多的书(我编纂过仅2000页的书，没有问题)
- 要解决很多自动问题：图、表和公式的自动编码和引用，参考文献的自动引用等(已解决，另文撰述)
- Word 本身对PDF 的支持就很不错。
- 使用Calibre 导入 Word 文档，经过一些简单的设置就能够导出格式不错的EPUB，AZW3, MOBI等(参看)

不足的就是不能生成算法交互的Web。

### 写书 - 算法交互的Web书

觉得 Jupyter NoteBook 就可以了：能够支持很多语言。要做的就是讲对应语言的Kernel 加载进 Jupyter Notebook。

### 论文 - Word + LaTeX

- 中文论文，还是使用Word 吧。主要的挑战就是要解决图、表、公式的自动编号和引用，以及参考文献的格式和引用。
- 英文论文，自然是 $LaTeX$ 不可。

### 想要算法交互展示？那还是使用 Jupyter NoteBook吧。

