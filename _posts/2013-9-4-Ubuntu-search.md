---
category: Tools
layout: post
title: Ubuntu系统中查找文件和字符命令介绍 
---

在刚开始接触Ubuntu的时候，通常会遇到自己建立的文件不知道放在硬盘的什么地方，这就需要掌握一些搜索命令，快速找到我们想找的文件。下来我们以查找文件和查找字符两大类，对find、locate、which、grep四种命令进行介绍。

###一、查找文件
-----------------------------------------------------------

#####1、find命令

**1.1 find的语法：**

{% highlight ruby %} 
    find [起始目录] 寻找条件 操作
    find PATH OPTION [-exec COMMAND { } \;]
{% endhighlight %} 

**该命令中的寻找条件可以是一个用逻辑运算符not、and、or组成的复合条件,逻辑运算符and、or、not的含义为：**

and：逻辑与，在命令中用“-a”表示，是系统缺省的选项，表示只有当所给的条件都满足时，寻找条件才算满足。例如:

{% highlight ruby %} 
    find –name ’tmp’ –xtype c -user ’inin’
{% endhighlight %} 

该命令寻找三个给定条件都满足的所有文件。

or：逻辑或，在命令中用“-o”表示。该运算符表示只要所给的条件中有一个满足时，寻找条件就算满足。例如:

{% highlight ruby %} 
    find –name ’tmp’ –o –name ’mina*’
{% endhighlight %} 

该命令查询文件名为’tmp’或是匹配’mina*’的所有文件。

not：逻辑非，在命令中用“!”表示。该运算符表示查找不满足所给条件的文件。例如:

{% highlight ruby %} 
    find ! –name ’tmp’
{% endhighlight %} 

该命令查询文件名不是’tmp’的所有文件。

需要说明的是：当使用很多的逻辑选项时，可以用括号把这些选项括起来。例如：

{% highlight ruby %} 
    find (–name ’tmp’ –xtype c -user ’inin’ )
{% endhighlight %} 

**1.2 在option中，具体有参数：**

-name ’字串’ 查找文件名匹配所给字串的所有文件，字串内可用通配符 *、?、[ ]。

-lname ’字串’ 查找文件名匹配所给字串的所有符号链接文件，字串内可用通配符 *、?、[ ]。

-gid n 查找属于ID号为 n 的用户组的所有文件。

-uid n 查找属于ID号为 n 的用户的所有文件。

-group ’字串’ 查找属于用户组名为所给字串的所有的文件。

-user ’字串’ 查找属于用户名为所给字串的所有的文件。

-empty 查找大小为 0的目录或文件。

-path ’字串’ 查找路径名匹配所给字串的所有文件，字串内可用通配符*、?、[ ]。

**1.3 我们再看一下exec选项：**

-exec：对搜索的结构指令指定的shell命令。注意格式要正确："-exec 命令 {} \;"

在}和\之间一定要有空格才行;{}表示命令的参数即为所找到的文件;命令的末尾必须以“\;”结束。

例如：对root以及子目录查找不包括目录/root/bin的，greek用户的，文件类型为普通文件的，3天之前的名为test-find.c的文件进行删除操作，命令如下：

{% highlight ruby %} 
    find / -name "test-find.c" -type f -mtime +3 -user greek -prune /root/bin -exec rm {} \;
{% endhighlight %} 

find命令指令实例：

{% highlight ruby %} 
    find . - name ‘main*’ - exec more {} \;
{% endhighlight %} 

查找当前目录中所有以main开头的文件，并显示这些文件的内容。

{% highlight ruby %} 
    find . (- name a.out - o - name ‘*.o’)> - atime +7 - exec rm {} \;
{% endhighlight %} 

删除当前目录下所有一周之内没有被访问过的a .out或*.o文件。

命令中的“.”表示当前目录，此时 find 将从当前目录开始，逐个在其子目录中查找满足后面指定条件的文件。

“-name a.out” 是指要查找名为a.out的文件;

“-name ‘*.o’” 是指要查找所有名字以 .o 结尾的文件。

这两个 -name 之间的 -o 表示逻辑或(or)，即查找名字为a.out或名字以 .o结尾的文件。

find命令在当前目录及其子目录下找到这佯的文件之后，再进行判断，看其最后访问时间是否在7天以前(条件 -atime +7)，若是，则对该文件执行命令rm(-exec rm {} \;)。

其中 {} 代表当前查到的符合条件的文件名，\;则是语法所要求的。

#####2、locate命令

