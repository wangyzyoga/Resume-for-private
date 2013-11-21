---
category: Rubyonrails
layout: post
title: HTML初步学习 
---

我的博客已基本搭建成功，可以写博客，也增加评论功能。但是我觉得整体功能还是不太友好，比如页面的格局不是我想要的，没有常见的日历/博客分类功能，也没有go_top功能等。随着时间推移，要是内容增多，就很不方便管理。

我讲下决定要暂时放下修改博客功能，快速系统学习HTML的原由。我在现有博客基础上，第一个意识要加的功能其实是go_top功能。因为我本身是做软件实施的，了解现场客户一些基本心里与需求。像这个满足基本功能后，下来要考虑的便是如何让客户用的舒服，享受使用的过程。于是我使用Chromuim浏览器，抓取到别人页面的go_top代码，试着放进自己的代码中，但是发现根本没有达到希望功能。我意识到，还是需要快速学习基础知识，一味的模仿，而不去学习的人，无法进行创新。此处说的有点大，呵呵。

[W3Shool](http://www.w3school.com.cn/html/)是一个学习HTML基础知识的好地方，当然这里还有很多其它方面的内容，做的都很好，以后再讲。抽了两天时间，把HTML基础教程快速学习一遍，现在将主要内容整理出来:

###HTML 基础

{% highlight html %}
     <html>
     <head>
     <title>文档名称</title>
     </head>
     <body>
     文档内容
     </body>
     </html>
{% endhighlight %}

###TEXT 元素

{% highlight html %}
     <p>文档段落</p>
     <br>换行
     <hr>水平线
     <pre>定义预格式化的文本</pre>
{% endhighlight %}

###HTML 逻辑格式，向浏览器传达强调的消息

{% highlight html %}
     <em>斜体字</em>
     <strong>字体加粗</strong>
     <code>表示计算机源代码或者其他机器可以阅读的文本内容</code>
{% endhighlight %}

###HTML 物理格式，只是告诉浏览器的对文字操作

{% highlight html %}
     <b>字体加粗</b>
     <i>斜体字</i>
{% endhighlight %}

###HTML 链接/锚/图片

{% highlight html %}
     <a href="http://www.example.com/">这是一个链接</a>
     <a href="mailto:webmaster@example.com">发送邮件</a>
     <a name="tips">Useful Tips Section</a>
     <a href="#tips">Jump to the Useful Tips Section</a>
     <a href="http://www.example.com/"><img src="URL"
     alt="破图后替换的内容"></a>
{% endhighlight %}

###HTML 无序清单

{% highlight html %}
     <ul>
     <li>First item</li>
     <li>Next item</li>
     </ul>
{% endhighlight %}

###HTML 有序清单

{% highlight html %}
     <ol>
     <li>First item</li>
     <li>Next item</li>
     </ol>
{% endhighlight %}

###HTML 定义清单

{% highlight html %}
     <dl>
     <dt>First term</dt>
     <dd>Definition</dd>
     <dt>Next term</dt>
     <dd>Definition</dd>
     </dl>
{% endhighlight %}

###HTML 表格

{% highlight html %}
     <table border="1">
     <tr>
       <th>someheader</th>
       <th>someheader</th>
     </tr>
     <tr>
       <td>sometext</td>
       <td>sometext</td>
     </tr>
     </table>
{% endhighlight %}

###HTML 框架

{% highlight html %}
     <frameset cols="25%，75%">
       <frame src="page1.htm">
       <frame src="page2.htm">
     </frameset>
{% endhighlight %}

###HTML 表单

{% highlight html %}
     <from action="http://www.example.com/test.asp" method="post/get">
     <input type="text" name="lastname"
     value="Nixon" size="30" maxlength="50">
     <input type="password">
     <input type="checkbox" checked="checked">
     <input type="radio" checked="checked">
     <input type="submit">
     <input type="reset">
     <input type="hidden">
     <select>
     <option>Apples
     <option selected>Bananas
     <option>Cherries
     </select>
     <textarea name="Comment" rows="60"
     cols="20"></textarea>
     </form>
{% endhighlight %}

###HTML 对象

{% highlight html %}
     &lt; is the same as <
     &gt; is the same as >
     &#169; is the same as ©
{% endhighlight %}

###HTML 其它元素

{% highlight html %}
     <!-- This is a comment --> 注释，不会在页面出现
     <blockquote>
     Text quoted from some source.
     </blockquote>
     <address>
     Address 1<br>
     Address 2<br>
     City<br>
     </address>
{% endhighlight %}
     

参考文章：

   <http://www.w3school.com.cn/html/html_quick.asp>
   <http://hi.baidu.com/snowicesky/item/3d22450b826124304ac4a311>














