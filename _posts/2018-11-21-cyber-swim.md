---
layout: post
title: 上外网（查阅资料）的几个方法 - Liang
date: 2018-11-21 17:02:12.000000000 +08:00
tags: host, Linux, Windows
---

1. 作为一名研究生，查阅文献，看文献甚至是发文献都是必不可少的。在这种情况下，谷歌学术(`https://scholar.google.cn`)当然是我们必不可少的辅助工具。
	
	什么？你说知网就够了？我都写英文文章了，你不可能比我还渣吧~

2. 首先，最简单的方法就是修改hosts了，但这个方法仅限ipv6下。由于多数高校都是ipv6环境，所以这也是我的第一选择。想知道自己的网络是否ipv6,点击[这里](http://test-ipv6.com/)

修改hosts步骤如下：

第一步，找到本机的hosts文件,将文件备份（可做可不做，本来hosts里面也没什么东西）

对Windows用户：该文件目录在

    C:\Windows\System32\drivers\etc  

	 
mac或linux用户
该文件目录在

    /etc/hosts

第二步，下载新的[hosts文件](https://github.com/lennylxx/ipv6-hosts/blob/master/hosts)，并将其复制到之前hosts文件目录下。

在[老D博客](https://laod.cn/hosts/)处下载也可以，但不知为什么对我来说他的版本上网好像慢一些，所以我还是推荐下载上面的hosts。

对window用户，将这个文件复制到上面写的路径即可。mac，linux同理。

测试：点击打开上面谷歌学术网的链接，能看到熟悉的"站在巨人的肩膀上"就可以了:

    
![有帮助的截图](raw/master/assets/images/screen3.png)

3. 如果没有ipv6,也有解决办法: 用隧道。

	原理大致如下，境内设备与境外机器通讯，境内想看什么网页，就告诉境外的机器，让境外机器代理抓取，然后送回来。其中有名的有`shdowsocks，xx-net`。也都有Android和IOS版本，此处特别推荐[xx-net](https://github.com/XX-net/XX-Net)，简单，大流量，重要的是，for free！

4. 再有就是各种各样的翻墙工具了，这部分就是八仙过海，五花八门的软件都有，此处不做推荐了。

最后，再次向开源世界致敬。还有就是，我们在拥抱自由开放世界的同时，也要明白到，开源，甚至于破解和用盗版，其实都是不可持续的。



