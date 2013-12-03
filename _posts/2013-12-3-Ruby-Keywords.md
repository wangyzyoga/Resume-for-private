---
category: Rubyonrails
layout: post
title: Ruby中部分Keywords的含义及用法
---

##一、alias
是Ruby的一个关键字，对一个函数名或者变量重新命名，当对变量重新命名之后，就和旧的变量绑定在一起，无论哪一个变量改变都会造成变量的改变。重命名函数(方法)名后，即使重新定义了原始方法，别名方法仍保持着重定义前老方法的特性。若改变了某方法的内容后，又想使用修改前的方法时，别名会很有用。
{% highlight ruby %}
def meth
  puts "I am old!"
end
alias :new_meth :meth
def meth
  puts "I am new!"
end
puts meth  $: I am new!
puts new_meth  $: I am old!
{% endhighlight %}

##二、alias_method
是Module类的一个方法，它的参数是字符串或者symbol，并用逗号分隔，alias_method可以重定义。
{% highlight ruby %}
class A
  def a
    p "aaa"
  end
  alias_method :ab, :a
end
c = A.new
c.ab  $: aaa
{% endhighlight %}

##三、BEGIN
BEGIN块中的代码在所有代码执行之前执行，允许设置多个BEGIN块并按出现顺序执行块中代码。只有当起始大括号和BEGIN标识符号位于同一行时，代码才能正确执行，同时GEGIN块也不受任何控制结果的影响，只要出现就会得到执行并只执行一次。
{% highlight ruby %}
BEGIN{
  print "OnInit(object sender, EventArgs args)\n"
}
BEGIN{
  print "OnLoad(object sender, EventArgs args)\n"
}
print "Running"
{% endhighlight %}

##四、break
是Ruby的一个关键字，如果符合当前条件，就跳出当前循环。
{% highlight ruby %}
loop do
  puts "Running..."
  print "Enter q to quit:"
  gets
  chomp
  break if $_=="q"
end
{% endhighlight %}

##五、defined
是Ruby语法中一个操作符，因此不会对参数进行计算。如果一个方法以大写字母开头，使用defined？判断需要在方法名后添加"()"，否则方法名会被当常数处理。
{% highlight ruby %}
p defined? Foo  $: nil
p defined? Foo()  $:"method"
{% endhighlight %}

##六、END
END块与BEGIN块相反，在所有代码执行之后执行，多个END块时最先出现的最后执行。除此之外，END块不受while的影响，但可能通过if来控制END块执行与否。
{% highlight ruby %}
if false
   END{
     print "Init"  #不输出
   }
end
END{
  print "Load\n"   #最后输出
}
END{
  pring "Start\n"  #先与Load输出
}
{% endhighlight %}

##七、ensure
Ruby异常处理关键字ensure，无论begin块是否成功，ensure代码域都将执行。Ruby异常处理可以只用ensure或rescue，但当它们在同一begin...end域中时，rescue必须放在ensure前面。
{% highlight ruby %}
begin
  file = open("/tmp/file","w")
  # write to the file...
  rescue
  # handle the exceptions...
  ensure
  file.close
end
{% endhighlight %}

##八、for
是通过调用each实现，在each的scope外面定义一个同名变量，因此for更慢一些。
{% highlight ruby %}
(1..5).each do |i|
i = nil; for i in (1..5)  # 两者等价
{% endhighlight %}

**下面的这些关键字，我就只讲含义，不一一举例说明。**

##九、module
是用来区分同名但属于不同开发者或组织的代码。

##十、next
忽略本次循环的剩余部分，开始下一次循环。

##十一、redo
重新开始循环，还是从这一次开始执行。

##十二、retry
重新开始执行这个循环体。

##十三、super
代替的是父类中和当前方法名相同的方法，如果不带任何参数(也没有括号)，实际上作用就是自动调用父类中的当前方法，并且把当前参数也传过去。如果父类该方法的参数和子类不一样，才需要显示传入参数调用。

##十四、then
在if、unless、case语句中，then都可省略。

##十五、undef
可以将类的方法取消定义(彻底删除掉)，需要注意：如果一个类继承自父类，并且又定义与父类同名的方法，用undef取消该方法后，将连带父类的同名方法一起取消。
