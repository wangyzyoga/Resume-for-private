---
category: Rubyonrails
layout: post
title: 给Blog增加评论功能-Disqus
---

### Disqus是什么

* Disqus是一家第三方社会化评论系统，主要为网站主提供评论托管服务。

* 当前有80万家第三方网站在使用Disqus提供的第三方评论系统，CNN、NBC、Fox News、Engadget、Time等知名网站均使用了Disqus提供的社会化评论系统。

* WordPress、Blogger、Tumblr等第三方博客平台均提供了Disqus第三方评论插件。


### 首先

注册<a href="http://disqus.com" target="_blank">Disqus</a>帐号，SiteURL,SiteName,SiteShortname这3个都是必填项，其中Site Shortname将会在最后的install时自动生存js代码中用到。

### 其次 

接下来会有一些简单的设置，比如语言／社交工具／评论选项等等内容。

### 接着

install，在platform中选择<a href="http://docs.disqus.com/developers/universal/" target="_blank">Universal Code</a>,所谓install，其实就是将一段js代码嵌入到你的博客源代码里面。

### 最后

获取js代码，DisQus生成了如下的一段代码：

{% highlight js linenos %}
<div id="disqus_thread"></div>
<script type="text/javascript">
    /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
    var disqus_shortname = 'example'; // replace example with your forum shortname
    /* * * DON'T EDIT BELOW THIS LINE * * */
    (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript';
        dsq.async = true;
        dsq.src = 'http://' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || 
        document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();</script>
<noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">
comments powered by Disqus.</a></noscript>
<a href="http://disqus.com" class="dsq-brlink">blog comments powered by <span 
class="logo-disqus">Disqus</span></a>
{% endhighlight %}

只需将代码中的'example'替换为注册时填写的Shortname，然后将它嵌入到所需页面中，通常是 /layout/post.html。


### 添加评论计数到首页

首先，添加下面的js代码到首页模板（default.html）</body>前。

{% highlight js linenos %}
<script type="text/javascript">
  /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
  var disqus_shortname = 'example'; // replace example with your forum shortname
  /* * * DON'T EDIT BELOW THIS LINE * * */
  (function () {
      var s = document.createElement('script'); s.async = true;
      s.type = 'text/javascript';
      s.src = 'http://' + disqus_shortname + '.disqus.com/count.js';
      (document.getElementsByTagName('HEAD')[0] || 
      document.getElementsByTagName('BODY')[0]).appendChild(s);
  }());</script>
{% endhighlight %}

然后，在首页需要添加评论的地方，写一个链接，

     <a href="\{\{ post.url }}#disqus_thread"></a>
Disqus将会通过URL获取评论数。说明：上述代码中 \ 为转义字符，\ { \ }代表大括号。



