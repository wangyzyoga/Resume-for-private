---
category: Rubyonrails
layout: post
title: Rails4.0 建立博客遇到问题一
---

{{ page.title }}
================

<p class="meta">2013-9-6 王要佳</p>

今天开始跟着[Rails初上手指南](http://guides.ruby.tw/rails3/getting_started.html)学习建立博客，遇到如下两个问题。

#####1. rails new blog时，总是卡在 'run  bundle install'

解决办法：
    
    rails new blog --sikp-bundle
    cd blog
    bundle install --local
<br>
#####2. rails server时，报错提示 'Could not find a JavaScript runtime'

解决办法:在blog文件夹下的Gemfile文件中加入

    gem 'therubyracer'
    gem 'execjs'

运行'rails server'后，在浏览器输入http://127.0.0.1:3000，应该就会看到Rails的预设首页。
 















