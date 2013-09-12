---
category: Blog
layout: post
title: Ubuntu 12.04 中GoAgent使用教程--轻轻松松翻墙咯
---

{{ page.title }}
================

<p class="meta">2013-9-12 王要佳</p>

### Ubuntu下的配置 

要运行goagent首先必须安装了python，推荐使用python2.7,如果没有python，安装方法：(以下方法选择一种合适的即可)

* 从源安装
   
      sudo apt-get install python

* 从源码安装

      wget http://python.org/ftp/python/2.7.5/Python-2.7.5.tar.bz2 && tar jxvf  
      Python-2.7.5.tar.bz2 && cd Python-2.7.5 && ./configure  --with-zlib &&  
      make && sudo make install 

##### 安装gevent

使用以下命令进行安装

    sudo apt-get install python-dev
<br>
##### 安装pyopenssl

* PyOpenSSL是OpenSSL的python接口，用于提供加密传输支持(SSL)，如果没用该模组，会导致goagent无法生成证书而影响使用。

  * 若系统没有openssl，先安装openssl，一般系统都已安装，可以忽略此步

* 安装pyopenssl（0.13）(以下方法选择一种合适的即可)

  1.从源安装,如果源中有的话

      sudo apt-get install python-openssl

  2.通过python包管理器pip安装

      sudo apt-get install python-pip
      sudo pip install pyOpenSSL

  3.从源码编译安装

      wget http://pypi.python.org/packages/source/p/pyOpenSSL/  pyOpenSSL
      -0.13.tar.gz && tar zxvf pyOpenSSL-0.13.tar.gz && cd pyOpenSSL-0.13  
      && sudo python setup.py install
<br>
##### 安装gtk托盘所需模组

要正常使用gtk托盘，需要安装以下软件包

    sudo apt-get install python-vte
<br>
### 上传GoAgent

[下载goagent](https://nodeload.github.com/goagent/goagent/legacy.zip/3.0)，解压，在终端cd到goagent所在目录下

* 在server目录下，编辑app.yaml文件,把第一行改为application:你创建的appid。然后在server目录下，运行

      python uploader.zip

* 根据提示输入你自己创建的appid（若要同时上传多appid在appid之间用|隔开）和你的Gmail帐号和密码(如果开启了两步验证，密码为16位的应用程序专用密码）

如何创建appid详见[申请Google App Engine并创建appid](http://www.douban.com/note/262773856/),据说一个appid每天流量1G，超了就不能用，次日可以继续使用，所以你要可以多创建一些appid。

说明：在上传时，出现goagent AttributeError: can't set attribute问题，是Gmail之前启用了二次验证的缘故，只要在输入邮箱密码的时候输入应用程序专属密码，就可以上传成功。

### 运行客户端

在local目录下，编辑proxy.ini文件，把[gae]项目的appid修改为你创建的appid。然后在local目录下，运行

    python proxy.py

即可使用代理，也可以赋予proxy.py可执行权限之后直接双击proxy.py。（在proxy.py上面右击，属性的权限中勾选允许以程序执行文件）

直接运行goagent-gtk.py可以使用gtk托盘方式运行goagent。 运行addto-startup.py即可加入开机启动。也可以自行添加一个启动项，命令为

    python /path/to/goagent/local/goagent-gtk.py

其中路径修改为自己系统中goagent-gtk.py的路径

说明：在运行客户端时，出现"UnicodeDecodeError:'ascii' codec can't decode byte"问题,是python的编码问题,要在终端下使用中文环境，那么要声明unicode的 UTF-8方式编码 打开你的proxy.py文件，在开头添加：

    import sys
    reload(sys)
    sys.setdefaultencoding('utf-8')

问题就解决了。

### 使用chrome浏览器

先安装chrome浏览器，然后安装SwitchySharp插件，最后导入这个设置<http://goagent.googlecode.com/files/SwitchyOptions.bak>

导入文件是指在SwitchySharp插件选项中的导入/导出设置，从文件恢复，选择刚才下载的.bak文件。

### 退出

* 如果是直接终端使用"python proxy.py"运行，在终端按"Ctrl+C"组合键可终止运行

* 如果使用gtk托盘，在托盘图标上右键菜单有退出选项

* 直接关闭终端窗口也会退出

* 如果以后台进程运行，先用"ps aux | grep proxy.py"找到goagent的PID，然后直接kill对应的PID

      ps aux|grep proxy.py|grep -v "grep"|awk '{print $2}'|xargs kill



    















