---
category: Tools
layout: post
title: Ubuntu12.04下安装与配置PostgreSQL-9.1详解
---

##一、在Ubuntu下安装Postgresql
###1.使用 apt-get install 安装

{% highlight ruby %}
    $ sudo apt-get install -y postgresql-9.1 postgresql-client-9.1 postgresql-contrib-9.1 postgresql-server-dev-9.1
{% endhighlight %}

##二、修改PostgreSQL数据库的默认用户postgres的密码
###1.使用postgres用户登录psql客户端

{% highlight ruby %}
    $ sudo -u postgres psql
{% endhighlight %}

###2.修改PostgreSQL默认用户postgres的密码（postgres=#为psql中的命令行）

{% highlight ruby %}
    postgres=# ALTER USER postgres WITH PASSWORD 'postgres';
{% endhighlight %}

###3.退出PostgreSQL的psql客户端

{% highlight ruby %}
    postgres=# \q
{% endhighlight %}

##三、修改Linux系统的postgres用户的密码

###1.设置PostgreSQL用户密码
PostgreSQL数据库默认会创建一个Linux用户postgres，通过下面的代码修改密码为'postgres’。

{% highlight ruby %}
    $ sudo -u postgres passwd
    输入新的 UNIX 密码：
    重新输入新的 UNIX 密码：
{% endhighlight %}

现在就可以在数据库服务器上，用postgres帐号通过psql或者pgAdmin等等客户端操作数据库了。

##四、修改PostgresSQL数据库配置实现远程访问

###1.监听任何地址访问，修改连接权限
将/etc/postgresql/9.1/main/postgresql.conf文档中如下注释去掉：

{% highlight ruby %}
    #listen_addresses = ‘localhost’ 改为 listen_addresses = ‘*’
    #password_encryption = on 改为 password_encryption = on
{% endhighlight %}

在/etc/postgresql/9.1/main/pg_hba.conf文档末尾加上如下内容：

{% highlight ruby %}
    # to allow your client visiting postgresql server
    host all all 0.0.0.0 0.0.0.0 md5
{% endhighlight %}

###2.重启PostgreSQL数据库

{% highlight ruby %}
    $ /etc/init.d/postgresql restart
{% endhighlight %}
         
##五、管理PostgreSQL用户和数据库
###1.登录postgre SQL数据库

{% highlight ruby %}
    $ psql -U postgres -h 127.0.0.1
{% endhighlight %}

###2.创建新用户test，密码123456，无建数据库的权限

{% highlight ruby %}
    $ postgres=# create user “test” with password ‘123456’ nocreatedb;
{% endhighlight %}

###3.建立数据库，并指定所有者

{% highlight ruby %}
    $ postgres=# create database “testdb” with owner=”test”;
{% endhighlight %}

##六、安装postgresql数据库pgAdmin3客户端管理程序

{% highlight ruby %}
    $ apt-get install -y pgadmin3
{% endhighlight %}

