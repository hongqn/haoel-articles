---
layout: post
title: 你能做对下面这些JavaScript的题吗？
date: 2009/4/26/ 6:48:51
updated: 2009/4/26/ 6:48:51
status: publish
published: true
type: post
---

你能做对下面这些JavaScript的题吗？


[原文](http://asserttrue.blogspot.com/2009/04/can-you-pass-this-javascript-test.html)


你认为你了解JavaScript? 快速的做一下下面的这些题目。并将下面的每一个表达式的值写出。(答案在问题后面)


1. ++Math.PI  

2. (0.1 + 0.2) + 0.3 == 0.1 + (0.2 + 0.3)  

3. typeof NaN  

4. typeof typeof undefined  

5. a = {null:null}; typeof a.null;  

6. a = “5”; b = “2”; c = a \* b;  

7. a = “5”; b = 2; c = a+++b;  

8. isNaN(1/null)  

9. (16).toString(16)  

10.016 \* 2  

11.~null  

12.”ab c”.match(/\b\w\b/)


  

首先，这不是一个入门教程，因此我不会去对每一个答案做单独的解释，如果你觉得你有不理解的地方，我建议你 while (!掌握()) 专研它();


答案：  

1. 4.141592653589793  

2. false  

3. “number”  

4. “string”  

5. “object”  

6. 10  

7. 7  

8. false  

9. 10  

10. 28  

11. -1  

12. [ “c” ]


我的打分如下(每答对一题一分)：


5分 – 7分: 了解javascript  

8分 – 10分: 专家  

11: 大学士  

12分: 大师


简要的注释：  

第2题：答案是false，javascript和java非常相似(或则其他使用了IEEE 754浮点数的语言)，这也是为什么在和钱打交道的正式应用程序中一般不使用浮点数四则运算的原因，浮点数的加或乘除外，下面[这篇](http://www.macaulay.ac.uk/fearlus/floating-point/)文章有关于浮点数四则运算的一个详细的讨论。


第6题：在四则运算表达式中使用乘、除或减，如果表达式中包含一个或多个字符型，那么语法解释器会试着首先将字符型转换为数值型，如果算术表达式包含着加号运算，那么所有的运算项都会被转换成字符型。


第7题：JavaScript中表达式的运算的优先级是从坐到右(类似于Java和C)，因此，在这里将会是一个先a计算值，加上b，然后在a++的次序，而不是a加上++b这样的运算。


第9题：toString() 可以带一个可选的数字参数。参数值16意味着基于16进制，返回的字符串将会是该数字的16进制表示，在这个例子里面就是10，如果你写.toString(2)那么你将会得到这个数字的2进制表示，等等。


第10题：016是8进制表示，即8进制的14。虽然是这样，但比较有趣的是，如果有你以”016″(字符串形式)去乘上一个数，语法解释器会认为”016″是基于10进制的数。


如果你不能正确的写出这些题目的答案，不要灰心丧气，因为几乎上面的每一个问题都(明显地)含有着蒙蔽人小伎俩，现在让我问面对它。当然，如果你非常正确的回答了上面的所有问题，你也不必太过沾沾自喜，这意味着这你仅仅是一个比任何正常人都奇怪的javascript怪杰而已！



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![程序员练级攻略（2018)  与我的专栏](https://coolshell.cn/wp-content/uploads/2018/05/300x262-150x150.jpg)](https://coolshell.cn/articles/18360.html)[程序员练级攻略（2018) 与我的专栏](https://coolshell.cn/articles/18360.html)
* [![Chrome开发者工具的小技巧](https://coolshell.cn/wp-content/uploads/2017/01/pretty-code-150x150.gif)](https://coolshell.cn/articles/17634.html)[Chrome开发者工具的小技巧](https://coolshell.cn/articles/17634.html)
* [![如何读懂并写出装逼的函数式代码](https://coolshell.cn/wp-content/uploads/2016/10/drawing-recursive-150x150.jpg)](https://coolshell.cn/articles/17524.html)[如何读懂并写出装逼的函数式代码](https://coolshell.cn/articles/17524.html)
* [![函数式编程](https://coolshell.cn/wp-content/uploads/2013/12/yoda-lambda-150x150.png)](https://coolshell.cn/articles/10822.html)[函数式编程](https://coolshell.cn/articles/10822.html)
* [![Lua简明教程](https://coolshell.cn/wp-content/uploads/2013/12/lua-150x150.gif)](https://coolshell.cn/articles/10739.html)[Lua简明教程](https://coolshell.cn/articles/10739.html)
* [![数据即代码：元驱动编程](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/24.jpg)](https://coolshell.cn/articles/10337.html)[数据即代码：元驱动编程](https://coolshell.cn/articles/10337.html)
The post [你能做对下面这些JavaScript的题吗？](https://coolshell.cn/articles/688.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).