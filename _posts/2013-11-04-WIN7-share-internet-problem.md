---
category: Tools
layout: post
title: WIN7中设置Internet连接共享保存时出现(null)错误
---

在WIN7中设置Internet连接共享，点击确定出现"Internet连接共享访问被启用时，出现了一个错误(null)"。

这个大多数都是没有启用'windows firewall'服务导致的，因为360安全卫士会禁用掉，只要手动启用就正常了。

手动启用的方法很简单：

* 点击开始按钮——搜索框中输入：服务，回车打开服务管理界面。

* 找到'windows firewall'服务，点击启动即可。
    















