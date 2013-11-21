---
category: Tools
layout: post
title: SublimeText2不能输入汉字解决办法
---

网上都说SublimeText2用着不错，但是我在ubuntu下安装后，发现不能输入中文，着实不方便。今天在网上看到解决办法，拿出来分享下：


###首先，在SublimeText2的菜单栏 -> Preferences -> Settings - User，在配置文件中增加：

{% highlight ruby %} 
    // Settings in here override those in "Default/Base File.sublime-settings", and

    // are overridden in turn by file type specific settings. Place your settings

    // here, to ensure they're preserved when upgrading.

    {
         "font_face": "WenQuanYi Micro Hei Mono"
    }
{% endhighlight %}

###其次，我们来解决中文输入的问题

{% highlight ruby %} 
    sudo apt-get install scim

    sudo apt-get install scim-pinyin
{% endhighlight %}

###在“系统－语言支持”设置里

Keyboard input method system 选“scim-bridge”

###在“系统－首选项－scim设置里”

scim设置－>全局设置－>将预字符串嵌入到客户端中 勾去掉

scim设置－>gtk－>嵌入式候选词标 勾去掉

记得这些修改完要注销重新登录进来,或者打开终端,输入 pkill scim,然后输入 scim -d

如果不起作用，那还是建议注销一下。

**坑爹啊，也不知道哪一步出问题，重启后又回复到原来输入法，怎么也切不回去，无解！**

###原文链接
<http://www.linuxidc.com/Linux/2012-06/62944.htm>
<http://www.cnblogs.com/QLeelulu/archive/2011/12/30/2308084.html>