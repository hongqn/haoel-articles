---
layout: post
title: SOAP的S是Simple
date: 2011/1/27/ 0:47:56
updated: 2011/1/27/ 0:47:56
status: publish
published: true
type: post
---

曾经有一个争论，一边是站在SOAP这边的人，另一边则是其它人。 站在SOAP这边人，当他们在争论SOAP和Web Service框架的复杂度时，SOAP这边的人说，在引入那些WS-\*东东之前，SOAP的确是简单的，这就是为什么SOAP的第一个字母S就是Simple。


在2000年的时候，有一个苦恼的程序员，


**程序员**: 不好意思，我的老板这周末去打高尔夫了，现在我不得不要搞一个SOAP的应用，但是我根本不知道什么是SOAP。SOAP专家，你能帮我吗？


**SOAP专家**: 当然可以。首先，我要告诉你，SOAP 就是 Simple Object Access Protocol.


**程序员**: 哦，那么说来，他是简单的罗？


**SOAP专家**: 简单的就像星期天一样，我的朋友。


**程序员**: OK，快跟我说说。


**SOAP专家**: 好，就像他的名字一样，SOAP用为远程对象访问。


**程序员**: 像CORBA一样？


**SOAP专家**: 正是如此，就是像 CORBA，只是更简单。不需要复杂的传输协议，还要设置防火墙，SOAP用的是HTTP。而且我们用的是XML作为传输数据格式而不是二进制。



**程序员**: 听起来很不错哦，告诉我它是怎么工作的？


**SOAP专家**: 没问题。首先，有一个SOAP信封，其相当的简单。就是一个XML文件由head和body组成。在body中进行你的RPC调用。


**程序员**: 哦，这就是所有的RPC的东西？


**SOAP专家**: 确对是的。就像我所说的，你的RPC调用的方法名和其参数都需要写的这个XML文档的body中。方法名是在最外层的tag，每一个嵌套的子tag就是其参数。并且所有参数的类型都可以被指定，请看能规格说明书的第五节。


**程序员**: (阅读第五节) 还好，不算太坏。


**SOAP专家**: 现在，当你的服务开发完后，你需要指定endpoint.


**程序员**: Endpoint?


**SOAP专家**: Endpoint, 就是服务的地址。你需要使用HTTP的 POST 方法把SOAP 信封放到 endpoint的 URL.


**程序员**: 如果我使用HTTP的GET方法什么怎么样？


**SOAP专家**: 不知道，使用GET的行为 undefined.


**程序员**: 哼哼。那么，要是我把我的服务移到别的 endpoint上？我是否可以得到一个301错误？


**SOAP专家**: 不会的，SOAP不会返回HTTP的错误码。


**程序员**: 那么，当你说SOAP使用HTTP，你的意思是说SOAP在HTTP打了个洞？


**SOAP专家**: 哦，别说得那么难听，应该说， SOAP 是一个传输协议。


**程序员**: HTTP 就不是吗？那是应用层的协议啊。总之，SOAP支持了别的什么传输协议？


**SOAP专家**: 官方地来说没有。但是你可以潜在地支持任何的协议。而且有许多的平台支持JMS，FTP还有SMTP。


**程序员**: 有人用那那些协议吗？


**SOAP专家**: 嗯，没有。不过，我想表达的是，你能够。


**程序员**: 好吧。关于 SOAPAction HTTP header，这是用来做什么的？


**SOAP专家**: 老实说，没人真正的知道。


**程序员**: 那么，那些 ‘actor’ 和 ‘mustUnderstand’ 属性，是否有人用呢？


**SOAP专家**: 没有，真的没人用。你就忽略这些东西吧。


**程序员**: 好吧，让我现读一读SOAP的规格说明书。


(程序员阅读中……)


**程序员**: 好了，我现在几乎可以做个简单的东西了，但是我不能说我喜欢这个远程过程调用RPC的方法以及其序列化对象的方式 。


**SOAP专家**: RPC！对象序列化！你从哪得到的SOAP就是一堆RPC的这种印象？! SOAP是关于基于文档的消息传递啊，我的朋友。


**程序员**: 但是，这是你说的……


**SOAP专家**: 忘了我所说的吧。现在，让我们谈谈消息传递吧。其消息格式遵守XML Schema，我们把之称为新型的文件格式。


**程序员**: XML Schema?


**SOAP专家**: 哦，这是很不错的东西，未来的头等技术，你应该看一下。


**程序员**: (阅读 Schema 规格说明书). 上帝保佑我们！就算是亚历山大帝也搞不定它啊。


**SOAP专家**: 不必太担心。会有专门的工作为你来创建XML Schema。真的，这只不过就是工具上的事。


**程序员**: 工具是怎么做的？


**SOAP专家**: 好吧，他们反映了你的代码，并自动生成Schema。


**程序员**: 反映了我的代码？我以为这只是文档，而不是对象序列化。


**SOAP专家**: 你没听我说吗？这只不是工具上的事。总之，我们不能期望你来手写 XML Schema 和 WSDL。另外，这其实就是一种校正测量。你不需要读的。


**程序员**:  喔喔，等一下，你刚才说的那个单词是什么？ Wizzdle?


**SOAP专家**: 哦，我没有说过吗？WSDL. Web Services Description Language. 它让你指定你的数据类型，参数，操作名，传输绑定，以及endpoint URI，这样，所有的客户程序员就可以访问你的服务了。你应该看看。


