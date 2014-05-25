---
category: Tools
layout: post
title: 解决ThinkpadT440p无线网卡驱动问题-Ubuntu13.10
---

新入手ThinkpadT440p本本，安装ubuntu13.10后，发现无法使用网线上网。找了好久才发现如下解决办法：

### 1. 下载驱动文件
{% highlight ruby %} 
$ wget https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1239578/+attachment/4057550/+files/rtl_92ce_92se_92de_8723ae_88ee_8723be_92ee_linux_mac80211_0017.1016v2.2013.tar.gz
{% endhighlight %} 

### 2. 解压驱动文件
{% highlight ruby %} 
$ tar zxf rtl_92ce_92se_92de_8723ae_88ee_8723be_92ee_linux_mac80211_0017.1016v2.2013.tar.gz
{% endhighlight %} 

### 3. 进入驱动文件目录
{% highlight ruby %} 
$ cd rtl_92ce_92se_92de_8723ae_88ee_8723be_92ee_linux_mac80211_0017.1016v2.2013
{% endhighlight %} 

### 4. 安装驱动文件
{% highlight ruby %} 
$ sudo make && make install
{% endhighlight %} 

### 5. 挂载新驱动文件
{% highlight ruby %} 
$ modprobe rtl8192ee
{% endhighlight %} 

完成以上操作，就可以搜到WIFI信号，连接无线网络上网。

参考：[L137's Blog](http://www.cnblogs.com/l137/p/3679279.html)


