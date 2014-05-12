---
layout: post
title: Mac os Goagent 设置总结
category : 电子数码
tags : [翻墙]
---

由于最近的净网行动，这两天Mac上的翻墙利器「鱼摆摆」被和谐了，无奈只能找新的替代品了。类似于「鱼摆摆」这样的软件，一段时间后用得人多了总会被和谐，目前比较稳定可靠的只能选择goagent了。Google App Engine是一个开发、托管网络应用程序的平台，使用Google管理的数据中心。它在2008年4月发布了第一个beta版本。Google App Engine使用了云计算技术。它跨越多个服务器和数据中心来虚拟化应用程序。不过goagent初次配置比较麻烦，小白用户第一次配置可能比较困难，两年前我在windows上折腾过，当时并没有成功。现在打算在Mac上配置，心里也是得没底。之前查阅了一些关于Mac上配置goagent的帖子，但看过之后还是有点云里雾里。本想找机房「小王老师」请教下，但今天他有事情，只好自己折腾了。

刚开始选择了最简单的方式，直接采用Mac下无需命令行操作的GUI界面的GoagentX，按照[这个帖子](http://iaiai.iteye.com/blog/1608369)上的步骤操作还算顺利，我之前已经申请了Google Appengine的账号，这一步就省了。按照帖子上的步骤部署好之后，goagent已经能正常运行。不过在用chrome浏览器上网时，碰到了一些问题。首先，chrome浏览器必须配合插件[SwitchySharp](https://code.google.com/p/switchysharp/)才能使用代理翻墙，按照网上教程填写好[SwitchySharp](https://code.google.com/p/switchysharp/)设置后，依然不能成功上YouTube，在chrome上试了很多次还是不行。无意间用safari浏览发现能上YouTube，猜测这应该是浏览器的问题，网上查询发现可能是证书导入的问题。又按照说明，导入了goagent的证书，发现在chrome上可以上YouTube了。不过网速很慢，不管它只能先用着了。后来，由于我安装的GoagentX比较低，就试着升级了，结果出现问题。升级后回到宿舍又不能翻墙了，配置失败，提示如下：
> WARNING - [xxxx] Load Crypto.Cipher.ARC4 Failed, Use Pure Python Instead.

查询之后发现是启动本地代理，可能出现的问题。
这个需要安装pycrypto，按照下述步骤即可。
`wget http://pypi.python.org/packages/source/p/pycrypto/pycrypto-2.0.1.tar.gz#md5=277aa00f27cfbb08f21063f4beb6de59`
`tar -zxvf pycrypto-2.0.1.tar.gz`	
`cd pycrypto-2.0.1`		
`python setup.py build`		
`sudo python setup.py install`

解决了上述问题之后，使用GoagentX还是有问题，不知道是不是校园网的问题。思考之后，最终选择了采用命令行直接部署goagent。没想到在Mac上很容易就成功了。大致步骤如下：

1. 申请Google Appengine并创建appid。（这个步骤我之前已经做过，网上很多教程）	
2. 下载[goagent稳定版]( http://code.google.com/p/goagent/)  	
3.  修改local\proxy.ini中的[gae]下的appid=你的appid(多appid请用|隔开)，具体步骤如下：
> 1) 解压goagent-3.0.zip，文件夹改名为goagent，复制文稿根目录	
> （也可以放到别的目录，只是注意更改下面步骤中终端指令的文件夹路径）	
> 2) 找到goagent目录里的local目录下proxy.ini文件，右击->打开方式->其他->文本编辑.app 打开
	
4.  在server目录下运行"python uploader.zip"(没有引号)，具体步骤如下：
> 打开应用程序->实用工具->终端.app	
> 命令pwd为查看当前在哪个目录，ls为查看当前目录下有什么文件，cd documents为进入当前目录下的documents目录	
> 1) 如果把goagent文件夹放在文档根目录,则输入 `cd /users/（用户名） /documents/goagent/server` 回车进入server目录	
> 2) 输入 `python uploader.zip` 回车根据提示输入APPID后等待(多appid请用|隔开)，运行一会后会提示输入注册的邮箱地址和密码	
> 直到出现Completed update of app:你的APPID,version: 1为止	
> 3) 命令行继续输入`cd /users/（用户名）/documents/goagent/local` 回车到达local目录	
> 4) 再输入`python proxy.py` 回车看到你的账号信息为成功	
> 如果出现这个错误：*WARNING - - [Jan 22 16:31:01] GoAgent install certificate failed, Please run proxy.py by administrator/root/sudo*	
> 就先不管了。你现在不是管理员账号，装证书失败。

5. 上传完服务端并设置好proxy.ini之后，在终端直接运行`python proxy.py`即可。需要Python版本2.6以上。	
6. chrome浏览器安装SwitchySharp插件，然后导入这个[设置](http://goagent.googlecode.com/files/SwitchyOptions.bak)

这样基本上就大功告成了，你终于自由了，外面的世界任你你探索，YouTube上有很多非常好的学习视频。最后，我一般只在浏览器上用代理，所以上面的设置目前只是在chrome浏览器上实现了翻墙，如果想使用全局代理，只需要在Mac的系统偏好设置->网络->代理中简单设置下就IP和端口就可以了。	
以后每次用的时候，只需要在终端里输入`python proxy.py`（记住终端不能关！），然后开启插件，选择goagent，就可以使用了，也就是：开终端-->开插件-->上网！不用的时候，关掉终端，插件选择最上面的“直接连接”选项，就可以了。	
如果想开机启动goagent，在终端运行 `sudo python goagent/local/addto-startup.py` 然后再运行 `sudo launchctl load /Library/LaunchDaemons/org.goagent.macos.plist` 即可（前面的路径修改成自己电脑上goagent的路径）。这样你就不用每次开机都打开终端输入命令，goagent就在后台默默地为你提供支持了，你可以无缝使用chrome翻墙了。
### 优酷上的视频教程（windows版）
<iframe height=498 width=510 src="http://player.youku.com/embed/XNjcwNzU5Nzgw" frameborder=0 allowfullscreen></iframe>