---
layout: post
title: Test-Driven Development？别逗了
date: 2011/10/17/ 0:38:15
updated: 2011/10/17/ 0:38:15
status: publish
published: true
type: post
---

这篇文章来源于Peter Sergeant在[Write More Test](http://www.writemoretests.com/) 博客上的《[Test-Driven Development? Give me a break…](http://www.writemoretests.com/2011/09/test-driven-development-give-me-break.html)》，在原文和[Reddit](http://www.reddit.com/r/programming/comments/kq001/testdriven_development_youve_gotta_be_kidding_me/) 上有很大反响。这篇文章里的很多观点在《[TDD并不是看上去的那么美](https://coolshell.cn/articles/3649.html "TDD并不是看上去的那么美")》和《[再谈敏捷和TW咨询师](https://coolshell.cn/articles/3745.html "再谈敏捷和ThoughtWorks中国咨询师")》里都出现过（我个人觉得我的观点比其更全面一些）。就像我转的《[Scrum为什么不行](https://coolshell.cn/articles/5044.html "为什么Scrum不行？")》 和《[Bob大叔和Jim Coplien对TDD的论战](https://coolshell.cn/articles/4891.html "Bob大叔和Jim Coplien对TDD的论战")》一样，从这些贴子我们可以看到——**这是一个全世界的问题，并不是只有在中国才有的问题**。


**很多敏粉都在说我在是喷敏捷，黑敏捷，向敏捷泼脏水，我只想对这些人说——**你们这样的见解很肤浅也很敏感，你们根本就没有认识到——争论，反思和不同观点的意义，你也就无法了解你们所信仰的敏捷！你们只是在肤浅和盲目地信仰和教条敏捷中的许多名词、方法和标准答案罢了。


——————————————正文开始——————————————


对于程序员来说有些事有非常危险的信号（red flag）。当我听到有人开始信仰Test-Driven Development 是 One True Programming Methodology（唯一正确的编程方法论），这就是危险信号（red flag），我开始假设你是一个劣等、没有经验的程序员，或是某些敏捷咨询师。


测试只是一个工具来**帮助你**，而不是用来证明谁比谁更虔诚，或是我的屌比你的要大，等这种愚蠢的行为。测试是用来让**程序员**得到有帮助的、更快的反馈，从而找到正确的路径，如果你搞坏一些事，其还可以用来给后人一些警告。这根本就不是一个神秘的有魔力的方法其可以让你的代码变得更好……


整个Test-Driven Development的概念是麻痹和信奉，从而让其成为你的人生观。相反的：Developer-Driven Testing，它给你和你的同事一些有用的工具来解决问题，来支持你自己，而不是那种以工具或方法为中心的让你假设其应该是那样的测试。



是不是在有些时候我们需要在写代码前写测试？当然是，比如，“修改已有的功能”，这会一个适用的场景，还有那些短小的和已定义完善的事物，或是对已被测试过的代码做一些改善。


但， 是不是你就应该需要**总是**要去先写测试？省省吧，别逗了。


这是极度白痴的行为，尤其是在设计，调查和开发的初期。让你的测试来接管你的代码（而不是影响那个模块的代码）和接管你的设计 这是一个巨大的失败，就是因为你写的那些测试范围太大太不靠谱。（陈皓注：我在《[TDD并不是看上去的那么美](https://coolshell.cn/articles/3649.html "TDD并不是看上去的那么美")》一文中说过测试案例的测试范围的问题，敏捷社区除了对我进行人身攻击外从未对此做过正面回答。）


在写代码前写测试案例在一些场景下的确很不错。然后，Test Driven Development，被敏捷专家或是其它各种五花八门的江湖骗子像神给凡人宣扬一样，这就是欺骗大众。


行动在想法之下，于是测试必需先行（所有我已看到的，所有我正在看到的都表明这是TDD的中心思想—— 你写了测试，然后你再写代码并通过测试），于是测试成为了最有用的活动并可以帮助程序员。这是错的。


就算你在一开始要写一些测试案例，但只要你想让这些测试案例更有意义，那么，你要么得让这些测试案例的测试范围更小更底层更精确，要么你就得在整个软件快要写完的时候再去写测试，要不然你就得欺骗或是篡改测试案例。在为数不多的情形下，前者是正确的——测试围绕于bug，或是小的，定义地很好的功能碎片（陈皓注：我个人理解为单元测试是目前最有效的））


把测试变成整个活动的中心因为其对程序员有用？真牛逼。老实说，控制程序员的工作流程只可能得出一条无比正确的答案——荒谬可笑。


测试帮助程序员，是因为其可以帮程序员组织自动化测试，所以才帮了程序员，而不是cargo-cult（[货物崇拜](http://zh.wikipedia.org/zh/%E8%88%B9%E8%B2%A8%E5%B4%87%E6%8B%9C)，参看《[各种流行的编程方法](https://coolshell.cn/articles/2058.html "各种流行的编程风格")》中的cargo-cult编程）——信仰一种工作流程并让所有的人或事来适应于他。


先写测试这种方法只会在“Developer Driven Testing”（程序员自己驱动的测试）下可行——关注于选取一个正确的方法让程序员更有生产力。生成一堆测试的规则并说这是唯一的真理是不正确的。


**一些讨论和想法（在此贴发出数小时后）…**


当我这篇博文发出几个小时后，其被转到了别的地方并引发了一些讨论。


在 [Hacker News](http://news.ycombinator.com/item?id=3033129) 上，有人说我提出了很多很不错的问题，并且那是真正的有理有据的观点。我在用用户名叫*peteretep* 的回复了一些。


在 [Reddit](http://www.reddit.com/r/programming/comments/kq001/testdriven_development_youve_gotta_be_kidding_me/) 上的争论更多更强。那里有很多的人觉得需要写自动化测试。并且这篇博文被大家演变成拥护测试和可实践的建议，我觉得我是误传达了我的想法，我觉得软件测试是非常重要的，而不是根据哪个方法论进行的教条主义！


——————————————正文结束——————————————


我在Reddit上看到了下面的事，我也作些评论。


* 大家在讨论很多很多的技术细节，比如如何测试私有方法，如何测试inner class，甚至还有代码。我太喜欢了，这才是真正的讨论，而不是像酷壳这边那些敏粉们说人而不说事的讨论，**那些所谓的敏捷咨询师的话里连一点技术细节都没有**。


* 并且也有人说TDD可以让你去Design，但随后就有人说，正真的Design就是Design，而不是hack 测试来强行让你Design。后面有了附和到——有**很多思想意识想用流程来代替思考，软件开发就是需要在某中上下文下去思考，而不是使用某种机制来让你思考** 。


* 我看了两极分化的大量的争论，这是我最喜欢看到事。世界就是因为有不同的观点而美好。**有反对才有争论，有争论才有思考，这才是进步的源泉，而不是统一认识，形成标准**。而对于那些党同伐异的，一听到有反对声就激动就要打压的敏粉来说，我只能认为他们的人生观世界观扭曲得就像朝鲜那样。


（全文完）


**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![“单元测试要做多细？”](https://coolshell.cn/wp-content/uploads/2012/09/fight-150x150.jpg)](https://coolshell.cn/articles/8209.html)[“单元测试要做多细？”](https://coolshell.cn/articles/8209.html)
* [![在新浪微博上关于敏捷的一些讨论](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/10.jpg)](https://coolshell.cn/articles/5143.html)[在新浪微博上关于敏捷的一些讨论](https://coolshell.cn/articles/5143.html)
* [![Bob大叔和Jim Coplien对TDD的论战](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/17.jpg)](https://coolshell.cn/articles/4891.html)[Bob大叔和Jim Coplien对TDD的论战](https://coolshell.cn/articles/4891.html)
* [![敏捷水管工](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/30.jpg)](https://coolshell.cn/articles/3778.html)[敏捷水管工](https://coolshell.cn/articles/3778.html)
* [![再谈敏捷和ThoughtWorks中国咨询师](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/26.jpg)](https://coolshell.cn/articles/3745.html)[再谈敏捷和ThoughtWorks中国咨询师](https://coolshell.cn/articles/3745.html)
* [![[转]TDD到底美还是不美？](https://coolshell.cn/wp-content/uploads/2011/02/feedback_cycle-150x150.jpg)](https://coolshell.cn/articles/3766.html)[[转]TDD到底美还是不美？](https://coolshell.cn/articles/3766.html)
The post [Test-Driven Development？别逗了](https://coolshell.cn/articles/5531.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).