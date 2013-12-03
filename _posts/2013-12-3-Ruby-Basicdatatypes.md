---
category: Rubyonrails
layout: post
title: Ruby的基本数据类型
---

##一、字符串 strings
ruby中没有字符，只有字符串。
单引号字符串，只有'和\需要进行转义，其它的字符保持字面的含义；
双引号字符串，双引号字符串最大的特点是可以进行数值内插，产生双引号字符串的方式有很多种。
单引号中两个相连的反斜线被替换成一个反斜线，一个反斜线后跟一个单引号被替换成一个单引号。
{% highlight ruby %}
insert = 100
print '#{insert}_string'  # #{insert}_sting
print %q/#{insert}_string/  # %q分隔符表示单引号字符串
print "#{insert}_string\n"  # 100_string
print %/#{insert}_string\n/ # %分隔符或%Q表示双引号字符串
print %Q/#{insert}_string\n/
{% endhighlight %}

##二、数值型 numbers
整数支持二进制，八进制，十进制，十六进制，根据整数的大小动态决定整数是Fixnum类型还是Bignum类型。浮点数支持科学计数法，小数点后至少有一个数字。
数值类型继承图如下：
{% highlight ruby %}
Numeric
  |--Integer
     |--Fixnum
		    |--Bignum
	|--Float
	|--Complex(标准库)
	|--BigDecimal(标准库)
	|--Rational(标准库)
{% endhighlight %}

##三、区间 ranges
区间提供了处理值具有连续特性的对象集合的简便方法，ruby为了节省空间只是在内存中保留了区间首尾两个对象的引用。
{% highlight ruby %}
for i in 1..3  # 闭合区间，1 2 3
  print i
end
for i in "num1"..."num3"  # 首闭尾开，输出num1 num2
  print i
end
{% endhighlight %}

##四、数组 arrays
可以容纳各种类型对象的集合。
{% highlight ruby %}
arr1 = [1,2,3,"num1"]
arr2 = %w/1 2 3 num1/ #%w和%W为字符数组分隔符，元素必须用空格隔开
print arr1,"\n",arr2,"\n"
print arr1[1].class,"\n"  # Fixnum类型
print arr2[1].class  # String类型
{% endhighlight %}

##五、散列表 hashes
键－值对的集合，应用广泛。
{% highlight ruby %}
hash1 = { 1 => "first", "second" => 2 }
print hash1["second"]
{% endhighlight %}

##六、符号 Symbol
由于相同的字符串在内存中有不同的拷贝，所以采用符号来节省内存，相同的符号在内存中只有一份拷贝，另外需注意字符串和符号是完全不同的类型。
{% highlight ruby %}
print "string".object_id,"\n"  # 相同的字符串具有不同的id
print "string".object_id,"\n"
print :string.object_id,"\n"  # 相同的符号具有相同的id
print :string.object_id,"\n"
{% endhighlight %}
