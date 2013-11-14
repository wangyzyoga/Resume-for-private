---
category: Tools
layout: post
title: Vim中分屏操作大全详解
---

{{ page.title }}
================

<p class="meta">2013-11-12 王要佳</p>

今天无意看到Vim还可以分屏显示，个人觉得很酷，因此把Vim中关于分屏相关操作整理。

###1、分屏启动

使用大写的O参数来垂直分屏：vim -On file1 file2 ...

使用小写的o参数来水平分屏：vim -on file1 file2 ...

注释：n代表数字，表示分成几个屏。

**小技巧：使用vim编程时需要多行缩进，可以在命令模式输入：开始行号,结束行号 < 或 > 向左缩进或向右缩进**

##2、Vim分屏

上下分割当前打开的文件：Ctrl+W s

上下分割并打开一个新的文件：:sp file

左右分割当前打开的文件：Ctrl+W v

左右分割并打开一个新的文件：:vsp file

命令模式下：

:new，新建文件并分屏，Ctrl+W n

:spilt，水平分屏，将当前屏分为两个，水平的：Ctrl+w s

:vsplit，垂直分屏，将当前屏分为两个，垂直的：Ctrl+w v

:only，取消当前的屏，当前屏指的是光标所在屏


###3、切换分屏

ViM中的光标键是h, j, k, l，要在各个屏间切换，只需要先按一下Ctrl+W。

把光标移到右边的屏：Ctrl+W l

把光标移到左边的屏中：Ctrl+W h

把光标移到上边的屏中：Ctrl+W k

把光标移到下边的屏中：Ctrl+W j

把光标移到下一个的屏中：Ctrl+W w

把光标移到下一个的屏中：Ctrl+W p

**小技巧：通过在.vimrc文件增加如下设置，可以使用鼠标在分屏之间切换光标**

     set mouse=a
     set selection=exclusive
	 set selectmode=mouse,key
<br />
###4、关闭分屏 

关闭其他窗口：Ctrl+W  o

关闭当前窗口：Ctrl+W c

关闭当前窗口，如果只剩最后一个了，则退出Vim：Ctrl+W q

###5、加载文件

在新的垂直分屏中打开文件：:vs 文件路径/文件名

在新的水平分屏中打开文件：:sv 文件路径/文件名

###6、屏幕尺寸

下面是改变尺寸的一些操作，主要是高度，对于宽度你可以使用Ctrl+W < 或是 >。

让所有的屏都有一样的高度：Ctrl+W =

增加高度：Ctrl+W +

减少高度：Ctrl+W -













