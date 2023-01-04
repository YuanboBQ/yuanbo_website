---
title:  Psychopy 学习记录
author: yuanbo
date: 2017-04-15
slug: Psychopy-study-note
category:   psychopy-note
tags: 
---

最近在群里看到王治国老师关于 psychopy 的教程，又燃起了我学习 psychopy 的热情。昨天晚上折腾了很久，自己手动安装了 psychopy 的程序，现在可以完全不依赖 standalone 版运行编写的程序。记录下中间遇到的一些坑，以及一些有用的命令。

## python 基础知识


## [手动安装 psyhcopy](http://psychopy.org/installation.html)

### [wxPython] (https://wxpython.org/download.php)的安装
wxPython 我下载了安装软件，但是一直在 mac 上无法正常安装
尝试使用 ``pip install wx``命令安装，也未能成功。
最后试了下使用``brew install wxpython``竟安装成功了。


### 安装下面的依赖包

使用下面命令安装各种依赖包，为了避免可能出现错误，我把命令进行了分割安装。

```
pip install xlrd configobj pyyaml gevent greenlet msgpack-python 
pip install psutil tables requests[security] pyosf cffi pysoundcard 
pip install  tables 
pip install psutil  requests[security] pyosf cffi pysoundcard 
pip install pysoundfile seaborn psychopy_ext python-bidi
pip install psychopy
pip install pyserial pyparallel egi iolabs
pip install pytest coverage sphinx
```

不知道为什么安装 ``pip install  tables`` 总是出现问题，目前还没是有解决这个问题。不过暂时还用不到 tables 这个模块，也懒得处理它了。安装好上面的依赖包之后，还需要再安装下面几个包（psychopy 依赖的包还真是多）。


#### Needed on Mac OS X:

``pip install pyobjc # takes a while!``

#### Handy extra options:

```
pip install seaborn  # nice graphing
pip install psychopy_ext  # common workflows made easy
pip install python-bidi  # for left-right language formatting
```

## 关于呈现中文显示不正常问题

默认情况下 psychopy 呈现中文会出现一些问题，要在代码的最前面加上这样一段语句``# -*- coding: utf-8 -*-``。并且在用到呈现中文的文本前面加上``u``。另外就是要在呈现文本的语句中指定中文字体。示例如下：

```
脚本.py文件第一行加上上面这一句 
# -*- coding: utf-8 -*- 
定义文本的时候加u 
msg1 = visual.TextStim(myWin, text=u"实验结束，谢谢!", pos=(0,0), color='red', bold=True, height=18, font ='Microsoft YaHei') 
```



有时间再慢慢学习 psychopy 吧，假期把现在用到的 eprime 程序都迁移到 psychopy 上，以后做实验就会方便多啦。
