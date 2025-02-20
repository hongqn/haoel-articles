---
layout: post
title: Jeff Dean的Stanford演讲
date: 2010/11/22/ 1:7:36
updated: 2010/11/22/ 1:7:36
status: publish
published: true
type: post
---

![](https://coolshell.cn/wp-content/uploads/2010/11/jeff.jpg "Jeff Dean")Google 公司的 [**Jeff Dean**](http://research.google.com/people/jeff/) 在Stanford大学做了一个非常 [**精彩的演讲**](http://stanford-online.stanford.edu/courses/ee380/101110-ee380-300.asx)（视频未墙）。我觉得我们每一个人都应该去看一看这个视频，当然，没有字幕，需要不错的听力，当然，我不可能全部翻译出来，因为我也不是完全能听懂，下面是一些相关的Notes，供你参夸，并欢迎牛人指证。


* 比较了从1999年到2010年十年来的搜索量的变化。搜索量增加了 1000 倍，而搜索速度快了5 倍。1999年，一个网页的更新最多需要一个月到两个月，而今天，只需要几秒钟，足足加快了5w倍。
* 一开始，这些大量的查询产生了大约30GB的I/O量。2004年，他们考虑过全部重写infrastructure。
* 讨论了一些关于变量长度字节对齐的东西。
* 今天的MapReduce 有400万个作业，处理将近1000PB的数据，130PB的中间数据，还有45PB的输出数据。（1PB =1024TB）关于 MapReduce （Google云计算的精髓） 的一些统计，见下图：
* ![](https://coolshell.cn/wp-content/uploads/2010/11/mapreducestats.jpg "Mapreduce Stats")



* 现在Jeff正在做一个叫Spanner的项目，这是一个跨多个数据中心的项目。在后来的Q&A中，Jeff解释了现在的数据基本上都在各个数据中心中，数据在不同数据中心间的交换几乎不可能。所以，他们需要提供一些手动的方式或是一些工作或任务来达到数据共享。这其中还需要有一些策略配置，共同的namespace，事务处理，数据一致性等等工作。


* 最后一个段落应该是最精彩的，Jeff讲了很多很有意思的东西，绝对让你受用一生：
	+ 一个大型的系统需要分解成N多的小services.（这和Amazon的很相似，一个页面的调用可能要经过几百个后台的services）
	+ 代码的性能将会是想当的重要。Jeff给了一张叫“Numbers Everyone Should Know” 的slide，如下所示，我觉得太经典了，其中的东西，如果你看过我的那篇“[**给老婆普及计算机知识**](https://coolshell.cn/articles/3236.html)”，我想我不需要多解释了。（注：1 ns = 十亿分之一秒）
	+ ![](https://coolshell.cn/wp-content/uploads/2010/11/numberseveryoneshouldknow.png "每一个程序员都应该知道的数字")
	+ 把相同的东西抽出来去建立一个系统，而不是把所有的事情交给所有的人。他说： “最后的那个功能可能会导致你怎么个系统超出了原有的复杂度”。
	+ 不要无限制地设计可扩展性。5倍到50倍的扩展性设计足够了。如果你要达到100倍的，那应该是re-arch了。
	+ Jeff很喜欢有中心主结点的架构体系，他并不喜欢分布式系统。当然，中心主结点主要是用来做控制的，而不是做数据或是计算服务的。
	+ J在一些小机器上运行多个小服务，而不在一个大机器上运行一个mongo作业。越小的单元就越容易处理，修复，负载均衡和扩展。（化繁为简）
	+ …… ……


这是一个非常不错的演讲，很让人开阔眼界。


最后，我想说说英文，很多程序员都很不喜欢英文，哎……怎么说呢？如果你今天对英文还很害怕的话，这只能怪我们的教育制度的失败。但如果你以此为借口的话，那只能怪你自己了。没有英文的能力，你的技术和认知仅限于中文圈中，而中文圈中基本上都是产商的文化。有人说，“功夫网”让我们的internet成为了局域网，而我想说，让我们成为局域网的不是那个墙，而是我们自己的世界观和英文能力。



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![一些文章和各种资源](https://coolshell.cn/wp-content/uploads/2011/09/image008-150x150.jpg)](https://coolshell.cn/articles/5224.html)[一些文章和各种资源](https://coolshell.cn/articles/5224.html)
* [![我看ChatGPT: 为啥谷歌掉了千亿美金](https://coolshell.cn/wp-content/uploads/2023/02/chatgpt-150x150.jpg)](https://coolshell.cn/articles/22398.html)[我看ChatGPT: 为啥谷歌掉了千亿美金](https://coolshell.cn/articles/22398.html)
* [![ETCD的内存问题](https://coolshell.cn/wp-content/uploads/2022/05/etcd-150x150.png)](https://coolshell.cn/articles/22242.html)[ETCD的内存问题](https://coolshell.cn/articles/22242.html)
* [![Go编程模式 ： 泛型编程](https://coolshell.cn/wp-content/uploads/2021/09/go-generics-150x150.png)](https://coolshell.cn/articles/21615.html)[Go编程模式 ： 泛型编程](https://coolshell.cn/articles/21615.html)
* [![Go编程模式：Map-Reduce](https://coolshell.cn/wp-content/uploads/2020/12/go.map_.reduce-150x150.png)](https://coolshell.cn/articles/21164.html)[Go编程模式：Map-Reduce](https://coolshell.cn/articles/21164.html)
* [![性能测试应该怎么做？](https://coolshell.cn/wp-content/uploads/2016/07/PerfTest-150x150.png)](https://coolshell.cn/articles/17381.html)[性能测试应该怎么做？](https://coolshell.cn/articles/17381.html)
The post [Jeff Dean的Stanford演讲](https://coolshell.cn/articles/3301.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).