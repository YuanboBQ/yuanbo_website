---
layout: post
title: Github博客有关的git命令
category : 电子数码
tags : [Github, Blog]
---

Github博客有关的git命令

使用Github pages可以像hacker一样发布blog，这里总结一下和发布博客有关的最常用、最基本的git命令。

git是一个版本控制系统。官方的解释是:
> 版本控制(Revision control)是一种软件工程技巧,籍以在开发的过程中,确保由不同人所编辑的同一档案都得到更新。

用个通俗的比喻你可以理解为:	
	
> 一群志同道合的人身处祖国各地,希望来合作开发一个项目（比如这个项目是使用 c 语言写的，当然用任何语言都可以的)。那么大家怎么合作呢?用信件?效率太低。用邮件，不好实现多人沟通。用 google group 吧,可开发阶段中的源代码没法科学管理。用自建的网站吧，需要人力物力财力来支撑。这个时候版本控制系统就派上用场了。它可以让一个团队里的不同的人在不同地点、不同时间开发和改进同一个项目，并且在大部分的时间里，版本控制系统会聪明的帮你把不同的人在不同地点不同时间修改的代码融合到项目中去。

git常用命令：	
`$ mkdir tmp      //创建推送目录`		
`$ cd tmp         //进入推送目录` 	   
`$ git init       //设置该目录为推送`		
`$ touch README   //生成readme`		
`$ git add README //加入修改列表`		
`$ git commit -m 'first commit'//递交修改声明`
`$ git remote add origin git@github.com:abcd/tmp.git //为远程Git更名为origin`		
`$ git push -u origin master //推送此次修改 `

我们在电脑上写完或者修改blog之后，一般会用到如下命令把新的blog提交到github上。
`$ git add .`	
`$ git commit -m "Add new content"`	
`$ git push origin master`
使用`git add `添加要提交的具体文件，`git add .`这个命令要求 git 给目前的这个项目制作一个快照，也可以用`git add -i`来智能添加文件。修改完blog或者文件后，使用`git status`可以查看文件的差别，之后`git commit`提交本次修改，`git push`上传到github。 