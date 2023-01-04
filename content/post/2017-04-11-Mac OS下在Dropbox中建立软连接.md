---
title:  Mac OS下在Dropbox中建立软连接
author: yuanbo
date: 2017-04-11
slug:  Dropbox-soft-links
category:   
tags: 
---

## 背景

需要同步到Dropbox的内容都得放置在一个文件夹里面，默认名字叫"Dropbox"。

## 问题

实际情况是：许多文档，代码等已经放置在其他相关的文件夹里面了。如果搬到"Dropbox"文件夹中，会给管理带来麻烦。如果不搬到“Dropbox”中，怎么样让Dropbox也能够自动的及时更新这些备份呢？

## 解决：

要用到软连接： ln -s 实际所在的路径及名字     **希望所在的路径及名字** 。具体命令如下（需要把 xxx替换成自己的用户名）：
``` bash
ln -s /Users/yuanbo/Work\ and\ Study/R_learning/R\ Working\ Directory/yuan_blogdown/mywebsite/docs /Users/yuanbo/Dropbox/应用/updog/yuanbo
```