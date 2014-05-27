---
category: Tools
layout: post
title: Ubuntu中创建Android手机识别Wifi
---

用Ubuntu系统自带功能创建AP操作是非常简单，但大多数Android手机都搜索不到它的信号，那是因为Android一般都不支持Ad-hoc模式的Wifi。为了在Ubuntu中创建一个Android手机能够识别的AP,下面向大家介绍另外一种方法： 

{% highlight ruby %}
$ sudo add-apt-repository ppa:nilarimogard/webupd8
$ sudo apt-get update
$ sudo apt-get install ap-hotspot
$ sudo ap-hotspot configure  //这一步会检查ubuntu的网络和WIFI接口，确定后会提示你配置热点，输入ssid和密码等内容
$ sudo ap-hotspot start
{% endhighlight %} 

完成以上步骤，Android手机顺利识别Wifi并连接。(但是不知到什么原因，连接上不是很稳定。)

参考：[Young++ workspace](http://blog.csdn.net/olanmomo/article/details/16922565)
