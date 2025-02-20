---
layout: post
title: 关于Facebook 的 React 专利许可证
date: 2017/9/19/ 6:8:0
updated: 2017/9/19/ 6:8:0
status: publish
published: true
type: post
---

![](https://coolshell.cn/wp-content/uploads/2017/09/react_patent-360x200.jpg)随着Apache、百度、Wordpress都在和Facebook的React.js以及其专利许可证划清界限，似乎大家又在讨论Facebook的这个BSD+PATENT的许可证问题了。这让我想起了之前在Medium读过的一篇文章——《[React, Facebook, and the Revocable Patent License, Why It’s a Paper](https://medium.com/@dwalsh.sdlr/react-facebook-and-the-revokable-patent-license-why-its-a-paper-25c40c50b562)》，我觉得那篇文章写的不错，而且还是一个会编程的律师写的，所以有必要把这篇文章传播到中文社区这边来。注意，我不会全部翻译，我只是用我的语言来负责搬运内容和观点，我只想通过这篇文章让大家了解一下这个世界以及专利相关的知识，这样可以避免你看到某乎的“怎么看待XXX”这类的问题时人云亦云，能有自己的独立思考和自我判断。;-)


这篇文章的作者叫Dennis Walsh，他自称是亚历桑那和加利福尼亚州的律师，主要针对版权法和专利诉论的法律领域。但是这个律师不一样，他更很喜欢商业和软件多一些。现在他用React/GraphQL/Elixir在写一个汽车代理销售相关的软件，而且已经发布到第2版了。


首先，作者表明，专利法经常被人误解，因为其实充满了各种晦涩难懂的法律术语，所以，作者用个例子来讲述专利的一个原则 —— **专利并不是授于让你制造或开发的权利，而是授予你可以排他的权利。（**事实上似乎也是这样，申请专利很多时候都不是为了制作相关的产品，而是为了防止别人使用类似的技术制作相关的产品）



如果有公司X为铅笔申请了专利，而另一家公司Y为把用于铅笔的橡皮擦申请了专利。那么，公司X可以阻止公司Y来生产铅笔，而对带橡皮擦的铅笔没办法，但是公司Y的专利可以让公司X不能生产带有橡皮擦的铅笔。


所以，公司Y的橡皮擦专利又被广泛地叫作“[Blocking Patent](https://definitions.uslegal.com/b/blocking-patent/)”。公司Y不能说他发明了铅笔，因为这是公司X的专利，但是，他们可以让公司X无法对铅笔做出某些改进。


于是，因为这种 Blocking Patent 存在，对于开源的公司是不利的，因为根据上面的那个例子来说，开源公司就是公司X，他们做了一个基础的软件，而公司Y在上面做了些改进，并注册成了专利，从而导致开源的公司X无法对它基础开源软件作出被公司Y专利阻止的改进，开源的公司X希望能够自由地使用公司Y的橡皮擦专利，因为毕竟是它发明了铅笔并放弃了铅笔的专利。


于是就出来了“专利反击条款”（[Patent Retaliation Clauses](https://en.wikipedia.org/wiki/Software_patents_and_free_software#Patent_retaliation)）。一般来说有两种专利条款，一种是弱条款，一种是强条款。


Weak Patent Retaliation Clauses – 这种条款声明，如果许可证持有者用某个专利来打击许可证颁布者，那么专利就视为终止。用人话来表达就是，公司X做了一个开源铅笔，而公司Y注册了橡皮檫专利。此时，公司X做了一支带像皮擦的铅笔，而公司Y马上对公司X提起专利侵权诉讼。那么，公司Y就失去了对底层铅笔的专利控制。（正如前面所说的，公司Y的橡皮擦专利因为在起诉公司X的开源铅笔，而失去了对开源铅笔的专利排他权利）


Strong Patent Retailiation Clauses – 这种条款声明比“弱条款”要的更多。具体来说就是，任何专利声明终结许可证，而不管这个专利有没有和你基础的软件有关系。用人话来说就是，公司Y使用他们的热气球专利来起诉公司X，那么公司Y就失去了他们对铅笔的专利限制。


我个人理解起来，这两种条款看上去是防御性质的。


Facebook的React的Patent License如下：



> The license granted hereunder will terminate, automatically and without notice,if you (or any of your subsidiaries, corporate affiliates or agents) initiatedirectly or indirectly, or take a direct financial interest in, any Patent Assertion: (i) against Facebook or any of its subsidiaries or corporateaffiliates, (ii) against any party if such Patent Assertion arises in whole orin part from any software, technology, product or service of Facebook or any ofits subsidiaries or corporate affiliates, or (iii) against any party relating to the Software. Notwithstanding the foregoing, if Facebook or any of itssubsidiaries or corporate affiliates files a lawsuit alleging patentinfringement against you in the first instance, and you respond by filing apatent infringement counterclaim in that lawsuit against that party that isunrelated to the Software, the license granted hereunder will not terminateunder section (i) of this paragraph due to such counterclaim.
> 
> 


这些条款中和基础软件没有任何关系，所以，**这个条款是“强专利反击条款”**。


在后面，本文的作者又解解释了，为什么React的“强专利反击条款”就跟没有似的。他在文中针对一些歇斯底里的言论，如：“Facebook不用害怕专利诉讼了，而且他可以随时偷袭你家的专利仓库”，也作出了一些解释来分析这个事。


Contractural Liability – 意思是说，专利方面的东西只会影响专利上的事，而不会影响和专利无关的事，React底层协议是BSD-3许可证还是会被保留。换句话说，React的“强专利反击条款”只生效于专利层面，而不会对非常专利的软件使用产生问题，如果和专利无关，React还是走BSD-3的许可协议。


Copyright Liability – 这个和Contractural Liablitity 一样。作者说，如果有人有特别的案例或是有说服力的论据来说明Facebook的这个条款会作用于非专利的地方，那么，请告诉他。


Patent Liability – 专利的责任和损害是两件事，非专业人士总是会把其搞混。


第一个问题是Liability， 要搞清这个事，得搞清“Patent’s Claims”，而不是这个技术的技术规格说明，技术规格说明和权力主张是两码事。作者说，现在的很多专利都是一些想法，很多投机份子随便一拍脑袋就发明出一个想法，然后就去注册专利了。但是可以被用来法律执行的只有“Patent’s Claims”（专利的权利主张），而不是那些想法。这些权利主张相当相当的晦涩难读，而且是会故意被模糊掉的，因为，当你清楚的定义了你的发明是什么，那么，就可以清楚的定义出来什么不是你的发明。比如：一个铅笔专利权利主张里说，“这一个用石墨和木头组合起来的写字工具”，那么，只要我不用木头和石墨来做组合，而是用塑料来做组合，那么我就不是专利侵权。所以，一般来说，专利主张是会更为通用一些，比如，“这是一个用于涂画表面的装置，其包括：与涂画端相连的握持端”。作者这里给了一个[苹果公司的滑动解锁专利](https://www.google.com/patents/US8046721)的示例。可以感受一下产品规格说明和专利权利主张完全是两码事。


专利这些事，在法律界里是非常非常困难作出评估的。所以，这个社会每年都会给律师们几十亿美金来一遍又一遍地回答这些问题，而且律师还经常回答错了。而对于美国的法律，对于专利诉讼会有一个叫[Markman hearing的审前听证会](https://en.wikipedia.org/wiki/Markman_hearing)（马克曼听证会），自从1996年美国最高法的“[马克曼诉威斯幽仪器公司案](https://en.wikipedia.org/wiki/Markman_v._Westview_Instruments,_Inc.)”这个听证会就变成了一个惯例，美国联邦法院用这个听证会来向决定专利权利主张的解释，而且，上诉法院还经常性的推翻审判法院的裁决。（对于美国法律来说，一般是法官认证法律，陪审团认定事实，然而，对于专利而言，1996年的那个案件认为专利术语是一个需要法官决定的法律问题，而不是陪审团决定的事实问题。关于马克曼听证会的事，可以参看本文未尾的附录）


所以，要决定Facebook的专利责任，我们需要评估Facebook的专利及其权利主张，而不是技术规格说明。具体来说，要明确Facebook对于React这个底层技术的专利权利主张是什么？但是作者搜了一下，发现什么也没有找到。也就是说，对于USPTO（美国专利商标局）或法院来说，他们没办法对Facebook的这样没有为React申请专利的方式来执行任何和专利的诉讼，也就是说，Facebook的这个React License的条款，美国政府是无法在法律上支持的。


第二个问题是专利损害。就算是Facebook可以评估出来一个合法可执行的专利来保护React，对于专利损害也是很有问题的。作者说他到目前还没有发现一个开源软件被专利侵权的事，就算有这样的案例，也不会是这里说的这个事。作者觉得在这个事上操作起来就是一个笑话。


另外，作者认为，React 专利许可证这个事就是个纸老虎。因为，一方面，这个专利不像电信通讯里的那些专利，你拿不掉。作者认为要从你的代码中把React去掉虽然难，但是也不是什么很难的事，另外，要打这样的专利官司，一般来说，在美国至少要花100-200万美金的费用才能发起诉讼，而要胜诉则需要需要200多万到2000万美金的费用，你觉得你要花多钱才能把React从你的代码库中剔除？肯定比这钱少。


作者还认为，Facebook玩这个事虽然出发点不错，但是感觉并不聪明，从目前的情况看下来，就像他想咬你一口，但却没有牙。


后面，作者还说了一下，转成别的框架会不会有问题？比如：你用Preact/Vue或是你自研的东西？作者说，未必，如果Facebook真的为React注册了专利，比如：React里的组件技术、虚拟DOM渲染技术等等。那么，你用Preact/Vue或是带这样技术的自研的框架，那么，从你使用的第一天就在侵犯Facebook的专利权了。然而，使用React反而不会有这么大的风险，因为Facebook让你免费的用React。作者说，用别的框架的法律风险比用其它替代品的风险更高。


后面，作者也更新了一篇文章 《[Using GraphQL? Why Facebook Now Owns You](https://medium.com/@dwalsh.sdlr/using-graphql-why-facebook-now-owns-you-3182751028c9)》，意思是，用React可能还好，但是用GraphQL就有问题了。因为找到了GraphQL的专利—— [“Graph Query Logic”](https://patents.google.com/patent/US9646028)。


后来我查了一下，我发现，React也有个相关的专利—— “[Efficient event delegation in browser scripts](https://patents.google.com/patent/US9003278) ”，看上去和虚拟DOM渲染有关。Holy Shit!


好了，用还是不用React我也不知道，总之，这个世界比较复杂，我只是想借这篇文章来学习一下法律上的相关东西，欢迎听到大家的观点。


最后，请允许我调侃一下来结束本文——“不用担心React的许可证问题，因为前端不是一年半就用新的框架重写一次么？”哈哈。


**更新：Facebook官方于20017年9月23日在其官方blog上发贴《[Relicensing React, Jest, Flow, and Immutable.js](https://code.facebook.com/posts/300798627056246/relicensing-react-jest-flow-and-immutable-js)》决定取消之前的带专利的许可证。**


#### 延伸阅读


##### 马克曼听证会 – Markman Hearing


马克曼听证会的一些背景知识，下面的文字来源于《[“马克曼听证”制度的由来及启示](http://www.sipo.gov.cn/sipo2013/mtjj/2013/201303/t20130320_788543.html)》


与美国专利诉讼的悠长历史相比，1996年才经美国最高法院确立的“马克曼听证”（Markman Hearing，也称为Claim Construction，即权利要求书的解释）无疑是一项年轻的制度。但由于几乎所有的专利侵权诉讼中都会遇到涉案专利权利要求书的解释这一核心问题，且因“马克曼听证”结果往往清楚地预示了案件结果，经“马克曼听证”获得有利结论的一方一旦据此向法庭提起不审即判的动议，专利侵权诉讼往往可就此快速了结，因此该制度的确立成为美国专利诉讼历史上的一件大事。


“马克曼听证”制度的由来


“马克曼听证”制度确立之前，在专利侵权诉讼中的权利要求书解释，通常交由陪审团在对案件事实进行裁决时一并做出，且并不会在诉讼文件上单独就陪审团这一问题的判断进行记录。1991年，马克曼（Markman）先生因认为其拥有的专利号为RE33054的“干洗衣物贮存及追踪控制装置”专利权被Westview公司所侵犯，遂向宾夕法尼亚州东区联邦地方法院提起了专利侵权诉讼。


该专利是用扫描的方式，将客户的衣物编号扫描后输入电脑中做分类标示，并在衣物干洗过程中追踪衣物位置，干洗完成后自动将衣物放回客户固定的存贮位置。被告的产品则是同时运用扫描器和电脑两种方式，将客户干洗衣物的资料存入电脑并显示费用、日期等相关信息。本案陪审团的裁决认为被告装置构成对原告专利权利的侵犯，但该地方法院认为系争专利与被告装置在功能实施上并不一致，遂推翻陪审团的裁决，判决被告不构成侵权。


马克曼不服，于1995年向联邦上诉法院提起上诉，但其上诉理由仅为联邦地方法院错误地解释了陪审团关于专利权利要求书解释中某个词语的涵义。联邦上诉法院在审理该案时，将案件的核心问题定为两个：一是原告对于请求项解释有无权利请求陪审团裁决;二是联邦地方法院是否正确地解释了“Inventory”一词。该院多数法官经审理后认为，权利要求书范围的解释与确定，属于法律问题而非事实问题，因而属于法院权限，而不应交由陪审团决定，且此前将此问题交由陪审团确定并不妥当。同时，由于认为原告专利与被告装置存在实质功能上的差异，联邦上诉法院亦不认为被告构成专利侵权。少数持不同意见的该院法官主要是质疑这一结论违反了美国第七宪法修正案（即所有根据美国法律进行的普通法诉讼，只要争议金额超过20美元，即有要求陪审团审判的权利）。


马克曼不服，向最高法院提出上诉。1996年4月23日，美国最高法院就马克曼诉Westview器械公司案（Markman v. Westview Instruments, Inc. 517 U.S. 370 （1996））做出终审裁决，裁决认定：权利要求书的解释是联邦地区法院法官应当处理的法律问题，而不是应当由陪审团来认定的事实问题，尽管在解释权利要求书的过程中可能会包含一些对于事实问题的解释，且这样做并不违反第七修正案赋予给陪审团的权利。这一裁决标志着“马克曼听证”制度的正式确立。


“马克曼听证”制度的不足


该案判决是美国专利诉讼史上的一个重大转折。“马克曼听证”成为法官专门用于解释专利权利要求的一个经常性听证程序，用以解决专利侵权诉讼的核心问题。由于该听证并非普遍适用，因此，十几年来，联邦民事诉讼规则并未正式对其有任何规定，而是给予法院绝对的自由裁量权。但是，何时可以进行“马克曼听证”?如何进行?是否有必要进行?类似问题在一定程度上困扰了审理专利侵权案件较多的法院。


2001年，加州北区联邦地区法院率先制定了供本法院使用的专利审判专属规则（Patent Local Rules），其中第四部分即为权利要求书的解释程序（Claim Construction Proceddings），对“马克曼听证”的时间、流程、限制及当事人的义务均进行了规定。此后，各州纷纷效仿。目前，乔治亚州北区联邦法院、得克萨斯州东区联邦法院、得克萨斯州南区联邦法院、宾夕法尼亚州西区联邦法院等都制订了书面的“马克曼听证”程序指南。近年来，不断有新的案例在解释与细化着“马克曼听证”，如2006年的Wilson Sporting Goods Co.诉Hillerich & Bradsby Co.案，2005年的Phillips诉AWH Corp.案，2008年的Howmedica Osteonics Corp.诉Wright Medical Technology, Inc.案，这些司法实践大大拓展与丰富了“马克曼听证”使用的实体和程序规则，使之日渐成为美国专利诉讼中一个复杂、完备的司法程序。以至于竟然有人开发了模拟“马克曼听证”程序，只要你愿意，可以下载并训练，以熟悉和确保有真正的权利要求书解释时不会出现不利于自己的问题。


但是，该听证带来的问题也逐渐受到重视。有人质疑说该程序导致专利诉讼费用增加，因为“马克曼听证”通常会单独进行，且程序复杂，因此导致当事人花费大量的时间与精力，更为重要的是，由于40%至60%的联邦地区法院案件会在联邦巡回上诉法院被推翻，因此，花费巨大的“马克曼听证”似乎价值有限。同时，权利要求书的解释要求是不多不少，忠实于技术发明思想与发明事实，但由于地区法院分散，法官的相关技术知识不十分专业，将权利要求书解释这样的问题交给他们，难免会带来一些无法克服的问题。


“马克曼听证”制度的启示


我国民事诉讼中并无陪审团制度，案件的事实问题与法律问题均由法官审理与确定。在专利侵权诉讼中，对于案件中涉及到的技术问题可以通过专家鉴定等方式解决，但并不因此免除法官审理案件的义务，即法律问题的判断归于法官，事实的法律属性判断仍然归于法官。同时，权利要求书的解释在我国的专利侵权诉讼中并不是一个单独的程序，而是合并在案件审理过程中。因此，仅就我国的司法审判而言，“马克曼听证”制度并无直接的借鉴意义。


但是，对于那些已经走出和正在走出国门的企业来说，了解与掌握这一重要的专利诉讼程序却是极其重要的。通领科技集团的积极尝试充分证明了这一点，而且随着这一程序的不断成熟，美国国际贸易法院（ITC）也开始在审理时适用“马克曼听证”制度。所以，知道“马克曼听证”意味着什么，确保所提交的用于解释权利要求的文件确实充分，学会利用“马克曼听证”，无论是对于破解美国的专利诉讼威胁，还是为未来准备有效的法律武器，无疑都非常重要。（知识产权报　作者　魏玮）


 


（全文完）



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![程序员练级攻略（2018)  与我的专栏](https://coolshell.cn/wp-content/uploads/2018/05/300x262-150x150.jpg)](https://coolshell.cn/articles/18360.html)[程序员练级攻略（2018) 与我的专栏](https://coolshell.cn/articles/18360.html)
* [![扎克伯格的一封信：关于Facebook IPO](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/15.jpg)](https://coolshell.cn/articles/7448.html)[扎克伯格的一封信：关于Facebook IPO](https://coolshell.cn/articles/7448.html)
* [![Quora使用到的技术](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/29.jpg)](https://coolshell.cn/articles/4939.html)[Quora使用到的技术](https://coolshell.cn/articles/4939.html)
* [![Facebook 的系统架构](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/7.jpg)](https://coolshell.cn/articles/4549.html)[Facebook 的系统架构](https://coolshell.cn/articles/4549.html)
* [![Facebook全球关系网](https://coolshell.cn/wp-content/uploads/2010/12/Visualizing-Friendships-on-Facebook-150x150.png)](https://coolshell.cn/articles/3396.html)[Facebook全球关系网](https://coolshell.cn/articles/3396.html)
* [![Go 语言简介（上）— 语法](https://coolshell.cn/wp-content/uploads/2012/11/go2-150x150.jpg)](https://coolshell.cn/articles/8460.html)[Go 语言简介（上）— 语法](https://coolshell.cn/articles/8460.html)
The post [关于Facebook 的 React 专利许可证](https://coolshell.cn/articles/18140.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).