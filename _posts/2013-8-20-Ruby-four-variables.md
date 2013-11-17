---
category: Rubyonrails
layout: post
title: Ruby从入门到精通 学习记录一(ruby四种变量)
---

####Ruby提供了四种类型的变量:

* 局部变量：局部变量是在一个方法中定义的变量,局部变量的变量名以小写字母或_开始。

{% highlight ruby %}
       x = 10
       puts x
{% endhighlight %}

* 实例变量：实例变量是在任何特定的实例或对象的变量，对象的所有方法都可访问对象的实例变量，实例变量的变量名以符号（@）开始。

{% highlight ruby %} 
       class Square
         def initialize(side_length)
           @side_length = side_length
       end
{% endhighlight %}

* 类变量：类变量是在类及所有子对象使用的变量，类变量的变量名以符号（@ @）开始。

{% highlight ruby %}
       class Square
         def initialize
           if defined?(@@number_of_squares)
              @@number_of_squares += 1
           else
              @@number_of_squares = 1
           end
         end
       end
{% endhighlight %}

* 全局变量：类变量是不能跨类，如果你想有一个在当前程序任何位置使用的变量，那你需要定义一个全局变量，全局变量的变量名以美元符号（$）开始。

{% highlight ruby %}
       def basic_method 
         puts $x
       end
       $ = 10
       basic_method
{% endhighlight %}









































