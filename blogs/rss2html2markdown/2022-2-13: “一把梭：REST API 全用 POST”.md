---
layout: post
title: “一把梭：REST API 全用 POST”
date: 2022/2/13/ 4:28:47
updated: 2022/2/13/ 4:28:47
status: publish
published: true
type: post
---

![](https://coolshell.cn/wp-content/uploads/2022/02/http_method-300x169.png)


写这篇文章的原因主要还是因为V2EX上的这个[贴子](https://www.v2ex.com/t/830030?p=1)，这个贴子中说——



> “对接同事的接口，他定义的所有接口都是 post 请求，理由是 https 用 post 更安全，之前习惯使用 restful api ，如果说 https 只有 post 请求是安全的话？那为啥还需要 get 、put 、delete ？我该如何反驳他。”
> 
> 


然后该贴中大量的回复大概有这么几种论调，1）POST挺好的，就应该这么干，沟通少，2）一把梭，早点干完早点回家，3）吵赢了又怎么样？工作而已，优雅不能当饭吃。虽然评论没有一边倒，但是也有大量的人支持。然后，我在Twitter上嘲讽了一下，用POST干一切就像看到了来你家装修工人说，“老子干活就是用钉子钉一切，什么螺丝、螺栓、卡扣、插销……通通不用，钉枪一把梭，方便，快捷，安全，干完早回家……不过，还是有一些网友觉得用POST挺好的，而且可以节约时间。所以，正好，我在《[我做系统架构的原则](https://coolshell.cn/articles/21672.html "我做系统架构的一些原则")》中的“[原则五](https://coolshell.cn/articles/21672.html#%E5%8E%9F%E5%88%99%E4%BA%94%EF%BC%9A%E5%88%B6%E5%AE%9A%E5%B9%B6%E9%81%B5%E5%BE%AA%E6%9C%8D%E4%BB%8E%E6%A0%87%E5%87%86%E3%80%81%E8%A7%84%E8%8C%83%E5%92%8C%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5)”中反对API返回码无论对错全是200的返回那，我专门写下这一篇文章，以正视听。


这篇文章主要分成下面这几个部分：


1. 为什么要用不同的HTTP动词？
2. Restful 进行复杂查询
3. 几个主要问题的回应
	* POST 更安全吗？
	* 全用 POST 可以节省时间沟通少吗？
	* 早点回家的正确姿势
	* 工作而已，优雅不能当饭吃



#### 为什么要用不同的HTTP动词


编程世界通常来说有两种逻辑：“**业务逻辑**” 和 “**控制逻辑**”。


* **业务逻辑**。就是你实现业务需求的功能的代码，就是跟用户需求强相关的代码。比如，把用户提交的数据保存起来，查询用户的数据，完成一个订单交易，为用户退款……等等，这些是业务逻辑
* **控制逻辑**。就是我们用于控制程序运行的非功能性的代码。比如，用于控制程序循环的变量和条件，使用多线程或分布式的技术，使用HTTP/TCP协议，使用什么样数据库，什么样的中间件……等等，这些跟用户需求完全没关系的东西。


网络协议也是一样的，一般来说，**几乎所有的主流网络协议都有两个部分，一个是协议头，一个是协议体。协议头中是协议自己要用的数据，协议体才是用户的数据。所以，协议头主要是用于协议的控制逻辑，而协议体则是业务逻辑。**


HTTP的动词（或是Method）是在协议头中，所以，其主要用于控制逻辑。


下面是HTTP的动词规范，一般来说，REST API 需要开发人员严格遵循下面的标准规范（参看[RFC7231 章节4.2.2 – Idempotent Methods](https://www.rfc-editor.org/rfc/rfc7231#section-4.2.2)）




| 方法 | 描述 | 幂等 |
| --- | --- | --- |
| GET | 用于查询操作，对应于数据库的 `select` 操作 | ✔︎ |
| PUT | 用于所有的信息更新，对应于数据库的 `update`操作 | ✔︎︎ |
| DELETE | 用于更新操作，对应于数据库的 `delete` 操作 | ✔︎︎ |
| POST | 用于新增操作，对应于数据库的 `insert` 操作 | ✘ |
| HEAD | 用于返回一个资源对象的“元数据”，或是用于探测API是否健康 | ✔︎ |
| PATCH | 用于局部信息的更新，对应于数据库的 `update` 操作 | ✘ |
| OPTIONS | 获取API的相关的信息。 | ✔︎ |


其中，`PUT` 和 `PACTH` 都是更新业务资源信息，如果资源对象不存在则可以新建一个，但他们两者的区别是，`PUT` 用于更新一个业务对象的所有完整信息，就像是我们通过表单提交所有的数据，而 `PACTH` 则对更为API化的数据更新操作，只需要更需要更新的字段（参看 [RFC 5789](http://tools.ietf.org/html/rfc5789) ）。


当然，现实世界中，可能并不一定严格地按照数据库操作的CRUD来理解API，比如，你有一个登录的API `/login` 你觉得这个API应该是 `GET` ，`POST`，`PUT` 还是 `PATCH` ?登录的时候用户需要输入用户名和密码，然后跟数据库里的对比（select操作）后反回一个登录的session token，然后这个token作为用户登录的状态令牌。如果按上面表格来说，应该是 select 操作进行 `GET` ，但是从语义上来说，登录并不是查询信息，应该是用户状态的更新或是新增操作（新增session），所以还是应该使用 `POST`，而 `/logout` 你可以使用 `DELETE` 。**这里相说明一下，不要机械地通过数据库的CRUD来对应这些动词，很多时候，还是要分析一下业务语义。**


**另外，我们注意到，在这个表格的最后一列中加入了“是否幂等”的，API的幂等对于控制逻辑来说是一件很重要的事。**所谓幂等，就是该API执行多次和执行一次的结果是完全一样的，没有副作用。


* `POST` 用于新增加数据，比如，新增一个交易订单，这肯定不能是幂等的
* `DELETE` 用于删除数据，一个数据删除多次和删除一次的结果是一样的，所以，是幂等的
* `PUT` 用于全部数更新，所以，是幂等的。
* `PATCH`用于局部更新，比如，更新某个字段 cnt = cnt+1，明显不可能是幂等操作。


幂等这个特性对于远程调用是一件非常关键的事，就是说，远程调用有很多时候会因为网络原因导致调用timeout，对于timeout的请求，我们是无法知道服务端是否已经是收到请求并执行了，此时，我们不能贸然重试请求，对于不是幂等的调用来说，这会是灾难性的。比如像转帐这样的业务逻辑，转一次和转多次结果是不一样的，如果重新的话有可能就会多转了一次。所以，这个时候，如果你的API遵从了HTTP动词的规范，那么你写起程序来就可以明白在哪些动词下可以重试，而在哪些动词下不能重试。如果你把所有的API都用POST来表达的话，就完全失控了。


除了幂等这样的控制逻辑之外，你可能还会有如下的这些控制逻辑的需求：


* **缓存**。通过CDN或是网关对API进行缓存，很显然，我们要在查询`GET` 操作上建议缓存。
* **流控**。你可以通过HTTP的动词进行更粒度的流控，比如：限制API的请用频率，在读操作上和写操作上应该是不一样的。
* **路由**。比如：写请求路由到写服务上，读请求路由到读服务上。
* **权限**。可以获得更细粒度的权限控制和审计。
* **监控**。因为不同的方法的API的性能都不一样，所以，可以区分做性能分析。
* **压测**。当你需要压力测试API时，如果没有动词的区分的话，我相信你的压力测试很难搞吧。
* ……等等


也许，你会说，我的业务太简单了，没有必要搞这么复杂。OK，没有问题，但**是我觉得你最差的情况下，也是需要做到“读写分离”的，就是说，至少要有两个动词，`GET` 表示是读操作，`POST`表示是写操作。**


#### Restful 复杂查询


一般来说，对于查询类的API，主要就是要完成四种操作：排序，过滤，搜索，分页。下面是一些相关的规范。参考于两个我觉得写的最好的Restful API的规范文档，[Microsoft REST API Guidelines](https://github.com/microsoft/api-guidelines/blob/vNext/Guidelines.md)，[Paypal API Design Guidelines](https://github.com/paypal/api-standards/blob/master/api-style-guide.md)。


* **排序**。对于结果集的排序，使用 `sort` 关键字，以及 `{field_name}|{asc|desc},{field_name}|{asc|desc}` 的相关语法。比如，某API需要返回公司的列表，并按照某些字段排序，如：`GET /admin/companies?sort=rank|asc` 或是 `GET /admin/companies?sort=rank|asc,zip_code|desc`
* **过滤**。对于结果集的过滤，使用 `filter` 关键字，以及 `{field_name} op{value}` 的语法。比如： `GET /companies?category=banking&location=china` 。但是，有些时候，我们需要更为灵活的表达式，我们就需要在URL上构造我们的表达式。这里需要定义六个比较操作：`=`，`<`，`>`，`<=`，`>=`，以及三个逻辑操作：`and`，`or`，`not`。（表达式中的一些特殊字符需要做一定的转义，比如：`>=` 转成 `ge`）于是，我们就会有如下的查询表达式：`GET /products?$filter=name eq 'Milk' and price lt 2.55` 查找所有的价柗小于2.55的牛奶。
* **搜索**。对于相关的搜索，使用 `search` 关键字，以及关键词。如：`GET /books/search?description=algorithm` 或是直接就是全文搜索 `GET /books/search?key=algorithm` 。
* **分页**。对于结果集进行分页处理，分页必需是一个默认行为，这样不会产生大量的返回数据。


	+ 使用`page`和`per_page`代表页码和每页数据量，比如：`GET /books?page=3&per_page=20`。
	+ **可选**。上面提到的`page`方式为使用相对位置来获取数据，可能会存在两个问题：性能（大数据量）与数据偏差（高频更新）。此时可以使用绝对位置来获取数据：事先记录下当前已获取数据里最后一条数据的`ID`、`时间`等信息，以此获取 “**该ID之前的数据**” 或 “**该时刻之前的数据**”。示例：`GET /news?max_id=23454345&per_page=20` 或 `GET /news?published_before=2011-01-01T00:00:00Z&per_page=20`。


**注意：这里需要注意一下，在理论上来说`GET`是可以带 body 的，但是很多程序的类库或是中间件并不支持 GET 带 body，导致你只能用 POST 来传递参数。这里的原则是：**


1. **对于简单的查询，很多参数都设计在 restful API 的路径上了，而 filter/sort/pagination 也不会带来很多的复杂，所以应该使用 `GET`**
2. **对于复杂的查询来说，可能会有很复杂的查询参数，比如：ElasticSearch 上的 `index/_search`里的 DSL，你也应该尽可能的使用 `GET`，而不是`POST` 除非客观条件上不支持`GET`。ElasticSearch 的[官方文档](https://www.elastic.co/guide/en/elasticsearch/guide/current/_empty_search.html)里也是这么说的。**



> The authors of Elasticsearch prefer using GET for a search request because they feel that it describes the action—​retrieving information—​better than the POST verb. （我们推荐使用 GET而不是 POST，因为语义更清楚）However, because GET with a request body is not universally supported, the search API also accepts POST requests （除非你的类库或是服务器不支持 GET带参数 ，你再用POST，我们两个都支持）
> 
> 
> **陈皓注：但是在 ElasticSearch 7.11 后，GET 也不支持 body 了。这是 ElasticSearch 的设计和实现不对应了。**
> 
> 






另外，对于一些更为复杂的操作，建议通过分别调用多个API的方式来完成，虽然这样会增加网络请求的次数，但是这样的可以让后端程序和数据耦合度更小，更容易成为微服务的架构。




最后，如果你想在Rest中使用像GraphQL那样的查询语言，你可以考虑一下类似 [OData](https://www.odata.org/) 的解决方案。OData 是 Open Data Protocol 的缩写，最初由 Microsoft 于 2007 年开发。它是一种开放协议，使您能够以简单和标准的方式创建和使用可查询和可互操作的 RESTful API。


#### 几个主要问题的回应


下面是对几个问题的直接回应，如果大家需要我回应更多的问题，可以在后面留言，我会把问题和我的回应添加到下面。


##### 1）为什么API 要Restful，并符合规范？


**Restful API算是一个HTTP的规范和标准了，你要说是最佳实践也好，总之，它是一个全世界对HTTP API的一个共识。在这个共识上，你可以无成本地享受很多的技术红利，比如：CDN，API网关，服务治理，监控……等等。这些都是可以让你大幅度降低研发成本，避免踩坑的原因。**


##### 2）为什么“过早优化”不适用于API设计？


因为API是一种契约，一旦被使用上，就很难再变更了，就算你发行新的版本的API，你还要驱动各种调用方升级他们的调用方式。所以，接口设计就像数据库模式设计一下，一旦设计好了，未来再变更就比较难了。所以，还是要好好设计。正如前面我给的几个文档——[Microsoft REST API Guidelines](https://github.com/microsoft/api-guidelines/blob/vNext/Guidelines.md)，[Paypal API Design Guidelines](https://github.com/paypal/api-standards/blob/master/api-style-guide.md) 或是 [Google API Design Guide](https://cloud.google.com/apis/design) 都是让你好好设计API的不错的 Guidelines.


##### 3）POST 更安全吗？


不会。


很多同学以为 `GET` 的请求数据在URL中，而 `POST` 的则不是，所以以为 `POST` 更安全。不是这样的，整个请求的HTTP URL PATH会全部封装在HTTP的协议头中。只要是HTTPS，就是安全的。当然，有些网关如nginx会把URL打到日志中，或是会放在浏览器的历史记录中，所以有人会说 `GET` 请求不安全，但是，`POST` 也没有好到哪里去，在 [CSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery) 这个最常见的安全问题上，则完全就是针对 `POST` 的。  安全是一件很复杂的事，无论你用哪方法或动词都会不能代表你会更安全。


另外，


* 如果你要 防止你的 `GET` 上有敏感信息，应该加个密，这个跟 `POST`是一样的。
* 如果你要防止 `GET` 会被中间人修改，你应该做一个URL签名。（通常来说， 我们都在 `GET` 上做签名，`POST` 就忘做了）
* 如果你要防止有人发一些恶意链接来 hack 你的用户（传说中的 `GET` 不如 `POST` 安全的一个问题），你应该用 HMAC 之类的认证技术做好认证（参看 [HTTP API 认证授权术](https://coolshell.cn/articles/19395.html "HTTP API 认证授权术")）。


总之，你要明白，`GET` 和 `POST` 的安全问题都一样的，不要有谁比谁更安全，然后你就可以掉以轻心的这样的想法，安全都是要很严肃对待的。


##### 4）全用 POST 可以节省时间减少沟通吗？


不但不会，反而更糟糕。


说这种话的人，我感觉是不会思考问题。


* 其一，为API赋于不同的动词，这个几乎不需要时间。把CRUD写在不同的函数下也是一种很好的编程风格。另外现在几乎所有的开发框架都支持很快速的CRUD的开发，比如Spring Boot，写数据库的CRUD基本上就不需要写SQL语言相关的查询代码，非常之方便。
* 其二，使用规范的方式，可以节约新加入团队人员的学习成本，而且可以大大减少跨团队的沟能成本。规范和标准其实就是在节约团队时间提升整体效率的，这个我们整个人类进行协作的基础。所以，这个世界上有很多的标准，你只要照着这个标准来，你的所生产的零件就可以适配到其它厂商的产品上。而不需要相互沟通。
* 其三，全用POST接口一把梭，不规范不标准，使用你的这个山寨API的人就得来不断的问你，反而增加了沟通。另外，也许你开发业务功能很快了，但是你在做控制逻辑的时候，你就要返工了，从长期上来讲，你的欠下了技术债，这个债反而导致了更大的成本。


##### 5）早点回家的正确姿势


不要以为你回家早就没事了，如果你的代码有这样那样的问题，别人看懂，或是出误用了你的代码出了问题，那么，你早回家有什么意义呢？你一样要被打扰，甚至被叫到公司来处理问题。所以，你应该做的是为了“长期的早回家”，而不是“短期的早回家”，要像长期的早回家，通常来说是这样的：


* **把代码组织设计好，有更好的扩展性**。这样在面对新需求的时候，你就可以做到少改代码，甚至不改代码。这样你才可能早回家。不然，每次需求一来，你得重新写，你怎么可能早回家？
* **你的代码质量是不错的，有不错的文档和注释**。所以，别人不会老有问题来找你，或是你下班后，叫你来处理问题。甚至任何人都可以很容易地接手你的代码，这样你才可能真正不被打扰


##### 6）工作而已，优雅不能当饭吃


回应两点：


其一，遵循个规范而已，把“正常”叫“优雅”，可见标准有多低。这么低的标准也只能“为了吃饭而生存了”。


其二，**作为一个“职业程序员”，要学会热爱和尊重自己的职业，热爱自己职业最重要的就是不要让外行人看扁这个职业，自己都不尊重这个职业，你让别人怎么尊重？尊重自己的职业，不仅仅只是能够获得让人羡慕的报酬，而更是要让自己的这个职业的更有含金量**。


**希望大家都能尊重自己从事的这个职业，成为真正的职业化的程序员，而不是一个码农！**


![](https://coolshell.cn/wp-content/uploads/2022/02/quote-your-job-gives-you-authority-your-behavior-gives-you-respect-irwin-federman-73-55-75.jpeg)你的工作给你权力，而只有你的行为才会给你尊重
（全文完）



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![聊聊团队协同和协同工具](https://coolshell.cn/wp-content/uploads/2022/10/communication-150x150.png)](https://coolshell.cn/articles/22298.html)[聊聊团队协同和协同工具](https://coolshell.cn/articles/22298.html)
* [![谈谈公司对员工的监控](https://coolshell.cn/wp-content/uploads/2022/02/monitoring-150x150.jpeg)](https://coolshell.cn/articles/22157.html)[谈谈公司对员工的监控](https://coolshell.cn/articles/22157.html)
* [![如何做一个有质量的技术分享](https://coolshell.cn/wp-content/uploads/2021/07/knowledge_sharing-300x169-1-150x150.jpeg)](https://coolshell.cn/articles/21589.html)[如何做一个有质量的技术分享](https://coolshell.cn/articles/21589.html)
* [![程序员如何把控自己的职业](https://coolshell.cn/wp-content/uploads/2020/08/programmer.01-e1596792460687-150x150.png)](https://coolshell.cn/articles/20977.html)[程序员如何把控自己的职业](https://coolshell.cn/articles/20977.html)
* [![MegaEase的远程工作文化](https://coolshell.cn/wp-content/uploads/2020/01/remote-150x150.jpg)](https://coolshell.cn/articles/20765.html)[MegaEase的远程工作文化](https://coolshell.cn/articles/20765.html)
* [![别让自己“墙”了自己](https://coolshell.cn/wp-content/uploads/2019/12/open-your-creative-mind-150x150.jpg)](https://coolshell.cn/articles/20276.html)[别让自己“墙”了自己](https://coolshell.cn/articles/20276.html)
The post [“一把梭：REST API 全用 POST”](https://coolshell.cn/articles/22173.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).