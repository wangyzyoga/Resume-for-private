---
category: Rubyonrails
layout: post
title: Ruby中yield的用法
---

在Ruby语言中，yield方法能自动检测传递给它的代码块，并将控制权移交给该代码块。简单说yield就是占位符，先在前面的某部分代码中用yield把位置占着，然后才在后面的某个代码块(block)里真正实现它,从而完成对号入座的过程。
    
例如：

{% highlight ruby %}
    def each_vowel
      a = %w{ a e i o u }
      a.each { |vowel| yield vowel } #yield先占位，至于具体实现什么功能，暂时不知道
    end
    
    each_vowel { |vowel| puts vowel } #该处就是上面yield具体实现功能
{% endhighlight %}

运行结果：

{% highlight ruby %}
    a
    e
    i
    o
    u
{% endhighlight %}