---
layout: post
title: Bret Victor – Learnable Programming
date: 2012/10/14/ 8:37:4
updated: 2012/10/14/ 8:37:4
status: publish
published: true
type: post
---

大家是否还记得之前酷壳向大家介绍的苹果设计师[Bret Victor](http://worrydream.com/)一种可视编程的视频《[Bret Victor – Inventing on Principle](https://coolshell.cn/articles/6775.html)》，最近，他写了一篇文章—— [Learnable Programming](http://worrydream.com/LearnableProgramming/)，写这篇文章的原因是因为“可汗学院(Khan Academy)”近期上线的一个[在线编程环境](http://www.khanacademy.org/cs)，根据他的演讲提供了一堆基于Javascript的“实时编程”的环境，因为这个环境是[引用了他的想法](http://ejohn.org/blog/introducing-khan-cs)，所以，他有必要出来喷两句。


这篇文章的开头就是一个问题——“*How do we get people to understand programming?*”，我们怎么让人们懂得编程？


![](https://coolshell.cn/wp-content/uploads/2012/10/Learnable_Programming.jpg "Learnable_Programming")


然后，他说了两条——


* **编程是一种思考，而不是一种死记硬背的技能！**你学会了“for循环”并不是说你就学会了编程，这就好像你知道有铅笔这个东西，但是你对绘画还是什么不懂。（对于这一条，正好这两天我在微博上和人辩论“[基础算法面试题是否好](http://weibo.com/1401880315/yFQkJn8bC)”（还有[微博一](http://weibo.com/1401880315/yFOeyy00M)，[微博二](http://weibo.com/1401880315/z06Y0qMGf)），而且我以前也写过一篇《[为什么我反对纯算法面试](https://coolshell.cn/articles/8138.html "为什么我反对纯算法面试题")》，这里借用Bret的话再加强一下我的观点——“**我们一方面在骂中国的应试教育毁了学生，另一方面我们又在把我们的面试变成“考八股文”式的考试！  你会qsort有什么用？你只不过是会用一支高级铅笔而已罢了。**”）


* **人只有看得见，才能理解。**如果一个程序员不能看到他的程序在干什么，那么她就不能理解程序。（对于这一条，让我想到了Donald Knuth的话——“An algorithm must be seen to be believe!”）


所以，Bret 觉得编程软件的目标是——



* 支持并激发强大的思考。 To support and encourage powerful ways of thinking.
* 让程序员可以看得见程序的运行过程。To enable programmers to see and understand the execution of their programs


他说，可汗学院的“实时编程环境”并没有达到上面的任何一个目标。他还说用Javascript这样设计得很垃圾的语言根本不能支持强大的思考，而且还忽略了近十年来的成果，可汗学院这些东西完全是毫无价值的。


Bret认为，Alan Perlis的名言——“要学会编程，你必需得同时变成机器和程序”是错误的，这句被广为流传的错误名言，让我们把编程变成很难，并且掩盖了编程的艺术。人并不是一台机器，我们也不应该强迫自己变成那样。


接下来，他说明了一个编程系统应该有两个部分——


* **编程的“环境”，是其中一部分需要安装在电脑上的。**


* **编程的“语言”，是另一部分需要安装在程序员大脑里的。**


他随笔给出来了一些Design Principles——


对于“**编程环境**”，应该能让学习者干下面的事：


* **阅读程序词汇 read the vocabulary** *—* 这些单词意味着什么？是不是显而易见不用思考的？是不是很自然地被上下文解释了？


* **跟进流程 follow the flow** *—* 在什么时候会发生什么？流程的时间过程是不是看得见摸得着的？流程的粒度是否有意义？


* **看见状态 see the state** *—* 电脑在想些什么？你能不能看到电脑里的数据？并可以看到不同状态的比较？没有任何状态会隐藏？


* **通过交互来创造代码 create by reacting** *—* 从粗糙开始，然后开始雕琢程序。交互是否实时显示在屏幕上？有多少组件我可以用来做实时交互？


* **通过抽像来创造代码 create by abstracting** *—* 从一些hard code开始，然后开始抽象成变量*，*抽象成公式，抽象成函数。从一个开始作模板，然后做多个不同的东西。


对于“**编程语言**” 来说，它应该提供下面的事：


* **同一性和比方 identity and metaphor** *—* 我怎么把电脑的世界和我的世界联系起来?推荐了一本书《*[“Mindstorms”](http://books.google.com/books?id=HhIEAgUfGHwC&printsec=frontcover)*》


* **分解 decomposition** *—* 怎么把我的想法分解成碎片？*how do I break down my thoughts into mind-sized pieces?*
* **重组 recomposition** *—* 怎么把这些碎片重组起来？ *how do I glue pieces together?*
* **可读性 readability** *—* 这一大堆程序单词是什么意思？*what do these words mean?*


然后，他说“The Features are not the point”，**我们很多时候会关注编程环境和编程语言提供的功能，这就好像我们在看一本书有哪些单词一样，有哪些单词不重要，重要的是我这些单词组合起来传达了一个什么信息**？**一个设计的好的系统并不是一堆功能，一个设计得好的编程环境是激发特定的思考方式**。所有的功能都是非常小心翼翼地组合起来为之服务。（不好意思，我又要插一句。我觉得这和我在《[抄袭，腾讯和产品](https://coolshell.cn/articles/7617.html "抄袭，腾讯 和 产品")》一文中，我所理解的“什么是真正的产品”有点类似——真正的产品不是功能的组合，而是要表达的价值和对某一特定问题端到端的解决方案）


接下来，Bret用大量的示例告诉了大家上面所说的那几条是具体是什么。大家一定要去读一读！（我把这些东西总结果在上面的那些条目中了）


最后，Bret说了一下，他被问过很多次——这些漂亮的想法怎么应用到现实世界中？他说这个问题问的是对的，但是这些问题问的就好像是——“怎么能让一匹马从内燃机引擎受益”一样，其假设的改变是错误的。他回答到，更准确的是——“**Programming has to work like this**”，所以他说，他的这些东西不是一种“Training”，也不是一种“银弹”，只不过是拿开了眼罩。


**更新：**一楼回复的朋友给了一个中译版的链接：<http://chengyichao.info/learnable-programming/>


(全文完)



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![50年前的登月程序和程序员有多硬核](https://coolshell.cn/wp-content/uploads/2019/07/1920px-Margaret_Hamilton_-_restoration-e1563697198766-1-150x150.jpg)](https://coolshell.cn/articles/19612.html)[50年前的登月程序和程序员有多硬核](https://coolshell.cn/articles/19612.html)
* [![Leetcode 编程训练](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/29.jpg)](https://coolshell.cn/articles/12052.html)[Leetcode 编程训练](https://coolshell.cn/articles/12052.html)
* [![Bret Victor – Inventing on Principle](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/24.jpg)](https://coolshell.cn/articles/6775.html)[Bret Victor – Inventing on Principle](https://coolshell.cn/articles/6775.html)
* [![聊聊团队协同和协同工具](https://coolshell.cn/wp-content/uploads/2022/10/communication-150x150.png)](https://coolshell.cn/articles/22298.html)[聊聊团队协同和协同工具](https://coolshell.cn/articles/22298.html)
* [![“一把梭：REST API 全用 POST”](https://coolshell.cn/wp-content/uploads/2022/02/http_method-150x150.png)](https://coolshell.cn/articles/22173.html)[“一把梭：REST API 全用 POST”](https://coolshell.cn/articles/22173.html)
* [![谈谈公司对员工的监控](https://coolshell.cn/wp-content/uploads/2022/02/monitoring-150x150.jpeg)](https://coolshell.cn/articles/22157.html)[谈谈公司对员工的监控](https://coolshell.cn/articles/22157.html)
The post [Bret Victor – Learnable Programming](https://coolshell.cn/articles/8387.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).