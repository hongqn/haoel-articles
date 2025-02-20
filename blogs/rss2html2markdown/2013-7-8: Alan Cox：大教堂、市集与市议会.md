---
layout: post
title: Alan Cox：大教堂、市集与市议会
date: 2013/7/8/ 7:42:27
updated: 2013/7/8/ 7:42:27
status: publish
published: true
type: post
---

**（感谢网友**[**@我的上铺叫路遥**](http://weibo.com/fullofbull)**投稿）**


在网上搜到的Cox大叔于1998年在开源社区写的一篇文章，当时很轰动，明眼人一看就知道是针对ESR那篇《大教堂与市集》，从中可见Alan在项目管理风格上乃至个人性格上都与ESR、Linus等人不同之处。顺便说一句，Alan现在出于“家庭原因”已经离开了Linux项目，他曾经评价Linus是[a good developer but a terrible engineer](http://apolyton.net/showthread.php/130212-Linus-Torvalds-is-a-terrible-engineer-Alan-Cox)，甚至在Google+上直接说Linus就是一a\*sh\*\*e。不管如何，两位曾经十余年里并肩战斗惺惺相惜的大牛就此分道扬镳还是惹人唏嘘。


言归正传，以下为slashdot收录的英文原文：[Cathedrals, Bazaars and the Town Council](http://news.slashdot.org/story/98/10/13/1423253/featurecathedrals-bazaars-and-the-town-council)。


以下是一些我对市集模式的想法，我认为这值得分享，这种模式会教你如何完全毁掉一个自由软件项目。我还举了一个我称之为“市议会”(Town Council)效应的实例（虽然那些市议员们可不这么认为，注：此处指Linux项目开发者）。


关于软件开发人员，你必须去了解一些情况。首先要了解的是真正优秀的程序员相对来说并不普遍，不仅如此，在很多其它专业领域里“真正的程序员”和一些捣乱的家伙之间的区别要比“伟大”和“普通”之间的区别要大得多，研究表明生产效率上最好的同其余的比重是30:1。


其次，你需要了解的是一大堆妄想型码农(wannabe programmer)总是善于发表意见。其中很多人患上了一种叫做“流行性热词”(buzzword)疾病，或者对他们“非黑即白”(one true path)的思考方式有着特殊的偏执，网上很多讨论都是廉价的。



第三个关于软件项目的事情就是我们所谓的“闲杂人员”(the masses)。他们不是编程人员，而在其它方面有着大量贡献——文档编辑、用户支持，以及对那类经常争论你应该获得许可证才能上网的人的说服工作。


我想以Linux 8086（注，Intel设计的16位处理器架构）为例来说明如何将整个工程全部搞砸。将Linux的一个子集移植到8086上大体是这世上最无聊的活动之一。整件事的发起就像个笑话并走向失控。


只有极少数真正的程序员会将时间及其良好的精神状态（或许那是假的）花费在那些唯一价值在于“黑客精神”(Hack Value)的项目上，故而在任何时候那种项目也就两三个核心贡献人员而已。


不幸的是大批人认为将Linux运行在8086上是干净的，为此义不容辞地想要“入伙”。这类人大多属于妄想型码农之流，以至于连闲杂人员在一个安全距离之外都会沾染上这个项目的“愚蠢”因子。


问题的导火索在于一大批充满（大多善意的）危险的一知半解的人们的意识观念——不是代码，而是意识观念。他们似乎很懂得如何去编程，但很多人连“Hello World”这样的C程序都不会。他们花了几星期时间去争论并投票该使用什么编译器，甚至在项目开展一年后还在争论是否去写个充分完美的编译器。他们热衷于辩论如何生成大量二进制文件，却又对内核swapper（注，即idle task）设计一无所知。


Linux 8086项目仍然进行着，真正的开发人员将邮件列表里许多其他成员加入到清除文件(kill files)中，以便他们之间可以顺畅地通过邮件列表沟通，只因半吊子打酱油的家伙实在太多了。这一切不再是市集模式，而是形成了一个核心小组，对圈子里许多人而言这是一种礼貌用语。在这种情形下人们不可避免地处于被动位置。


像Linux这种基于用户/程序员的项目成长缓慢，虽然它是靠着一群贡献代码的人得以成长起来，但这些人的背景要么是从原始的Minix（注，一种微内核操作系统）黑客社区起家，要么通过艰难的方式不断从头学起。随着项目增长，人们本应该形成一个“Linux内核结构规划管理委员会”，而不是掉入将人们招来唤去，不将失败视为问题的怪圈，用Linus的话来说就是“给我看源码”。


如果有人陷入困境，他可以发帖询问，在这之前包括现在很大程度上都基于人们正常地拥有时间并具备知识来回复他。在Linux 8086的案例中，开发人员很长一段时间身陷囹圄。假使主动活跃的程序员对只有潜在用处的妄想型码农的比例更高一点的话，我们就可以将一些杂音转化成生产力。项目也就获得更多有用的程序员，他们可以轮流向他人传授经验，任何学习活动都会让你变得更好，哪怕只有一些少量实习生。


一些人会认为你无法将那些“次要程序员”(lesser programmer)训练成真正的程序员。就Linux项目的个人经验而言，很多人员只要获得一丁点儿的帮助和自信鼓励都将成为世界上最好的开发人员之一。只要帮助和鼓励足够多，很多人就能成功。


Linux 8086总算大部分从“侵扰”中恢复过来，可至今仍是个不起眼的小项目。你可以从CVS目录树上下载这个由Alistair Riddich领导的项目，他做了很多优秀的工作。随着市议员的撤出，人们可以询问、参与并改善这个项目。


我们从这个项目，还有其它相同命运的早期Linux 16位处理器项目（有的已死）中很清楚地学到以下几点教训。


* 从项目一开始就发布源代码。哪怕不是很有用也无关紧要，将市议会排序分类的最好方式就是发布源代码并告知人们。Linux、KDE以及GNOME都遵循这种方式并获益良多。你可以花一辈子时间去争论怎样写代码才是正确的。只要代码公布，人们（不管水平怎样）都会把玩它。


* 要欣赏那些给一点帮助就会对项目做出巨大贡献的人。如果他们最初的补丁有错误，不要盛气凌人，向其解释问题出在哪里并给出解决方案的建议，或者可以查询解决方法的地方。解答真正的问题，帮助别人，你所花费的一分一秒都会成十倍地回报在项目上，对社会也会带来无法估量的好处。[注]


* 不要忘记那些非开发人员。我难过地发现许多人问起“前5名最重要的内核成员”时却极少涉及在所有人中最重要的一些——他们负责维护网站，更新日志和邮件列表，还有编辑文档，这些都是同等重要。  

Linus那句“给我看源代码”对真正的项目来说是个狭隘的视角。当你听到人们说“我很想帮忙，可我不会编程”，那么他可以从事文档编写。当人们说“但英语不是我的第一语言”，这时你需要的是一位文档编辑或另一门语言翻译者。


* 尝试将有用的人从杂音中分离出来，将有意愿帮忙的人从一大堆无聊评论中分离出来是很难的。在Linux 8086项目中我的确错误地放弃了这一目标，如何将那些只会空谈而又无所事事的人弄走是一门学问。


下次碰到人们在项目上投票，或者问题讨论了一个月才实现这类情况，给予他们警告。这样才能使人正确地解决问题。在你看来如果一些稀奇古怪的事务不顾一切地运行着，要求他们给你发个补丁，只要能够生效的话。


小心地说“我们应该怎样”之类的话，对“我该如何做”这样的人伸出援手。


Alan


[注]这段话举个例子说明一下。Linux IPv6源码作者以前在葡萄牙上网聊天，只会简单讨论和问一些基本问题。我们助其弄明白一些内核原理之后，他写了大约75%的IPv6协议栈代码，他最近受聘于美国思科公司。


附录一：一篇针对本文的[吐槽贴](http://tech.groups.yahoo.com/group/java-os-project/message/2358?var=1&p=1)


附录二：2009年Cox回复Torvalds的[邮件](https://lkml.org/lkml/2009/7/28/375)，事情起因是Cox的一个tty patch导致[kdesu(KDE project’s su utility)](https://lkml.org/lkml/2009/7/11/125)程序无法工作，该问题争论长达两个星期，此后Alan离开了Linux项目投奔Intel。



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![Alan Cox：单向链表中prev指针的妙用](https://coolshell.cn/wp-content/uploads/2013/06/Alan-Cox-150x150.jpg)](https://coolshell.cn/articles/9859.html)[Alan Cox：单向链表中prev指针的妙用](https://coolshell.cn/articles/9859.html)
* [![Linus：利用二级指针删除单向链表](https://coolshell.cn/wp-content/uploads/2013/02/linus_pointer_to_pointer-150x150.jpg)](https://coolshell.cn/articles/8990.html)[Linus：利用二级指针删除单向链表](https://coolshell.cn/articles/8990.html)
* [![Unix传奇(上篇)](https://coolshell.cn/wp-content/uploads/2010/04/o_unixrichiethompson-150x150.jpg)](https://coolshell.cn/articles/2322.html)[Unix传奇(上篇)](https://coolshell.cn/articles/2322.html)
* [![Linus Torvalds 语录 Top 10](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/20.jpg)](https://coolshell.cn/articles/1278.html)[Linus Torvalds 语录 Top 10](https://coolshell.cn/articles/1278.html)
* [![eBPF 介绍](https://coolshell.cn/wp-content/uploads/2022/12/eBPF-150x150.jpeg)](https://coolshell.cn/articles/22320.html)[eBPF 介绍](https://coolshell.cn/articles/22320.html)
* [![打造高效的工作环境 – Shell 篇](https://coolshell.cn/wp-content/uploads/2019/03/linux.ninja_-150x150.png)](https://coolshell.cn/articles/19219.html)[打造高效的工作环境 – Shell 篇](https://coolshell.cn/articles/19219.html)
The post [Alan Cox：大教堂、市集与市议会](https://coolshell.cn/articles/9917.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).