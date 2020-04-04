---
title: 变ipynb为服务 - 不需要用户安装环境
date: 2020-04-04 01:00:00
categories:
- 电子书制作
tags:
- Jupyter NoteBook
- JupyterHub
- Binder
- Cocalc
- sagemath
published: true
typora-root-url: ../../mlinking.github.io
---

这几天围绕着 Jupyter NoteBook的使用浏览和尝试了很多，比如如何使用Jupyter Notebook 完成交互式代码展示([记录：筛选写书工具的艰苦经历](http://www.kukoo.online/2020-03/Slashie-My-experience-to-produce-e-books/))，使用Jupyter Book 写Web书([自己制作本地的Jupyter Book](http://www.kukoo.online/2020-03/Get-Web-Jupyter-Book/))，甚至涉猎了与R相关的技巧([使用R BookDown 来写书 - PDF, EPUB和Web版。还是算了吧！](http://www.kukoo.online/2020-03/Try-R-Bookdown/)，[Jupyter Book 支持 R:做的还不够呀](http://www.kukoo.online/2020-03/Jupyter-for-R-book/))等。

到今天，算是对如何使用 Jupyter Notebook 构建算法交互展示有了了解。不过，制作了ipynb文件，总不能奢望读者都有足够的运行环境(Python, Juoyter Notebook甚至是很多必要的包)，所以，如何变ipynb为服务，让读者不需要安装那些环境就能交互，自然是好的。据此，找了几篇网文实践了下，记录于此。

# 补充下Jupyter 的好

- Jupyter支持超过40种语言, 其中包括Python, R, Julia和Scala。
- Jupyter的编程环境很不错： 你可以写一段图文并茂的说明(Markdown), 再写一段代码(Python, R等), 然后单独运行刚刚写过的这一段代码, 看到结果, 调试代码, 改好以后再进行下一段
- 如果一个程序要间断好多天才能写完, 那么这种方式能够帮你迅速找到前几天的思路，显然利于继续完成之前的作品
- Jupyter 的安装，比较好的搭配就是使用Anaconda 来完成
- 可以将制作的ipynb文件存放到Github上供大家分享(Github上有很多)

但是，想要让读者愉快地阅读和执行ipynb中的代码，奢求他们都能熟练地安装那些环境，还是有些不方便。如果能够像使用WWW技术访问网站一样，只要有浏览器就可以访问那些ipynb并执行其中的代码，自是值得追求一下。好在，80%的情况下，你的需求也是被人的需求，很大可能也已经解决了的。

# 几个支持Web 访问和执行ipynb 代码的网站

## [JupyterHub](https://github.com/jupyterhub/jupyterhub) + [BinderHub](https://github.com/jupyterhub/binderhub)

两个都是Jupyter 旗下的子项目。

> With [JupyterHub](https://jupyterhub.readthedocs.io/) you can create a **multi-user Hub** which spawns, manages, and proxies multiple instances of the single-user [Jupyter notebook](https://jupyter-notebook.readthedocs.io/) server.

> **BinderHub** allows you to `BUILD` and `REGISTER` a Docker image from a Git repository, then `CONNECT` with JupyterHub, allowing you to create a public IP address that allows users to interact with the code and environment within a live JupyterHub instance. You can select a specific branch name, commit, or tag to serve.
>
> BinderHub ties together:
>
> - [JupyterHub](https://github.com/jupyterhub/jupyterhub) to provide a scalable system for authenticating users and spawning single user Jupyter Notebook servers, and
> - [Repo2Docker](https://github.com/jupyter/repo2docker) which generates a Docker image using a Git repository hosted online.
>
> BinderHub is built with Python, kubernetes, tornado, npm, webpack, and sphinx.

## [Cocalc](https://cocalc.com)

Cocalc 是一个科学计算平台, 除了提供Jupyter, 还提供了sagemath(也是一个强大的数学计算工具, 可以当作一个开源的mathematica, 随手解个方程, 求个微分之列都很方便)。

CoCalc已经安装好了大量的python包, 比如numpy, tensorflow, keras, pytorch…

Cocalc有免费版和付费版。 免费版没有额外的网络连接, 也就是说你无法在cocalc里面再访问其他网页, 比如你用Jupyter写了一个网络服务程序, 那么是无法用在cocalc免费版里面的. 用git也会受限制. 没有网络连接最麻烦的是如果cocalc没有预装的包, 你是无法自行安装的. 不过如果确实是很常用有名的Python包, 那么可以向cocalc网站的支持发个email, 他们的响应速度超级快, 很有可能就帮你装好了.

## [Azure notebook](https://notebooks.azure.com)

[Azure notebook](https://notebooks.azure.com)是微软提供的在线jupyter服务, 财大气粗的微软提供的内存, CPU, 存储空间都不错.

特色功能有二:

- 方便一键clone, 看好其他人的做得不错的东西, 可以方便clone一份自己研究
- 可以从github导入, 只需要将看中的github repo页面添加, 就可以自动clone, 如果对方更新了, 自己这边也可以方便使用git pull
  微软的这个服务是有网络连接的, 你可以远程下载数据或者导入其他的库. 因此如果出现没有预装的库, 可以自己手动安装. 但麻烦的是, 如果你的notebook停用1小时以后, 远程的server就会停止, 然后你之前安装的东西就会被清除(数据和文件不会), 所以如果有额外的库, 就需要在每次打开的时候预先再次安装一遍.

## [Google Colaboratory](https://colab.research.google.com/)

借助 Colaboratory（简称 Colab），您可在浏览器中编写和执行 Python 代码，并且：

- 无需任何配置
- 免费使用 GPU
- 轻松共享

无论您是一名**学生**、**数据科学家**还是 **AI 研究员**，Colab 都能够帮助您更轻松地完成工作。

# 配置服务器的Jupyter Notebook 以提供服务

## 在服务器段安装Jupyter Notebook (使用Anaconda进行安装比较好)

## 在服务器完成配置

### 生成配置文件

```{Python}
$ jupyter notebook --generate-config
```

### 生成密码

```{Python}
C:\WINDOWS\system32>ipython
Python 3.7.4 (default, Aug  9 2019, 18:34:13) [MSC v.1915 64 bit (AMD64)]
Type 'copyright', 'credits' or 'license' for more information
IPython 7.8.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]: from notebook.auth import passwd

In [2]: passwd() #需要输入密码
Enter password:
Verify password:
Passwords do not match.
Enter password:
Verify password:
Out[2]: 'sha1:9e5b5679bbbf:75d5e60xxxxxa029e798623626e443'
```

### 修改默认配置文件

```{python}
c.NotebookApp.ip='localhost'
c.NotebookApp.password=u'sha1:9e5b5679bbbf:75d5e60xxxxxa029e798623626e443'
c.NotebookApp.open_brower=False
c.NotebookApp.port=5486
c.NotebookApp.allow_remote_access = True
```

### 启动Jupyter Notebook 服务

```{Python}
C:\WINDOWS\system32>jupyter notebook --allow-root --port=5486
[I 21:49:10.477 NotebookApp] JupyterLab extension loaded from C:\ProgramData\Anaconda3\lib\site-packages\jupyterlab
[I 21:49:10.477 NotebookApp] JupyterLab application directory is C:\ProgramData\Anaconda3\share\jupyter\lab
[I 21:49:10.540 NotebookApp] [Jupytext Server Extension] Deriving a JupytextContentsManager from LargeFileManager
[I 21:49:10.605 NotebookApp] Serving notebooks from local directory: C:\WINDOWS\system32
[I 21:49:10.606 NotebookApp] The Jupyter Notebook is running at:
[I 21:49:10.607 NotebookApp] http://localhost:5486/?token=daec549df6f4b10e87033fd57411cd69f1f032024321642a
[I 21:49:10.608 NotebookApp]  or http://127.0.0.1:5486/?token=daec549df6f4b10e87033fd57411cd69f1f032024321642a
[I 21:49:10.608 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 21:49:10.711 NotebookApp]

    To access the notebook, open this file in a browser:
        file:///C:/Users/86150/AppData/Roaming/jupyter/runtime/nbserver-22696-open.html
    Or copy and paste one of these URLs:
        http://localhost:5486/?token=daec549df6f4b10e87033fd57411cd69f1f032024321642a
     or http://127.0.0.1:5486/?token=daec549df6f4b10e87033fd57411cd69f1f032024321642a
```

![ServeUrIpynb](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Skills/Jupyter/ServeUrIpynb.jpg)

但是，默认的路径是`system32`，自然希望直接定位到我的ipynb项目目录。

## 指定Jupyter Notebook访问目录

打开配置文件jupyter_notebook_config.py，全文搜索`notebook_dir`，找到后填入自己的工作路径并保存。（注意：工作路径不能出现中文，否则无法打开Jupyter Notebook）

![ServeUrIpynb-ChangeDirConf](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Skills/Jupyter/ServeUrIpynb-ChangeDirConf.png)

打开新的Anaconda Prompt，运行 `jupyter notebook --allow-root --port=5486`。再出现的目录就是指定的了。

![ServeUrIpynb-ChangeDir](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Skills/Jupyter/ServeUrIpynb-ChangeDir.png)

> 据说可以只改快捷方式的属性：“目标”那里的 “%USERPROFILE%” 删除，“起始位置”改成你希望的路径。
>
> ![ServeUrIpynb-ChangeDirHomepath](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Skills/Jupyter/ServeUrIpynb-ChangeDirHomepath.png)
>
> - 在不改 jupyter_notebook_config.py 文件的情况下，仅改变这两个地方，并不起任何作用。
>
> - 如果改了 jupyter_notebook_config.py，这两个地方都不改的话，从这个快捷方式进入 Jupyter Notebook 会进入默认路径，用 Anaconda Navigator 启动就会进入改变后的路径。对“目标”栏进行改动后，则从快捷方式进入，也会进入修改后的路径。“起始位置”那里的值，改不改都不影响。

> 想截些图，Snagit不能运行，查了下，Windows 自带一些截图的彩蛋呢！
>
> - **快捷键**：`Win + PrintScreen`：使用 `Win + PrintScreen` 快捷键截取全屏画面后，系统会将截图自动保存到「C:\Users\XXX\Pictures\屏幕截图」（XXX 为用户名称）目录下，省下了保存图片文件的操作步骤。
>   - 我的实践中，在使用两个屏幕。`Win + PrintScreen`竟然将它们截到了一起。
>   - ![Capture2Scrns](https://images4git-1301301910.cos.ap-beijing.myqcloud.com/Skills/Jupyter/Capture2Scrns.png)
>
> - **快捷键**：`Win + G`：在 Windows 10 系统中，内置了一项针对游戏的特色截图工具，通过 `Win + G` 唤起简洁的工具条。这个截图工具可以实现在游戏中截取画面，也可以截取其他软件界面。截取的图片会保存在「C:\Users\XXX\Videos\Captures」（XXX 为用户名称）这个文件夹里。

# 客户远程访问

## IP访问

此时应该可以直接从本地浏览器直接访问http://address_of_remote(服务器ip地址):5486就可以看到jupyter的登陆界面。

第一次登陆要求输入账号和密码，账号为服务器端用户名，密码即为刚刚第二步中设置的密码，即可看到目录列表。

## SSH 访问

若上面输入网址无法进入，提示可能是防火墙问题，此时可以通过SSH访问远程服务器， 在Windows下通过xshell等工具访问远程服务器，可在会话中设置，选择属性-ssh-隧道。
