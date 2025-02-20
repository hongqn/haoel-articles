---
layout: post
title: 与Martin Fowler关于敏捷方法的问答
date: 2009/7/5/ 2:15:1
updated: 2009/7/5/ 2:15:1
status: publish
published: true
type: post
---

2009年6月23日，Martin Fowler到公司访问，与我们开了一个小型座谈会并顺便拜访了他在ThoughtWorks的同事们。


![MeetMartinFowlerSmall](https://coolshell.cn/wp-content/uploads/2009/07/MeetMartinFowlerSmall.JPG "MeetMartinFowlerSmall")


以下是座谈的内容：



**1、如何在常规业务中应用敏捷方法？** 


常规业务（Business As Usual）是指使公司业务正常运营而进行的一些日常业务活动，对于IT部门而言则包括系统维护、技术支持以及应用更改。这些工作相对于独立的软件项目而言即琐碎又零散，但又是不可或缺的。“如何在常规业务中应用敏捷方法？”，这是我们向Martin提出的第一个问题。Martin阐述道，首先需要澄清一下对项目的定义，传统的项目运作方式是集中一批业务人员、开发人员和管理人员进行产品开发，开发完成后将产品交付系统运行和支持部门，项目也就随之结束了。在敏捷方法中，项目是一个持续性的过程，系统随着业务的需要不断地更改和重构，参与项目的人员也相应地在不断地增加或者减少。笔者的理解是只要系统仍在支持业务运营，项目就不会结束，因为业务几乎不可能不变更，并且必要的重构也不可避免，对于ThoughtWorks的顾问们来说这意味着他们和客户的业务关系也不会结束，呵呵，双赢的策略！


**2、集中式办公和分布式办公** 


Martin强烈反对项目成员分散式办公，甚至觉得如果你需要业务人员每天到你的办公室来访问你，那简直是不可接受的，至少你应该每天都去拜访他们。“It is a shame if the business stakeholders need to come to your office every day”大意如此。但是现实却是，对于很多公司而言，将业务经理、项目经理、业务分析人员、开发人员和测试人员都集中在一个办公室简直就是一件不可能完成的任务。笔者目前所在的项目有三个团队，一个在悉尼，两个在墨尔本，每周进行四次远程视频会议，同时通过使用电话、即时消息系统、电子邮件、项目WiKi系统等手段来解决分布办公带来的沟通不及时和信息不透明等问题。Martin最后也不得不承认，很多时候如果实在不能够做到集中式办公，那只有准备好为此付出一定的成本。笔者认为要做到完全的集中式办公可能不太现实，不过可以尽可能在异地团队之间保持相关业务的对等沟通，比如在各个团队中都尽可能安排项目相关的各类角色，如：业务经理、项目经理、开发人员等，让这些人员与在异地的相同职能的人员沟通，然后再将信息在各自的团队内消化和共享，这样的效果也许会好于纯粹的按照职能来分布团队。


**3、交叉技能（Cross Skills）**


这里主要讲的是BA（Business Analyst 业务分析人员）和QA（Quality Assurance 质量保证人员或测试人员），Martin说在理想的情况下，BA和QA的角色可以合并，开发人员和QA的角色也可以互换。因为BA和QA都需要对系统功能有很清晰全面的了解，他们也是系统测试的主要参与者和鉴定者，他们用来定义系统功能的主要文档是用户故事（Story），而用来测试系统功能的则是功能测试代码，测试人员和开发人员有责任将功能测试代码写得易于阅读，特别是对于BA，如果他们能够象阅读用户故事一样阅读功能测试代码，将会提高他们测试系统的效率和兴趣。这也是在功能测试中使用领域特定语言（Domain Specific Language）的目的，如果BA和QA都能够阅读和使用DSL编写测试代码，那该多好啊！（憧憬中…） 通过让开发人员轮换地担任QA的角色，可以帮助提高测试代码的质量，也可以让开发人员真正从用户的角度来考虑系统功能的设计，还可以建立相互信任、相互尊重（appreciate each others work）的良好氛围。


**4、设计和编码** 


一位同事谈到对业务模型缺乏了解会导致代码难于理解，有时候即使代码的质量过关并且系统功能都在正常工作，但是系统的设计却和业务模型出现很大的偏差。“ 在实现设计之前，开发人员需要正确理解整个业务模型（The big picture）”，这是被经常提及的解决方法之一。Martin对此却不置可否，当然能够理解整个业务模型是最理想的情况，但是往往很少有人能够做到这一点，即便能够做到，业务模型也会随着时间和具体情况而变更。Martin首先认为设计和编码不是两个分离的过程，开发人员在设计过程中编码，也在编码过程中设计。开发人员在编码的过程中实现自己当前对业务模型的了解，首先让功能模块工作起来（Get it working），同时考虑如何让代码更便于日后的必要的重构，随着时间的推移，开发人员对业务模型的了解会不断清晰和全面，只要代码易于重构，整个系统的设计和实现将会不断地、最终地符合业务模型。


**5、公司内部的开源项目，鼓励用户参与产品开发** 


很多公司里不同的IT部门可能会重复开发相同功能的产品，这样会导致很大的资源浪费，用户也会面临选择的难题。再者，Martin发现很多IT部门对用户提出的功能需求缺乏足够快的响应速度，主要原因是开发人员资源有限，即使再玩命地工作也不可能在用户的预期时间内处理完本来就很长的功能需求队列。典型的例子是：公司有两个IT部门A和B，A部门需要B部门对邮政编码的Web Service做一个功能更改，而B部门的开发人员正忙于处理n个之前提交的功能需求，所以A部门的需求只能在队列中耐心等待直到B部门有开发人员空闲。如何缩短用户的等待时间？Martin建议如果A部门有开发人员熟悉Web Services，他可以从B部门的源代码库中提取邮政编码Web Service的代码，并且编码实现他需要的功能，完成之后生成代码包提交给B部门审核和测试，通过后就可以将代码合并到代码库中。这样做的优点是：1. 将功能需求由开发部门驱动转变为用户驱动，因为用户是真正了解并需要这个功能的人，所以用户会更为迫切地运用各种手段实现该功能，同时保证功能如其预期的那样运行。 2. 缩短开发周期，如果用户不愿意等待的话他可以立即着手开始功能的实现，而不必等待B部门的人员。3. 有利于公司内部的知识共享和交流，即便A部门的开发人员不熟悉Web Services但是愿意学习，B部门的开发人员可以通过结对编程（Pair Programming）的方法指导对方，待对方上手之后即可返回自己的工作，相对于B部门开发人员由始至终开发整个功能而言，这仍然可以大大缩短整个开发周期。当然，公司内部的开源策略需要一些前提，首先是部门之间应该有共同的知识领域，代码和文档需要版本控制的支持，部门人员能够理解和运用结对编程。


**6、选择和运用框架** 


“It is like you buying a new PC every 2 years” 当Martin被问道“这么多的应用框架层出不穷，我们该如何选择？”的时候如是回答。每几年我们都会换一台新电脑，是因为新的电脑内存更大，处理速度更快，应用软件也更复杂，要求的系统资源也更多。我们使用框架的目的也是解决业务相关的问题，只要是对业务有利的框架，都值得花一点时间去关注。 Martin鼓励公司允许开发人员占用一定的工作时间来实验新的框架，因为不这样如何能够知道它是否对提升业务价值有帮助。当然框架在生产环境（Production Environment）中的表现是衡量的一个重要标准，因为不经过生产环境中各种复杂情况的检验，很难最终确定框架是否适用。


**（**本文系作者原创，请勿用于商业用途**，如转载请注明出自酷壳www.cocre.com）**



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![为什么敏捷方法能在软件开发中行之有效？](https://coolshell.cn/wp-content/uploads/2010/07/Martin-Flower1-150x150.jpg)](https://coolshell.cn/articles/2622.html)[为什么敏捷方法能在软件开发中行之有效？](https://coolshell.cn/articles/2622.html)
* [![ETCD的内存问题](https://coolshell.cn/wp-content/uploads/2022/05/etcd-150x150.png)](https://coolshell.cn/articles/22242.html)[ETCD的内存问题](https://coolshell.cn/articles/22242.html)
* [![Linux 相关的资源站makelinux.net](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/15.jpg)](https://coolshell.cn/articles/194.html)[Linux 相关的资源站makelinux.net](https://coolshell.cn/articles/194.html)
* [![iPad进化图](https://coolshell.cn/wp-content/uploads/2010/02/ipad-150x150.jpg)](https://coolshell.cn/articles/2086.html)[iPad进化图](https://coolshell.cn/articles/2086.html)
* [![图解SQL的Join](https://coolshell.cn/wp-content/uploads/2011/01/Inner_Join-150x150.png)](https://coolshell.cn/articles/3463.html)[图解SQL的Join](https://coolshell.cn/articles/3463.html)
* [![HTTP API 认证授权术](https://coolshell.cn/wp-content/uploads/2019/05/Authorization-360x200-1-150x150.png)](https://coolshell.cn/articles/19395.html)[HTTP API 认证授权术](https://coolshell.cn/articles/19395.html)
The post [与Martin Fowler关于敏捷方法的问答](https://coolshell.cn/articles/1113.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).