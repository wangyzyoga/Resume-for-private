---
category: Blog
layout: post
title: 使用OmniAuth调用Github时provider参数设置
---

{{ page.title }}
================

<p class="meta">2013-11-07 王要佳</p>

跟着[Railscasts](http://railscasts-china.com/episodes/omniauth-1)学习OmniAuth调用Github时，遇到如下代码：

    Rails.application.config.middleware.use OmniAuth::Builder do
      provider :github, 'key', 'secrets'
    end

不知道代码中key与secrets两个参数在Github中如何找到，Google/百度各种搜索，折腾1个多小时没解决。

最后还是在[RubyChina社区](http://ruby-china.org)找到帮助，具体方法如下：

* 使用github帐号登录到github主页面，点击‘Edit Your Profile’

* 在Profile页面左侧，点击‘Application’

* 在Application页面右侧，点击‘Register-new-application’,填写Oauth－application的名字/URL/callbackURL,我的信息是这样填写的:

      Application name
      Omniauth

      Homepage URL
      http://localhost:3000

      Authorization callback URL
      http://localhost:3000/auth/github

* 最后点击‘Register-application’，页面就会出现ClientID/ClientSecret的信息

* 用ClientID替换key,ClientSecret替换secrets即可

    















