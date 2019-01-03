这个章节阅读起来还是比较轻松的，本身篇幅也比较短，如导读章节所说，就是一个必要的准备的介绍，和一个简要的感性认识

# 8. Introducing Spring Boot 就是个广告

除了广告词，还是要相信Spring Boot产品团队是板起脸来给出了他们的的设（广）计（告）目（宣）标（传），简要国文演绎如下（含注释）：

+ 让使用Spring的开发过程更容易起步（要不怎么叫boot呢，不用initializer的情况下，也只需要copy & paste少量内容）
+ 精心组合的开箱即用特性（boot的自动装配能力），且具备定制灵活度（毕竟根基上是Spring Framework的装配能力）
+ 提供大量的喜闻乐见的非功能性特性，如balabalaba，它里面提到真的是那么回事的是测量（指标），健康检查，外化配置这三点，诸如嵌入式容器这点其实容器厂牌自身已经做得很不错了
+ 这回真的没有xml配置了（看样子之前java-based configuration推广十分不力，按说早就该没了啊），而且不是代码生成方案哦（这一点要言传确实balabala要说一堆，这么理解吧，它的解决方案就是一个第三方依赖库，而不会额外让使用者产生第二方依赖管理的困扰，觉得没说人话也没关系，毕竟这个问题对Spring Boot本身的学习来说没什么影响）

# 9. System Requirements 可以略过

也就是最后一句确实可以提下，即spring boot也可以打war包的，而且这个war包还是个可执行的war包！对于maven的构建方式，仅仅需要声明构件类型为war即可

# 10. Installing Spring Boot CLI - coding前的准备工作

## 10.1 

扯的是maven和gradle的安装，给出的例子：如果是一个web应用，那么最简的脚手架的pom或build.gradle文件部分要如何撰写；这里还第一次明确引入了Spring Boot中很重要的Starter这个东西

这里面主要是提到了这么一个重要的东西：**以maven为例，究竟一个Spring Boot的maven工程的pom有什么与众不同**？

+ 标志内容之一：通过parent或者dependencyManagement引入Spring Boot的BOM（而不是自家私造的）
+ 标志内容之二：denpendency中按需声明的starters（而不用事必躬亲乱写一通）
+ 标志内容之三：build.plugins部分声明plugin，spring boot maven plugin（其实不写也行...）

关于BOM清单部分，这个省了很多不必要的版本约定部分，扪心自问，以前是不是拍脑袋居多？当然证明Spring Boot没有拍脑袋也有点难

> 以前需要手动生成项目脚手架，统一依赖的版本是主要目的之一，现在在Spring Boot这里得到了极大的解放，解放了所有人实际上
> 
> 除了依赖库版本管理，过去的所谓脚手架，大都是一个样板化boilerplate的代码、甚至目录和配置文件，管理的不好（如果不产品化，实际上也很难管理好）就会形成一个臃肿的存在，大量的冗余和重复，拷贝粘贴，干扰真正的目的；maven给出了解决方案是 archetype:generate，只是自身内部没有一个真正的规则，整体推广效果相当差，受众接受度也不高，但是实际上形成了一个产品的雏形；Spring Boot如同Spring一直做的那样，立足于现状，改变了现状，所以确实是一个值得尊重的产品，Spring Boot Initializer在这个方面就这么成了一个maven archetype的更成熟的替代品

关于starters，这是最没技术含量的部分之一（但并非不重要，或者说它展示了依赖传递的一种best practice），当然Spring Boot 基础注解和Auto-configuration的jar包也是借道这里引入的（所有的starter按图索骥都会追溯到它，然后就是maven那套规则来做依赖传递时的相同jar包甄选和排除）

关于 plugin 部分，有一点点需要注意的，如果用的parent形式，就比较方便了，因为parent属于无脑继承，但是文档中偏偏提到了用dependencyManagment引入spring boot（组合），这时的plugin部分是需要额外配置的，这块儿内容在11.5节有提到，并给出了链接（就是maven-plugin那份文档），文档这里只提到无法单独对PluginManagment进行import设置，所以要打可执行jar包，为了减少配置，还是直接parent spring boot就可以了

## 10.2 

Spring 当年好像押宝过groovy，所以Spring Boot CLI这个东西无责任推测一下，很有可能在他们内部是个怪胎（也不排除人家是喜欢抛弃式原型的），不仅这里有一节，后面还有单独一个Part来讲他的，抛开其实用性如何不谈，10.2节的意义更多在于：

+ 知道有这么个工具，他除了吹嘘的那一大堆可能也用不到功能，把他当封装好的Spring Initializer命令行版也行（不必操控curl去捅start.spring.io），如果真的还想要自己的脚手架（可能有这个需要，但真的有这个必要么？这是在越界约定优于配置的信仰），这可以考虑作为基础工具之一（其实也可能curl更好，因为curl几乎是所有*nix发行版预置）
+ 额外福利，秀了一下全平台各种的包管理器...不知Spring的文档里面把choco scoop homebrew macport 都覆盖了是几个意思，感觉和Spring Boot的目的都不太搭界...不过话说回来了，当初知道这两个东西，包括sdkman，不会就是拜这份文档所赐吧（记忆确实模糊了）...

## 10.3

这一节应该很重要，他说的是从1.x.x上升级吧，如果没这个需要倒是可以不看

# 11. Developing Your First Spring Boot Application - 终于到了本该最欢乐结果却是本篇最无趣的环节了！

老实说真不如官网[learn签页](https://spring.io/projects/spring-boot#learn)里面[那个](https://spring.io/guides/gs/rest-service/)

应该说确实是关注点不一样吧

这一节如很多人所愿手把手讲了一个hello world，但是概念上也触及到很多比较根本的东西，比如人家明明白白得讲了，哪些是Spring的，哪些是Boot的，哪些是maven或gradle提供的

11.3.2 节有一段框文字强调了starter和auto-configuration之间的关系，提到了二者实际上不是绑定的，大概的意思是说，starter是来做依赖传递用的，而auto-configuration是在SpringBoot引导加载时来进行判断的，也就是说，如果没有引用任何的starter，可以通过引用boot-autoconfiguration的包来完成自动装配（boot和boot-autoconfiguration是两个包，是否都要引用，真的没有试过，这里文档强调的是概念，但是如果不理解，最好自己动手试一下）

除此之外，这个流程里面有一个小小的细节，流程中一笔带过，虽然文档给出了解释，但是并不充分，用（无）心（聊）的同学也许能发现：

11.4节运行```mvn spring-boot:run```的时候并没有在 pom 里面声明 spring boot maven 插件，而是在11.5节的时候要求加入plugin这段配置，然后要求执行```mvn clean package```

那凭什么不声明的时候可以 mvn spring-boot:run，而声明了之后要执行mvn clean package呢？如果这个问题不觉得奇怪，那么应该试试看，如果不补充11.5节那段plugin声明，如何完成打出spring boot风格的可执行jar包（这本质上只是一个maven的问题，所以这份Ref文档没有细说是可以理解的，但是他偏偏这么行文下来，是否有用意呢？估计想多了）

如果能做到这点，相信对最简单的Part II这章的学习在理解层面会有进一步的深化：maven和Spring Boot的关系，或者说Spring Boot如何利用maven能力这个方面

除此之外，还可以考虑玩儿这么一个游戏（生产时候完全没必要这么干，所以真的只是一个游戏，主要是这个示例太简单了，不会消耗太多的打字时间），不配置starter，来启动并完成这章的示例，来印证一下文档中提到的starter和自动装配不绑定的解释


