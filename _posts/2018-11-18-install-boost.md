---
layout: post
title: Linux中安装boost库 - Liang
date: 2018-11-18 22:38:08.000000000 +08:00
tags: Linux
---

最近因为模拟需要，要Linux中安装boost库，而且是1.38的远古版本。Google了一番，发现教程多数是新版本的，或者是英文版本的，故此在这里发一遍1.38版本的，避坑专用～

Linux的流畅度，还有权限管理也给我留下了很深刻的印象。
同时，这次经历也让我感到了Linux下安装个东西实在是……#@f#u￥c%k！


### 1.准备 

首先要知道我们的程序性质是什么，要运行他又要安装什么包。

键入：  

    $ file GLAK_1.0.0_Linux 

显示：

    GLAK_1.0.0_Linux: ELF 64-bit LSB  executable, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.4.0, not stripped

`x86_64` 代表程序是64位的

键入：  

    $ ldd GLAK_1.0.0_Linux

显示：

{% highlight c %}
linux-vdso.so.1 =>  (0x00007ffd8b12a000)  
libboost_filesystem-gcc34-mt-1_38.so.1.38.0 => not found  
libboost_system-gcc34-mt-1_38.so.1.38.0 => not found
libstdc++.so.6 => /usr/lib/x86_64-linux-gnu/libstdc++.so.6 (0x00007ff560540000)
libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007ff56023a000)	libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007ff560024000)
libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007ff55fc5f000)
/lib64/ld-linux-x86-64.so.2 (0x00007ff560844000)
{% endhighlight %}

我们要解决的，就是显示"`not found`"的这两个文件了。

可以看出，缺少的是用`gcc 3.4`编译的`boost 1.38`。看来一场恶战不可避免了~

