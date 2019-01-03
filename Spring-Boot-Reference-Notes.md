# 概述

如题，其实是Spring 官方参考文档的阅读笔记

# 如果心太急

Spring Boot Reference 有一个[章节](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/reference/htmlsingle/#getting-started-whats-next)为被她称作impatient的同学指明了方向，但是她明显假设了读者已进入了那一小节，这段就是为了弥补她假设不成立时候这个漏洞而存在的

无论如何，还是应该把[文档第一部分](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/reference/htmlsingle/#boot-documentation-first-steps)读完

# 参考链接

貌似这个章节有点多余，既然是官方文档，直接去官网上看好了，但考虑到Spring Boot作为一个成熟开源项目，其自身稳步迭代的能力，该文档的版本问题不应该被回避

这里是想以2.0.4.RELEASE为基础来进行学习，希望能在2.1.x.RELEASE之前，将文档通读完成，目前看[Spring Boot的发版计划](https://github.com/spring-projects/spring-boot/milestones) 2.1版本第二个里程碑是8.21，然后就是RC1版在9.21，~~放弃一些不必要的细节是应该能做得到的~~ （2018.9.13 事实证明一个月不努力还是很难做到的，[2.0.5 已发](https://github.com/spring-projects/spring-boot/releases/tag/v2.0.5.RELEASE)）

## 根目录

2.0.4版本的文档在[这里](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/)，如截图：

![https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/](https://github.com/leizhnxp/learning/blob/master/images/spring-boot-doc.PNG)

分了几个部分

+ [actuator-api](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/actuator-api/)
  - 这是一篇HTTP API的文档，说明Spring Actuator 细节功能的，Actuator的概要部分这里没有涉及，还得看[ref](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/reference/htmlsingle/#production-ready)
  - actuator 就是 Spring Boot 宣传中所谓的 production-grade 部分的重要构成
+ [api](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/api/)
  - 这组文档和上面那个api形式不一样，这个是javadoc形式的，Spring Boot主体功能实现的api接口说明
  - 比如Spring Boot世界万物的起始 [SpringBootApplication注解](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/api/org/springframework/boot/autoconfigure/SpringBootApplication.html)
  - 再比如starter中激活了的用于自动装配的类（实际上就是那些Java-Based Configuration，例如被很多人心爱的[redis](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/api/org/springframework/boot/autoconfigure/data/redis/package-frame.html)访问的配置相关）
  - 当然了他这个都是基于源码中的JavaDoc生成的，也许看源码更方便；但实际上意义也在于此，维护文档和代码的一致性的意义（对[源码即是设计](https://blog.csdn.net/hoping/article/details/16902)这种[观点](https://www.developerdotstar.com/mag/articles/reeves_design.html)<sup><a id="a1">[1](#fn1)</a></sup>的一种肯定和实践）和手段（其实就在身边，古老但实用）
+ [gradle-plugin](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/gradle-plugin/reference/html/)，顾名思义，如果不是想为Spring的某些项目贡献力量或者有旺盛的兴趣，这个可以放放
+ [maven-plugin](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/maven-plugin/)，顾名思义
  - 这和上面的gradle-plugin部分一起对构成Spring Boot体系的另外一方面给出了详细的使用级别的说明，
  - 有一点有意思的是，这两个plugin的文档样式风格迥然不同（他们和JavaDoc，以及Spring自身的Reference文档风格也都不同），组织形式也不同，明显他们这都是继承自各自社区的风格
+ [reference](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/reference/)，这是正格的参考文档，本文重点的关注对象

## 其他交叉参考

也是官网文档链接

+ [源码tag](https://github.com/spring-projects/spring-boot/tree/v2.0.4.RELEASE) -  看不看的，得确定它在哪儿，记得对应2.0.4的tag来看文档
+ [properties list](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/reference/html/common-application-properties.html) - 这是一份重要的参数列表参考，案头备查
+ 官网主页的三个页签 - 这三个页签其实非常有料，不仅导向了本文的主角，其他资源都认真浏览过一遍（如果能做到的话），保守估计能超越全球60%的开发者吧，在天朝能超越70%（主要是胜过那些不看英文的）
  - [overview](https://spring.io/projects/spring-boot#overview)
    * 上面都是宣传语，但是如果背下来基本上面试的忽悠环节也就过了
    * 几个video视频很可以看下，大多是youtue上的，所以有机翻字幕，Spring Boot 基础概念（其实是Spring）和2.0的最重要新特性一网打尽
    * Spring Boot社区的Gitter.IM地址 <sup><a id="a1">[1](#fn1)</a></sup>，曾经有种IRC里练口语的，听说过没这么干过
    * Spring Boot Initializer的web版入口，有的人爱它，有人觉得它真无用
  - [learn](https://spring.io/projects/spring-boot#learn)
    * 几个在册版本的reference link，当他强调这里讲述的东西有多个版本
    * 最重要的是它给出了一个guide的地址，为什么选这个？因为着就是一个pivotal帮写的关于spring boot的hello world
    > 真的简单是吧，简单到都懒得去做了是吧，那想办法背着他实现一遍，然后改动成pathvariable形式的参数（同时应当想一下原参数放这里合不合理？），再改造成按用户分别记录访问数，然后需要做的是仔细体会，究竟框架帮助解决的是哪方面的问题？解决业务问题，靠的最后又是什么能力？<sup><a id="a2">[2](#fn2)</a></sup>
  - [samples](https://spring.io/projects/spring-boot#samples)，这是正格的参考，两个工程，都非常有意思
    * 上面提到的Spring Boot Initializer的repo，一个平台化的产品，在多大程度上能够自举是很重要的，她确实完成了基本该做的，如果说她真有缺陷（不生成多模块项目；不能增量管理denpendency...是不是太苛责了？），真的不是Spring Boot的缺陷，只是作为Initializer的缺陷
    * 这个说明点问题，整个Spring网站，是在Spring Boot基础上构建的，但是由于它用的gradle来做的build，作为不熟悉gradle的同学，暂时不去探究这个东西或许明智

# 从目录结构来观察该文档

要说github的web site上 markdown显示没有给自动生成概览的折叠ToC认了，毕竟它能定制，Spring的Reference在这么长的情况下HTML版没有个可以折叠的catalog实在是不像话，他可能是满足于它 Part I 内容的编排吧

好在他有pdf，有epub，那找一个有折叠目录能力的reader就可以了（chrome browser就可以）

![目录](https://github.com/leizhnxp/learning/blob/master/images/spring-boot-ToC-outline.PNG)

如图，它十个大段落

为了避免这个文档在解释Spring Boot Reference结构时变成跟他的ToC一样很难概览，因此分段落介绍拆成独立的wiki页来说明，分段落导读则需移步

+ [Part I. Spring Boot Documentation](Spring-Boot-Reference-Notes---Part-I)
+ [Part II. Getting Started](Spring-Boot-Reference-Notes-Part-II)
+ [Part III. Using Spring Boot](Spring-Boot-Reference-Notes-Part-III)
+ Part IV. Spring Boot features
+ Part V. Spring Boot Actuator:Production-ready features
+ Part VI. Deploying Spring Boot Applications
+ Part VII. Spring Boot CLI
+ Part VIII. Build tool plugins
+ Part IX. ‘How-to’ guides
+ Part X. Appendices

这里给出一组简要的指引结论：

+ Part I II III 一定要看**完**
+ 特别是Part I 和 Part II 的 12. What to Read Next，明确搞清楚自己需要的是什么

其实有这两点就够了，但考虑到这份文档写作动机并非单纯为了自己，因此还需要补充一些废话

+ 收藏Part IX链接，熟悉 Part IX 的结构，了解大概这里都涉及到了哪些主题，然后还是搞清楚自己想要什么，最后直达目的
+ 收藏Part X Appdendix A的链接，待查阅
+ 如果想玩儿转 Spring Boot，Part IV V 不能回避
+ 对于Part VI，根据爱好和需要看就可以了，如果需要和国际接轨或者用比较传统的服务方式来跑程序的，值得看
+ 如果是一个命令行爱好者，可以看下Part VII
  但最好只有限的使用几个command，比如init，它作为一种辅助原型设计的工具可能还好，但多少需要对groovy有些了解，否则很难发挥出它的能力；另外它不具备REPL能力，如果开发过程有这个需要的，老老实实装个JDK 9+的环境（推荐用SDKman，这样切换比较容易）
+ 剩下的应该只有 Part VIII 和 Part X 其他的Appdendix没有提到，可以看看Part VIII 68.2，描述了可以执行的war包，具体想看什么，其实还是看自己的意向

# 脚注

1. <a id="fn1"> 恕孤陋寡闻，gitter好像天朝没有山寨的，估计是开发社区根源上的文化的原因，这里都是为了生计，人家真是为了乐趣，所以洋人有slack，广大群众就用钉钉；他们用gitter，如果也想用，那就也用gitter吧，正好和国际接轨了 </a> [↩](#a1)
2. <a id="fn2"> 这个问题好像有一本参考书，叫『笑傲江湖』 </a> [↩](#a2)
3. <a id="fn3"> [Jack W. Reeves 的警世恒言](http://user.it.uu.se/~carle/softcraft/notes/Reeve_SourceCodeIsTheDesign.pdf)</a> [↩](#a3)