locate命令其实是“find -name”的另一种写法，但是要比后者快得多，原因在于它不搜索具体目录，而是搜索一个数据库（/var/lib/locatedb），这个数据库中含有本地所有文件信息。Linux系统自动创建这个数据库，并且每天自动更新一次，所以使用locate命令查不到最新变动过的文件。为了避免这种情况，可以在使用locate之前，先使用'sudo updatedb'命令，手动更新数据库。

**locate常用写法：**

{% highlight ruby %} 
    locate filename
{% endhighlight %} 

locate命令的使用实例：

{% highlight ruby %}  
    locate /etc/sh
{% endhighlight %} 

搜索etc目录下所有以sh开头的文件。

{% highlight ruby %}  
    locate ~/m
{% endhighlight %} 

搜索用户主目录下，所有以m开头的文件。

{% highlight ruby %}  
    locate -i ~/m
{% endhighlight %} 

搜索用户主目录下，所有以m开头的文件，并且忽略大小写。 

#####3、which命令

根据可执行文件的文件名,查找可执行文件。

**which常用写法：**

{% highlight ruby %} 
    which executeable_name
{% endhighlight %} 

例如:

{% highlight ruby %} 
    which apache2
{% endhighlight %} 

返回/usr/sbin/apache2

###二、查找字符
-----------------------------------------------------------
#####4、grep命令

grep命令是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹 配的行打印出来。grep全称是Global Regular Expression Print，表示全局正则表达式版本，它的使用权限是所有用户。

**4.1 grep的语法：**

{% highlight ruby %} 
    语法: grep [options] PATTERN [FILE...]
{% endhighlight %} 

**4.2 [options]主要参数：**

>－c：只输出匹配行的计数。

>－I：不区分大 小写(只适用于单字符)。

>－h：查询多文件时不显示文件名。

>－l：查询多文件时只输出包含匹配字符的文件名。

>－n：显示匹配行及 行号。

>－s：不显示不存在或无匹配文本的错误信息。

>－v：显示不包含匹配文本的所有行。


**4.3 PATTERN主要参数：**

\： 忽略正则表达式中特殊字符的原有含义。

^：匹配正则表达式的开始行。

$: 匹配正则表达式的结束行。

\<：从匹配正则表达 式的行开始。

\>：到匹配正则表达式的行结束。

[ ]：单个字符，如[A]即A符合要求 。

[ - ]：范围，如[A-Z]，即A、B、C一直到Z都符合要求 。

。：所有的单个字符。

\* ：有字符，长度可以为0。

**4.4 grep命令使用简单实例**

{% highlight ruby %} 
    grep ‘test’ d*
{% endhighlight %} 

显示所有以d开头的文件中包含 test的行。

{% highlight ruby %} 
    grep ‘test’ aa bb cc
{% endhighlight %} 

显示在aa，bb，cc文件中匹配test的行。

{% highlight ruby %} 
    grep ‘[a-z]\{5\}’ aa
{% endhighlight %} 

显示所有包含每个字符串至少有5个连续小写字符的字符串的行。

{% highlight ruby %} 
    grep ‘w\(es\)t.*\1′ aa
{% endhighlight %} 

如果west被匹配，则es就被存储到内存中，并标记为1，然后搜索任意个字符(.*)，这些字符后面紧跟着 另外一个es(\1)，找到就显示该行。如果用egrep或grep -E，就不用”\”号进行转义，直接写成’w(es)t.*\1′就可以了。

**4.5 grep命令使用复杂实例**

假设在’/usr/src/Linux/Doc’目录下搜索带字符 串’magic’的文件：

{% highlight ruby %} 
    grep magic /usr/src/Linux/Doc/*
    sysrq.txt:* How do I enable the magic SysRQ key?
    sysrq.txt:* How do I use the magic SysRQ key?
{% endhighlight %} 

其中文件’sysrp.txt’包含该字符串，讨论的是SysRQ的功能。
默认情况下，’grep’只搜索当前目录。如果此目录下有许多子目录，’grep’会以如下形式列出：

{% highlight ruby %} 
    grep: sound: Is a directory
{% endhighlight %} 

这可能会使’grep’ 的输出难于阅读。这里有两种解决的办法：
明确要求搜索子目录：grep -r
或忽略子目录：grep -d skip
如果有很多输出时，可以通过管道将其转到’less’上阅读：

{% highlight ruby %} 
    grep magic /usr/src/Linux/Documentation/* | less
{% endhighlight %} 

这样，就可以更方便地阅读。

有一点要注意，必需提供一个文件过滤方式(搜索全部文件的话用 *)。如果忘了，’grep’会一直等着，直到该程序被中断。如果遇到了这样的情况，按 <CTRL c> ，然后再试。
     













