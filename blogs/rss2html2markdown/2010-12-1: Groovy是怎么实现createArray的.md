---
layout: post
title: Groovy是怎么实现createArray的
date: 2010/12/1/ 6:8:53
updated: 2010/12/1/ 6:8:53
status: publish
published: true
type: post
---

[Groovy](http://groovy.codehaus.org/)是一个基于 Java虚拟机的敏捷 动态语言。构建在强大的Java语言之上 并 添加了从Python，Ruby和Smalltalk等语言中学到的 诸多特征。为Java开发者提供了 现代最流行的编程语言特性，而且学习成本很低（几乎为零）。在以前的酷壳的[五大基于JVM的脚本语言](https://coolshell.cn/articles/2631.html)中也介绍过它。


下面，让我们看看他的一个createArray的实现，请大家前去围观下面的Groovy的trunk上的源码吧。真是很好很强大。


<http://svn.codehaus.org/groovy/trunk/groovy/groovy-core/src/main/org/codehaus/groovy/runtime/ArrayUtil.java>


这里摘上前几个createArray重载函数让大家看看，（一共有250个重载函数）



```
public class ArrayUtil {
    ... ...
    ... ...
 public static Object[] createArray(Object arg0, Object arg1) {
 return new Object[]{
 arg0, arg1};
 }

 public static Object[] createArray(Object arg0, Object arg1, Object arg2) {
 return new Object[]{
 arg0, arg1, arg2};
 }

 public static Object[] createArray(Object arg0, Object arg1, Object arg2, Object arg3) {
 return new Object[]{
 arg0, arg1, arg2, arg3};
 }

 public static Object[] createArray(Object arg0, Object arg1, Object arg2, Object arg3, Object arg4) {
 return new Object[]{
 arg0, arg1, arg2, arg3, arg4};
 }

 public static Object[] createArray(Object arg0, Object arg1, Object arg2, Object arg3, Object arg4, Object arg5) {
 return new Object[]{
 arg0, arg1, arg2, arg3, arg4, arg5};
 }
 ... ...
 ... ...
} 
```

这里给了一些[解释](http://groovy.329449.n5.nabble.com/Guys-any-explanations-about-this-td3285524.html#a3285676)：



* **First**: the package is org.codehaus.groovy.runtime. This is NOT a class that any user of Groovy will ever use. There are plenty of XML utilities in groovy.lang or groovy.xml for you to use.
* **Second**: This class is never invoked from code. It exists so that byte code statements have something to link against. If you dump the stack language of a .class file you may indeed see a “INVOKESTATIC org/codehaus/groovy/runtime/XMLUtil” invocation. This logic is used around the CallSite writing features.
* **Third**: Implementing a dynamic language (Groovy) in a static language (Java) on a type less virtual machine (JVM) is hard. Every language has their work arounds. We generated some code so that we had something to link against. At one point, JRuby was generating reams of interfaces (IIRC) and have you seen the implementation of OpenJDK? Ever notice now many methods are overloaded for all the primitives plus Object. These are all workarounds to get the end user a good programming experience while still running on the JVM.


大意是：这个类对于Groovy的使用者是不会用到的，也不会被调用到，因为在JVM下实现动态语言是有一定的难度，这算是一个work around。



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![语言的数据亲和力](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/3.jpg)](https://coolshell.cn/articles/4905.html)[语言的数据亲和力](https://coolshell.cn/articles/4905.html)
* [![五大基于JVM的脚本语言](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/8.jpg)](https://coolshell.cn/articles/2631.html)[五大基于JVM的脚本语言](https://coolshell.cn/articles/2631.html)
* [![【问题】传球问题](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/30.jpg)](https://coolshell.cn/articles/1976.html)[【问题】传球问题](https://coolshell.cn/articles/1976.html)
* [![Linus：利用二级指针删除单向链表](https://coolshell.cn/wp-content/uploads/2013/02/linus_pointer_to_pointer-150x150.jpg)](https://coolshell.cn/articles/8990.html)[Linus：利用二级指针删除单向链表](https://coolshell.cn/articles/8990.html)
* [![结对编程的利与弊](https://coolshell.cn/wp-content/uploads/2009/03/cccpairprogramming-150x150.jpg)](https://coolshell.cn/articles/16.html)[结对编程的利与弊](https://coolshell.cn/articles/16.html)
* [![Docker基础技术：Linux Namespace（下）](https://coolshell.cn/wp-content/uploads/2015/04/jail_cell-150x150.jpg)](https://coolshell.cn/articles/17029.html)[Docker基础技术：Linux Namespace（下）](https://coolshell.cn/articles/17029.html)
The post [Groovy是怎么实现createArray的](https://coolshell.cn/articles/3335.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).