**程序员**: (阅读WSDL 规格说明书)。我相信那个写下这个文章的人已经被枪杀了。其内部说明都不一致。而且，其用的是HTTP GET绑定，你不是和我说过， GET 是 undefined吗.


**SOAP专家**: 不必担心那个，没人会用那玩意。总之，工具会帮你生成WSDL，而且在WDSL里会有Schema的。


**程序员**: 但是，不应该用别的方法吗？不应该是先设计好接口然后再是生成代码吗？


**SOAP专家**: 是的，我猜那在原则上听起来是对的。但做起来并不容易，只有很少的SOAP栈支持先开发WSDL。让工具为这个事操心去吧。


**程序员**: 还有一个问题。如果我们传递 XML Schema 的消息，我们在哪里指写操作名？


**SOAP专家**: 好吧，你还记得 SOAPAction HTTP header吗? 绝大多数的人把操作名放在那里。


**程序员**: 大多数人？


**SOAP专家**: 嗯，这种新型并不会被写在所有的地方。


**程序员**: 我注意到你们整个SOAP界有很多的模糊和歧意，有些地方还是错的，并没有标准的规格说明书。实际上， SOAP 和 WSDL 规格说明书只是 W3C 的笔记罢了，连草稿都不是。


**SOAP专家**: 我们还在继续中。


**程序员**: 这个真的能行吗？能承诺吗？


**SOAP专家**: 绝对没有问题。


**程序员**: 好吧，那我去试试。


(不久以后……)


**程序员**: 事情变得很恶心。我这边的工具生成的WDSL居然不能被我同事的工具使用。还不仅仅是这个，其生成的XML Schemas 无法重用。而且，好像没有工具可以最好的处理SOAPAction header.


**SOAP专家**:  很报歉，兄弟。在光明的那一面，没人用这些文件。为了让传输独立，我们所有人都用包装好的文件。听着是不是很酷：包装好的文件？


**程序员**: 那是什么？


**SOAP专家**: 就像是原来那样，只不过，你整个消息被 包装起来成一个元素，其和操作有一样的名字。现在操作名和消息成了一体了。


**程序员**: 好吧，请问说明书在哪里？


**SOAP专家**: 哦，没有规格说明书。这只是Microsoft自己搞的。不过应该是个很不错的主意，挺不错的。然后，这是一个新玩意。我想你一定会喜欢它的—— Web Services Interoperability Group，简称 WS-I，它就是为了移除 SOAP 和 WSDL 规格说明书中的那些歧义。我知道你有多么喜欢规格说明书。


**程序员**: 所以，换句话说，原来的那些规格说明书太糟糕了，以致于你需要一个标准化的东西来标准化这些标准。上帝啊。好吧，那么，是否这些协调问题被 解决了？


**SOAP专家**: 当然，只要你使用 WS-I 的 SOAP 栈，就可以减少使用80%的 XML Schema，别用任何不同寻常的数据类型，也别期望可以和WebSphere和 Apache Axis一起运行。


**程序员**: 那么，是否包装的文件被在那里被解释了？


**SOAP专家**: 没有，但是你的工具会明白的。绝大多数，总之。


**程序员**: 让我总结一下，SOAP的定义是不变的，SOAP可以是任何东西，但就是简单，它不再意味着对象访问，就算是所有的工具都那样做。


**SOAP专家**: 基本上是对的，但是我们走得比你要远一些。我们不赞成SOAP缩写的含义。


**程序员**: 真的！那么SOAP是什么的缩写？


**SOAP专家**: 什么也不是，就是SOAP.


**程序员**: (无语中……)


**SOAP专家**: 下面让我来告诉你什么是 UDDI。


（注：我以前还认真地学过SOAP，不过真是学不懂。）


原文：[来源](http://harmful.cat-v.org/software/xml/soap/simple)



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![那些炒作过度的技术和概念](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/2.jpg)](https://coolshell.cn/articles/3609.html)[那些炒作过度的技术和概念](https://coolshell.cn/articles/3609.html)
* [![PFIF网上寻人协议](https://coolshell.cn/wp-content/uploads/2013/04/Google-Person-Finder-150x150.png)](https://coolshell.cn/articles/9508.html)[PFIF网上寻人协议](https://coolshell.cn/articles/9508.html)
* [![语言的数据亲和力](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/3.jpg)](https://coolshell.cn/articles/4905.html)[语言的数据亲和力](https://coolshell.cn/articles/4905.html)
* [![Web开发人员速查卡](https://coolshell.cn/wp-content/uploads/2011/02/1128-150x150.jpg)](https://coolshell.cn/articles/3684.html)[Web开发人员速查卡](https://coolshell.cn/articles/3684.html)
* [![信XML，得自信](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/9.jpg)](https://coolshell.cn/articles/3498.html)[信XML，得自信](https://coolshell.cn/articles/3498.html)
* [![信XML，得永生！](https://coolshell.cn/wp-content/plugins/wordpress-23-related-posts-plugin/static/thumbs/16.jpg)](https://coolshell.cn/articles/2504.html)[信XML，得永生！](https://coolshell.cn/articles/2504.html)
The post [SOAP的S是Simple](https://coolshell.cn/articles/3585.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).