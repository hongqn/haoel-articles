---
layout: post
title: Kent Beck 谈单元测试和持续部署
date: 2010/7/22/ 0:0:23
updated: 2010/7/22/ 0:0:23
status: publish
published: true
type: post
---

*[文章来源](http://blog.typemock.com/2010/07/video-kent-beck-on-junit-max-and-lean.html)*


2010年7月2日，Roy Osherove 和 Kent Beck 在 blog.typemock.com 进行了一次对话，话题涉及单元测试（Unit Testing），[JUnit Max](http://www.threeriversinstitute.org/junitmax/)（Kent 开发的一个单元测试的 Eclipse Plugin，不免费），和面向初创企业的精益方法（Lean Startups）。


**单元测试和 JUnit Max**  

作为软件开发方法学的大师、极限编程XP的创始人、敏捷宣言的创始人之一，Kent Beck 一直在努力最大化地利用单元测试的价值，他说一些程序员仍然认为单元测试并不是他们的工作，但是单元测试确实能够提高软件的质量。目前他正在开发 JUnit Max，这是一个 Eclipse plugin，每当程序员保存一个 Java 源文件的时候，JUnit Max 就会运行测试并报告反馈信息。测试中的错误将会如同编译错误一样被报告给程序员。JUnit Max 的核心思想是测试错误应该和编译错误一样被 IDE 报告给程序员，程序员不需要额外的菜单选项或者运行其他的工具来运行测试。特别是那些经常失败的测试，对于程序员来说是非常有价值的反馈信息。在测试驱动开发（Test Driven Development – TDD）中，我们重复着这样一个循环：“编写一个‘失败’的测试（Failing Test）” – “编码实现功能以便让测试通过”，随着开发的深入，测试越来越丰富，测试能够反馈给程序员的信息也越来越多，它们可以帮助程序员找出那些需要改进的代码。JUnit Max 能够缩短这个循环的周期，因为它更为频繁地运行测试和提供反馈。Roy 问道：“当你一个人编码的时候，你是否严格地遵循 TDD，即一定要先写测试，然后写实现代码。我个人发现这并不是一件容易做到的事情，特别是当一个人编码的时候。” Kent 回答：“视情况而定，有时候并不需要死板地遵循 TDD，比如当我在做一些探索性或者说实验性的编码时，并不需要写测试，因为我只是想尝试一下某些功能和特性。”



Roy： “你在测试驱动开发中见过的最糟糕的错误有哪些？”  

Kent：“很多程序员仅仅是拷贝和粘贴测试代码，但并不理解它们。所以我们经常能看到没有断言的测试，同时测试很多逻辑和功能的测试，过于臃肿或者过于短小的测试等等。当然这些错误在学习过程中很普遍，也是我们学习的一部分。”


Roy：“你下一步最想尝试的新概念是什么？”  

Kent：“我最近谈论的一个主题是 Software G Forces，是关于软件产品的部署频率（Frequency of Deployment），这里的部署是指面向最终用户的部署或者说发布，是生产环境而非测试环境。从前的软件产品每年（或数年）发布一个新的版本，而现在的软件产品发布频率越来越快，从每季度，每月，每周，每天，直至每小时。Kent 提及有一些非常复杂的软件产品的发布频率甚至是每天 40 到 50 次。此时 Roy 提出了一个非常好的问题：“产品发布得如此频繁，我们如何能够在这么短的时间间隔内获得用户反馈呢？”，Kent 回答道：“持续部署（Continuous Deployment）确实需要一些基础设施建设来支持，比如：自动版本回滚，自动错误检测，系统同时运行多个版本的能力，比如一个服务器集群中不同的服务器上可以运行产品的不同版本。”


Roy 问道：“当你在开发一个产品的时候，你在为客户创造价值，而持续部署创造的则是一种内在的价值，并且实施过程也是非常复杂的，你怎样投入时间去实施它呢？是否需要从产品设计的一开始就考虑这些问题呢？”，Kent 答道：“5 年之内市场上可能会有许多持续部署的产品出现，目前我们可能需要自己来寻求解决方案，因为现在它还是一个较新的领域。持续部署的重点之一是及时捕获系统错误，不仅仅是技术层面上的错误，同时也包括业务层面。以 Amazon.com 为例，他们评价系统运行的良好程度是以业务运营状况为依据的，如果销售额出现不明原因的下降，系统也会发出错误警告。”


注：为了不让文章过长，下半部分的面向初创企业的精益方法（Lean Startups）将在后面发布。



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![聊聊团队协同和协同工具](https://coolshell.cn/wp-content/uploads/2022/10/communication-150x150.png)](https://coolshell.cn/articles/22298.html)[聊聊团队协同和协同工具](https://coolshell.cn/articles/22298.html)
* [![“一把梭：REST API 全用 POST”](https://coolshell.cn/wp-content/uploads/2022/02/http_method-150x150.png)](https://coolshell.cn/articles/22173.html)[“一把梭：REST API 全用 POST”](https://coolshell.cn/articles/22173.html)
* [![谈谈公司对员工的监控](https://coolshell.cn/wp-content/uploads/2022/02/monitoring-150x150.jpeg)](https://coolshell.cn/articles/22157.html)[谈谈公司对员工的监控](https://coolshell.cn/articles/22157.html)
* [![我做系统架构的一些原则](https://coolshell.cn/wp-content/uploads/2021/12/bachelor-mechanical-eng-icon@72x-150x150.png)](https://coolshell.cn/articles/21672.html)[我做系统架构的一些原则](https://coolshell.cn/articles/21672.html)
* [![如何做一个有质量的技术分享](https://coolshell.cn/wp-content/uploads/2021/07/knowledge_sharing-300x169-1-150x150.jpeg)](https://coolshell.cn/articles/21589.html)[如何做一个有质量的技术分享](https://coolshell.cn/articles/21589.html)
* [![程序员如何把控自己的职业](https://coolshell.cn/wp-content/uploads/2020/08/programmer.01-e1596792460687-150x150.png)](https://coolshell.cn/articles/20977.html)[程序员如何把控自己的职业](https://coolshell.cn/articles/20977.html)
The post [Kent Beck 谈单元测试和持续部署](https://coolshell.cn/articles/2681.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).