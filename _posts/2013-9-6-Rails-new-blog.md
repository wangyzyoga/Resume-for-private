---
category: Rubyonrails
layout: post
title: Rails4.0建立博客遇到问题一
---

今天开始跟着[Rails初上手指南](http://guides.ruby.tw/rails3/getting_started.html)学习建立博客，遇到如下两个问题。

###1. rails new blog时，总是卡在:

{% highlight ruby %} 
    run bundle install
{% endhighlight %}

解决办法：

{% highlight ruby %}     
    rails new blog --sikp-bundle
    cd blog
    bundle install --local
{% endhighlight %} 

###2. rails server时，报错提示:

{% highlight ruby %} 
    Could not find a JavaScript runtime
{% endhighlight %}

解决办法:在blog文件夹下的Gemfile文件中加入

{% highlight ruby %} 
    gem 'therubyracer'
    gem 'execjs'
{% endhighlight %} 

运行'rails server'后，在浏览器输入http://127.0.0.1:3000，应该就会看到Rails的预设首页。
 















