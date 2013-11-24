---
category: Rubyonrails
layout: post
title: Rails中使用PostgreSQL数据库经常遇到两个问题
---


##问题一、找不到.s.PGSQL.5432这个文件

页面提示具体错误信息如下：

{% highlight ruby %}
    No such file or directory 
    Is the server running locally and accepting 
    connections on Unix domain socket "/var/run/postgresql/.s.PGSQL.5432"
{% endhighlight %}

遇到这个问题需要先运行

{% highlight ruby %}
    sudo netstat -nlp | grep 5432
{% endhighlight %}

找出与端口5432（PostgreSQL默认端口号）相关进程信息,如果你更改了PostgreSQL的端口（我把端口改为5433），需要对应修改上述命令的端口。

{% highlight ruby %}
    tcp        0      0 0.0.0.0:5433            0.0.0.0:*               LISTEN      6209/postgres
    tcp6       0      0 :::5433                 :::*                    LISTEN      6209/postgres
    unix       2      [ ACC ]                   流                      LISTENING   40311    6209/postgres       /var/run/postgresql/.s.PGSQL.5433
{% endhighlight %}

找到/var/run/postgresql/.s.PGSQL.5433文件，然后与/var/run/postgresql/.s.PGSQL.5432文件建立软链接就解决该问题。

{% highlight ruby %}
    sudo ln -s /var/run/postgresql/.s.PGSQL.5433 /var/run/postgresql/.s.PGSQL.5432
{% endhighlight %}

##问题二、PostgreSQL数据库用户认证失败

页面提示具体错误信息如下：

{% highlight ruby %}
    Peer authentication failed for user "postgres"
{% endhighlight %}

这个问题是因为在/etc/postgresql/9.1/main/pg_hba.conf中：

{% highlight ruby %}
    # "local" is for Unix domain socket connections only
    local             all             all             peer
{% endhighlight %}

只需要把peer改为md5，然后重启PostgreSQL数据库就解决该问题。









