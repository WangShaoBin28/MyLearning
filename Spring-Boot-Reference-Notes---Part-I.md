这个Part就是个索引，用来基于不同的目的快速导引到特定章节

这个Part分为 标号 1 到 7 总共7个小节（全书小节的编号是统一连续的）

# 1. About the Documentation

告诉大家它这份文档有不同的格式，并且从哪里找最新版，然后一堆版权信息，自由分发，不犯法的

# 2. Getting Help

+ 提示了一种这个文档的用法，这个文档有一个Part IX，是专门用来答疑的
+ 提醒读者Spring Boot的基础是Spring，要理解Spring的基础上来理解Spring Boot的运作，并且给出了一份[清单](https://spring.io/guides)
  
  这个清单应该是很多人喜欢的，就是手把手的写一些样例，有前辈告诉大家说，不管例子多简单，认真照着敲一遍做一遍总会有收获，这种建议背后的含义应该是让人静下心来做事情，不要一味图快，有些人囫囵吞枣的把很多东西堆出来，未必真的明白自己在做什么，用心做事的人看似笨拙，但长远看气力悠长，龟兔赛跑讲的也是这个道理吧

+ 告诉大家stackoverflow是个好地方，加上spring-boot标签的问题他们（pivotal？）会有人盯着看的
+ 主动的给Spring-Boot报bug，不用客气

最后提示大家，任何人都可以为她贡献一份力量

# 3. First Steps

为初入山门的同学提供了一份阅读指引：直接进入Part II！

同时对 Part II 进行了catalog之外的一种逻辑划分：

+ 准备工作（原文叫 from scratch，从零开始，从抓狂开始？）：8、9、10小节
+ 入门教程：第11小节，以11.3为界分为两部分
  - 前半部分是脚手架（合着人也没一开始就Spring Boot Initializer啊）
  - 后半部分开始写点能出东西的代码
+ 具体run起来：
  - run着玩玩儿
  - 正儿八经的build之后run

从Part II 开始，每个Part的最后一个小节都是 What to Read Next，这本身进一步的表明了章节之间的逻辑顺序

Part II 的 [12. What to Read Next](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/reference/htmlsingle/#getting-started-whats-next) 是一个重要的分野，值得单独拎出来看一下，特别是他里面提到的task-oriented type of developer，扪心自问一下自己是不是这样的人，然后考虑是否遵从这个chapter的指引

# 4. Working with Spring Boot

看名字就说明比前面的要严肃一点了，更深入到讨论一些主题

要进入工程的状态，可以从这个视角来进行切入，具体对应的内容是Part III

这节是对Part III进行了catalog之外的一种[逻辑划分](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/reference/htmlsingle/#_working_with_spring_boot)

进入工程状态，除了要涉及

+ 构建系统（这里主要是指的依赖管理主题，Spring Boot 给出的答案是Starter）
+ 考虑最佳形式（一些工程代码结构的约定，确实没什么必要在一些事情上过度发挥）
+ 调试技巧
+ 面向生产的打包（正文内容指明了这里涉及Part V），这是一个相对独立的方面，但是工程化视角不能忽视的环节

还有一个有人爱有人不爱的工具也加入了这个逻辑视角，那就是Spring Boot CLI

# 5. Learning about Spring Boot Features

Part III 比 Part II 要介绍的深入，但是视角还是 how you should use 

所以这个段落试图告诉大家说，但如果想玩转整个Spring Boot的运作机制，则需要进入Part IV

具体这个摘要段落的逻辑分组直接看原文就好了

# 6. Moving to Production

开发完成之后，服务上线，也就是传统的运维阶段还是有很多问题需要解决，Spring Boot Actuator 就是在这方面给出的答案，严格的说起来，Spring Boot就是一个两面怪，一个是所谓的opinionated的一组views和practices，另一个就是所谓的production-ready，后者这个努力非常有价值，这类非功能性需求很少被业务向的产品研发团队涉及，大一点的组织会有专门的运维开发团队来处理，但是往往都是和应用研发脱节的，分成对立的组织结构来各自维护各自的产品，Spring Boot Actuator 一方面为中小团队减少了这方面的开发量并提供开箱即用的一揽子解决方案，更主要的是从框架工具层面提醒产品开发团队要重视起这个问题（就像Spring 框架最大的价值不仅仅是简化了java开发，更重要的是它的基本理念在辅助开发人员强化设计，所以Spring Boot就是Spring Framework一脉相承的结晶）

总而言之，这个视角非常重要，应该认真阅读的一个章节

# 7. Advanced Topics

实际上是other，相比较起来，没其他的视角主题那么大，但针对特定的目的有其独特的参考价值，通读完其他章节后再来阅读会比较好一点，除了 Appendix A. Common application properties，这个属于案头必查

下面就该进入真正的阅读之旅了
