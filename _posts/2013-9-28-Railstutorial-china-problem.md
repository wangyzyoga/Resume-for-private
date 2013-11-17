---
category: Rubyonrails
layout: post
title: Ruby On Rails教程中遇到几个问题
---

这两周断断续续在跟着[Ruby On Rails教程](http://railstutorial-china.org/)实战练习，最终会做成一个拥有用户注册/登录/发微博等功能简单应用程序。

目前我看到第6章节，完成部分的代码已经上传[GitHub](https://github.com/wangyzyoga/sample_app)。现在把练习过程中遇到的3个问题进行整理，希望可以帮助遇到类似问题的人。

### 1.Gemfile中Gem版本兼容问题

本书推荐使用Ruby：2.0.0，Rails：4.0，我电脑上的环境是Ruby:1.9.3，Rails:3.2.13，这就会导致一些高版本内容不支持低版本情况。如果直接复制第3章-基本静态页面中Gemfile的内容，并运行‘bundle install’时会出现问题。

大家根据错误提示，修改Gemfile对应Gem的版本即可。

###2.Rails 路由设置

书中5.3.2章节中提到添加根地址的路由设置：

    SampleApp::Application.routes.draw do
      root to: 'static_pages#home'
      .
      .
      .
    end

上面的代码会把根地址/映射到/static_pages/home页面上，也就是让http://localhost:3000/指向/static_pages/home。

我按照书中介绍进行配置后，死活都无法实现输入http://localhost:3000/，展现/static_pages/home内容。折腾了两三天后，我突然想起之前在“Ruby从入门到精通”里面看到要更改首页，除了更改路由设置，还需要把rails默认首页删除才行。将sample_app/public路径下的index.html文件删除后，首页就指向/static_pages/home。

###3.动态find_by的变化

书中6.3.3章节中提到用户身份验证时，需要调用find_by方法：

    User.find_by(email: email)

通过Email地址查找用户记录。

当我使用上述方案调用find_by方法时，老提示：没有定义find_by方法。后来在网上查询原因才发现，书中的写法是Rails4.0的用法，Rails3.x的用法应该是这样的：

    User.find_by_email(@user.email)

更多升级到Rails4.0的说明，详见<http://www.oschina.net/translate/get-your-app-ready-for-rails-4>。











    