### 2. 下载安装包
没什么说的，下一步当然是先下载[boost_1_38_0.tar.bz2](http://sourceforge.net/project/showfiles.php?group_id=7586&package_id=8041)

### 3. 安装gcc。
我这边要求的gcc版本是3.4，在`ubuntu`的[归档页面](http://old-releases.ubuntu.com/ubuntu/pool/universe/g/gcc-3.4/)下载下面五个文件

>     cpp-3.4_3.4.6-6ubuntu3_i386.deb
>     
>     g++-3.4_3.4.6-6ubuntu3_i386.deb
>     
>     gcc-3.4_3.4.6-6ubuntu3_i386.deb
>     
>     gcc-3.4-base_3.4.6-6ubuntu3_i386.deb
>     
>     libstdc++6-dev_3.4.6-6ubuntu3_i386.deb

需要注意的是，上面几个文件后缀i386表示32位。这个我直到最后才发现这个【泪】，后面搞了几天的一大堆问题应该就是出自这里，因此又回来重新下载了。

我的系统是64位的，对于我来说，真实需要下载的是
>     cpp-3.4_3.4.6-6ubuntu3_amd64.deb
>     
>     g++-3.4_3.4.6-6ubuntu3_amd64.deb
>     
>     gcc-3.4_3.4.6-6ubuntu3_amd64.deb
>     
>     gcc-3.4-base_3.4.6-6ubuntu3_amd64.deb
>     
>     libstdc++6-dev_3.4.6-6ubuntu3_amd64.deb

也可以在gcc官网直接找压缩包解压安装。

然后安装 `gcc3.4`

    $ cd gcc-3.4  #进入文件目录
    $ sudo dpkg -i *.deb #安装所有.deb文件

不行的话，使用  

    $ sudo dpkg --force-depends -i *.deb  
来安装

安装完成之后最好先用  

    $ ls /usr/bin/gcc* -ll  
看一下当前安装的gcc的各个版本，来检测下是否安装成功，再出什么幺蛾子的话，请自行谷歌，我也没办法，哈哈

一切正常的话安装完成之后，在系统里会多出：gcc-3.4

目前系统里有两个版本的gcc，缺省时gcc4.8；需要改变系统的缺省配置：

增加gcc3.4和gcc4.8可选项

    $ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 40
    $ sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-3.4 30

这后边的30和40分别是各版本的优先级

切换版本到gcc-3.4
    
    $ sudo update-alternatives --config gcc

现有 2 个可选项，它们都提供了“gcc”

    <选择可选项-----------------------------------------------
      1    /usr/bin/gcc-3.4*+

      2    /usr/bin/gcc-4.8

要维持缺省值[*]，按回车键，或者键入选择的编号：1

使用“/usr/bin/gcc-3.4”来提供“gcc”。

至此gcc3.4.6安装成功

ps：整完后，如果系统找不到g++，可以自己安装一下g++：

    $ sudo apt-get install g++

### 4. 一顿头昏脑涨之后，跟着boost的Getting Started on Unix Variants开始安装boost

一开始先安装依赖

	$ apt-get install mpi-default-dev libicu-dev python-dev python3-dev libbz2-dev zlib1g-dev

首先解压

    $ tar --bzip2 -xf /path/to/boost_1_38_0.tar.bz2
注意这里的/path/to要换成你自己的目录，一般放在/usr/local里面

你可以使用mv命令进行文件的移动，此处不详细说  

然后，进入目录进行安装：

    $ cd path/to/boost_1_38_0

首先安装HEAD ONLY库，说是安装，其实就是讲boost的目录软连接到系统目录

    $ sudo ln -s /usr/local/boost_1_38_0/boost boost

再就是安装需要单独编译的库，库的名单在网站上有  

下面这个命令是看设置的一些东西

    $ ./configure --help
例如你可以指定用gcc编译（我就是这么干的）

    $ ./configure --with-toolset=gcc 3.4
    $ make install

我在这一步折腾了不少时间。。。一直提示我说failed或者passed。
  
然后，解决办法就是，我又重新安装了一遍！哈哈哈哈！！

最后终于发现了，也是位数的问题。提示是：

    /usr/bin/ld: 找不到 crt1.o: 没有那个文件或目录
    /usr/bin/ld: 找不到 crti.o: 没有那个文件或目录
    /usr/bin/ld: 找不到 -lgcc_s
    collect2: ld returned 1 exit status

在配置的时候，电脑认为要编译32位的程序，系统中64位的GCC当然不兼容。那么怎么让系统编译64位的呢？

首先，我们要找到电脑中的上述文件到底在哪

    $ find /usr/ -name crti*
    $ find /usr/ -name crt1*

找到之后，添加路径到系统路径就行了～
    
    $ export LIBRARY_PATH=/usr/lib/x86_64-linux-gnu:$LIBRARY_PATH

### 5. 安装成功（Finally！）
重装无数次，sudo apt install和uninstall无数次，从deepin换到ubuntu，我总算成功了。这次安装事件对我的启发是：想折腾linux的话，还是不要用deepin了。出了问题一Google，得出的结果都是ubuntu的。其实换一个方面看，由此看出deepin的用户真的不折腾...哈哈

这之后，如果让我deepin，ubuntu二选一的话，毫不犹豫ubuntu（对不起，国产deepin）。

### 6. 有库文件的安装方法
下面说说最简单的方法：编译出库文件之后，直接复制下来，就可以应用在另一台电脑上。我就是这么移植过去的，一开始还以为要再重复一遍上面的过程。。。

总之，就是不管做了什么关于library的变动后，最好都ldconfig一下，不然会出现一些意想不到的结果。不会花太多的时间，但是会省很多的事。

也有可能，就是在你复制的时候，没有给文件"read"的权限，导致ld找不到库文件，针对这种情况，可以找到库文件，之后用这行代码：

    $ ls -l filename

查看文件属性

如果有错，例如我的是

	-rw------- 1 root root 84992 11月 21 21:24 libboost_filesystem.so.1.40.0

表示仅所有者有读和写的权限，组用户没有权限

因此我们可以用

    $ sudo chmod 644 ××× （所有者有读和写的权限，组用户只有读的权限）

例如我就用这两行代码完成了编辑

    $ sudo chmod 644 libboost_filesystem.so.1.40.0 
    $ sudo chmod 644 libboost_system.so.1.40.0
    
再查看：

    $ ldd GLAK_1.0.0_Linux_ps 

显示：

	linux-vdso.so.1 =>  (0x00007ffcbf938000)
	libboost_filesystem.so.1.40.0 => /usr/lib/x86_64-linux-gnu/libboost_filesystem.so.1.40.0 (0x00007f9397b7d000)
	libboost_system.so.1.40.0 => /usr/lib/x86_64-linux-gnu/libboost_system.so.1.40.0 (0x00007f9397979000)
	libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007f939736f000)
	libgomp.so.1 => /usr/lib/x86_64-linux-gnu/libgomp.so.1 (0x00007f9397160000)
	libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007f9396f4a000)
	libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007f9396d2c000)
	libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f9396967000)
	librt.so.1 => /lib/x86_64-linux-gnu/librt.so.1 (0x00007f939675f000)
	/lib64/ld-linux-x86-64.so.2 (0x00007f9397d92000)

就全都能找到了。

对于可执行文件执行不了的情况，也有解决办法。首先也是cd到目录中用

    $ ls -l filename

查看列表显示的文件属性

再和上面过程一样改文件属性，应该就可以了。

当然也可以在图形界面上再确认下是否设置正确了：

![有帮助的截图](assets/images/screen2.png)


### 7. 补充：
一路来踩坑不少，感谢Dr.Qian、CSDN、stackoverflow还有Google等等，有了他们我才能完成安装。感谢陈绮贞，在这个过程中是听着陈老师的歌完成的，没有她，我可能早抓狂了（3月陈老师要来开演唱会啦，开心）。还有一个原因就是研究生要毕业【泪】。现在再看下上面写的文字，感觉戾气很重。不过再让我改文字是不可能的了～  
（完）