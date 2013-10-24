---
category: Blog
layout: post
title: Ruby中require/load/include/extend的区别
---

{{ page.title }}
================

<p class="meta">2013-10-24 王要佳</p>

### 1、Require：

require方法是加载一个库，并且只加载一次，如果多次加载会返回false。只有当要加载的库位于一个分离的文件中时才有必要使用require，使用时不需要加扩展名，一般放在文件的最前面：

    require ‘test_library’
<br>
#####1.1、Require引用文件默认路径：

运行

    xxx@ubuntu:~/repos/sample_app/ruby-1.9.3$ require 'filename'

系统会在ruby安装的lib目录和~/repos/sample_app/ruby-1.9.3/目录下查找加载的文件。

#####1.2、Require引用单个文件的四种方法：
<br>

    1  require File.join(__FILE__, '../file_to_require')。  # __FILE__为常量，表示当前文件绝对路径
    2  require File.expand_path('../file_to_require', __FILE__)  # 这种方法是Rails常用的做法
    3  require File.dirname(__FILE__) + '/file_to_require'    
    4  $LOAD_PATH.unshift(File.dirname(__FILE__))  # 先把目录加入LOAD_PATH变量中，然后直接引用文件名
       require 'filename'
<br>
#####1.3、Require引用一个目录下所有文件的两种方法：
<br>

    1  Dir[File.dirname(__FILE__) + '/lib/*.rb'].each {|file| require file }
    2  引用Require_all gem搞定,地址：https://rubygems.org/gems/require_all
<br>
### 2、Load：

load用来多次加载一个库，必须指定扩展名：

    load ‘test_library.rb’
<br>
### 3、Include:

当库被加载之后，可以在类定义中包含一个module，让module的实例方法和变量成为类本身的实例方法和类变量，它们mix进来。include并不会把module的实例方法拷贝到类中，只是做了引用，包含module的不同类都指向了同一个对象。如果改变了module的定义，即使程序还在运行，所有包含module的类都会改变行为。

    module Log 
        def class_type 
            “This class is of type: #{self.class}” 
        end 
    end 
    class TestClass 
        include Log 
    end 

    > TestClass.new.class_type    => This class is of type: TestClass
<br>
### 4、Extend:

extend会把module的实例方法作为类方法加入类中：

    module Log 
        def class_type 
           “This class is of type: #{self.class}” 
        end 
    end 
    class TestClass 
        extend Log 
    end
 
    > TestClass.class_type    => This class is of type: TestClass





    















