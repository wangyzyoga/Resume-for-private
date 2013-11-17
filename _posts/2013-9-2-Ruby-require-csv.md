---
category: Rubyonrails
layout: post
title: Ruby从入门到精通 学习记录二(require/CSV) 
---

###一、REQUIRE

今天学习<Ruby从入门到精通>时，使用require加载文件，老提示：LoadError。然后在网上查看原因，并整理几种加载当前路径下的某个源文件的常用方法。

1. 在加载的源文件名前加上当前目录"./"，即require "./test"
2. 使用load加载完整文件名，即load "test.rb"
3. 使用require_relative替代require，即require_relative "test"
4. 使用解析后的文件路径，即require File.expand_path("./test", \_\_FILE\_\_)  
   这里File.expand_path是将指定的参数路径解析成绝对路径，./test是希望加载的文件,\_\_FILE\_\_是当前文件绝对路径。
5. 动态修改加载路径，即$LOAD_PATH.unshift(File.dirname(\_\_FILE\_\_))unless $LOAD_PATH.include?(File.dirname(\_\_FILE\_\_))  
   其中$LOAD_PATH 指的是Ruby读取外部文件的一个环境变量，Ruby会在这个环境变量的路径中读取需要require的文件，如果在环境变量中找不到自己想要的文件，就会报LoadError，还有$LOAD_PATH和$:指的都是同一个环境变量；File.dirname(\_\_FILE\_\_)代表当前路径；而$LOAD_PATH.unshift方法的目的就是将当前目录作用ruby标准的加载路径，即$LOAD_PATH.unshift 就是把上面得出的绝对路径加到现在已经存在所有环境变量之前。    
<br>

###二、CSV

书中程序：

    require 'csv'
    CSV.open('text.txt', 'r') do |person|
      puts person.inspect
    end

该程序无法运行，提示：

    <#CSV io_type:File io_path:"text.txt" encoding:GBK lineno:0 col_sep:",
    " row_sep:"n" quote_char:""">

后来百度搜索一下，得知在ruby1.9.x中CSV.open的API发生了变更，在ruby1.9.x中要想打印或者输出csv/txt的文件内容，需要按照如下的写法：

    require 'csv'
    CSV.open('text.txt', 'r') do |person|
      person.each { |row| puts row }
    end
     

参考文章：

   <http://zorro.blog.51cto.com/2139862/893944>
   <http://blog.sina.com.cn/s/blog_67b5c7b7010154rn.html>











