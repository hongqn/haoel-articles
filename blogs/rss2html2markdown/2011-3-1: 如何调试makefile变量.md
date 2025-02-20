---
layout: post
title: 如何调试makefile变量
date: 2011/3/1/ 0:34:38
updated: 2011/3/1/ 0:34:38
status: publish
published: true
type: post
---

六、七年前写过一篇《[跟我一起写Makefile](http://blog.csdn.net/haoel/archive/2004/02/24/2886.aspx "跟我一起写Makefile")》，直到今天，还有一些朋友问我一些Makefile的问题，老实说，我有一段时间没有用Makefile了，生疏了。回顾，这几年来大家问题我的问题，其实很多时候是makefile的调试问题。所以，就像我在之前的那篇[关于GDB的技巧的文章](https://coolshell.cn/articles/3643.html "GDB中应该知道的几个调试方法")中做的一样，在这里向大家介绍一个小小的调试变量的技巧。相信一定对你有用。


对于Makefile中的各种变量，可能是我们比较头痛的事了。我们要查看他们并不是很方便，需要修改makefile加入echo命令。这有时候很不方便。其实我们可以制作下面一个专门用来输出变量的makefile（假设名字叫：vars.mk）



```

%:
        @echo '$*=$($*)'

d-%:
        @echo '$*=$($*)'
        @echo '  origin = $(origin $*)'
        @echo '   value = $(value  $*)'
        @echo '  flavor = $(flavor $*)'

```

这样一来，我们可以使用make命令的-f参数来查看makefile中的相关变量（包括make的内建变量，比如：COMPILE.c或MAKE\_VERSION之类的）。**注意：第二个以“d-”为前缀的目标可以用来打印关于这个变量更为详细的东西**（后面有详细说明）  




假设我们的makefile是这个样子（test.mk）



```


OBJDIR := objdir
OBJS := $(addprefix $(OBJDIR)/,foo.o bar.o baz.o)

foo = $(bar)bar = $(ugh)ugh = Huh?

CFLAGS = $(include_dirs) -O
include_dirs = -Ifoo -Ibar
CFLAGS := $(CFLAGS) -Wall

MYOBJ := a.o b.o c.o
MYSRC := $(MYOBJ:.o=.c)
```

那么，我们可以这样进行调试：



```


[hchen@RHELSVR5]$ make -f test.mk -f var.mk OBJS
OBJS=objdir/foo.o objdir/bar.o objdir/baz.o

[hchen@RHELSVR5]$ make -f test.mk -f var.mk d-foo
foo=Huh?
  origin = file
  value = $(bar)
  flavor = recursive

[hchen@RHELSVR5]$ make -f test.mk -f var.mk d-CFLAGS
CFLAGS=-Ifoo -Ibar -O -O
  origin = file
  value = -Ifoo -Ibar -O -O
  flavor = simple

[hchen@RHELSVR5]$  make -f test.mk -f var.mk d-COMPILE.c
COMPILE.c=cc -Ifoo -Ibar -O -Wall   -c
  origin = default
  flavor = recursive
   value = $(CC) $(CFLAGS) $(CPPFLAGS) $(TARGET_ARCH) -c

```

我们可以看到：


* make的第一个-f后是要测试的makefile，第二个是我们的debug makefile。
* 后面直接跟变量名，如果在变量名前加”d-“，则输出更为详细的东西。


说一说”d-” 前缀（其意为details），其中调用了下面三个参数。


* [$(origin)](http://www.gnu.org/software/make/manual/make.html#Origin-Function)：告诉你这个变量是来自哪儿，file表示文件，environment表示环境变量，还有environment override，command line，override，automatic等。
* [$(value)](http://www.gnu.org/software/make/manual/make.html#Value-Function)：打出这个变量没有被展开的样子。比如上述示例中的 foo 变量。
* [$(flavor)](http://www.gnu.org/software/make/manual/make.html#Flavor-Function)：有两个值，simple表示是一般展开的变量，recursive表示递归展开的变量。


（全文完）



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![Rust语言的编程范式](https://coolshell.cn/wp-content/uploads/2020/03/rust-social-wide-150x150.jpg)](https://coolshell.cn/articles/20845.html)[Rust语言的编程范式](https://coolshell.cn/articles/20845.html)
* [![程序员练级攻略（2018)  与我的专栏](https://coolshell.cn/wp-content/uploads/2018/05/300x262-150x150.jpg)](https://coolshell.cn/articles/18360.html)[程序员练级攻略（2018) 与我的专栏](https://coolshell.cn/articles/18360.html)
* [![API设计原则 – Qt官网的设计实践总结](https://coolshell.cn/wp-content/uploads/2017/07/api-design-300x278-2-150x150.jpg)](https://coolshell.cn/articles/18024.html)[API设计原则 – Qt官网的设计实践总结](https://coolshell.cn/articles/18024.html)
* [![Leetcode 编程训练](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/29.jpg)](https://coolshell.cn/articles/12052.html)[Leetcode 编程训练](https://coolshell.cn/articles/12052.html)
* [![State Threads 回调终结者](https://coolshell.cn/wp-content/uploads/2014/10/edsm-150x150.gif)](https://coolshell.cn/articles/12012.html)[State Threads 回调终结者](https://coolshell.cn/articles/12012.html)
* [![C语言的整型溢出问题](https://coolshell.cn/wp-content/uploads/2014/04/c99-150x150.jpg)](https://coolshell.cn/articles/11466.html)[C语言的整型溢出问题](https://coolshell.cn/articles/11466.html)
The post [如何调试makefile变量](https://coolshell.cn/articles/3790.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).