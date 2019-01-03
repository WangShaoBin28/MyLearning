这是底线学习的最后一部分，内容稍微开始有点料了

开篇是告诉读者他的主体范围，乍看起来和前一章差不多啊，所以她说是 more detail；然后往回找补说这里也有点小秘籍（best practices），虽然并非必须，但是会让你更爽云云...

# 13. Build Systems

上来就又是这个，估计很多想看代码的同学会立即失望，但构建系统的依赖管理功能，是构成Spring Boot便捷性的一块基石，她绕不过去，只能说一下，注意Starters是合在这个章节的，所以说明Starter本身就是依赖管理（依赖传递），确实没有更多的内容了

重点看一下maven这一节，毕竟仅剩的xml在这

## 13.2 Maven

这里重点重申了使用和不使用Parent引入spring boot时候得到的效果上的区别

如果是继承的，她认为会获得很多有价值的东西（obtain sensible defaults）：

+ 1.8 编译级别
+ UTF-8 的源文件编码

这确实不继承我自己也得这么写，还不能算是它很opinionated

+ 包含一个依赖管理版本清单

说起来这里面就会开始有一点微妙了，值得假设Spring团队对兼容性的经验比较强一点

+ 合理的资源文件占位符管理（特别是Spring Boot自身的一些配置文件）
+ 合理的插件配置

合不合理的，他有他的原因，比如这里有解释，因为spring自身使用${}占位符，所以maven的resource filtering部分它换成了@@（并且说明了如果不喜欢这个的话，用哪个property来修改）

插件配置是很重要的一点，这是用不用parent节点引入spring-boot的一个最主要影响

接着给出了一种如果想覆盖缺省的版本声明的推荐方法——使用properties，并且告诉我们properties中和版本相关的属性名要去[这里](https://github.com/spring-projects/spring-boot/tree/v2.0.4.RELEASE/spring-boot-project/spring-boot-dependencies/pom.xml)去看

反复重申使用它们推荐的version，愉快的省略，省的自己在这方面找麻烦，这里提到有这么两个主要的麻烦：

+ 没法用properties来覆盖缺省版本，因为它import进来的是另一个东西，而不是parent里面的那个，所以它压根就没有properties去复写
+ 非要想复写，还需要在dependencyManagment里面把想复写的BOM放置在spring-boot-dependencies之前
  - 这个应该是对物料清单类型的引入的限制，如果是直接依赖项应该没这个限制

总之就是又得额外付出不少敲击或者copy&paste成本

### 13.2.3 Using the Spring Boot Maven Plugin

这一节没有什么新东西，主要强调老老实实用它缺省的配置就行了

**总之 13.2 这一节就是苦口婆心的劝说还是用它做parent就完了**

## 13.5 Starters

这一节首先声明自己一点都不神秘，但是特别的好用（他整篇文档都有广告的嫌疑）；好在她用词比较切中要害，比如这么做就是为了避免sample code and copy-paste，这也是为什么值得用Spring Boot而不是自己再在这个方面再去花心思搭什么脚手架的原因：他在中央仓库，是一个广泛的被采用的第三方库，假设自己也用类似的方式来实现它的效果——首先想想自己是它这种思路吗？应该首先是copy-paste吧，就算是库，很有可能变成一个二方库，从可靠性和可维护性上，是否相对Spring Boot 的Starter有优势呢？重复造轮子其实没什么不可以（要和重复发明轮子区分开，事实上Spring Boot就是在这里造了一个更好的轮子），关键是得真造的比别人的好

接下来给出一个命名规则，主要是为了自己想动手实现自己starter的同学准备的

再往下是一个Spring Boot项目维护的starter列表，所以[这个链接](https://docs.spring.io/spring-boot/docs/2.0.4.RELEASE/reference/htmlsingle/#using-boot-starter)，也应该是案头备查

最后还有一个tip，里面指向了Spring Boot 代码仓库中文件，里面维护了一个[列表](https://github.com/spring-projects/spring-boot/blob/master/spring-boot-project/spring-boot-starters/README.adoc)，是一些社区项目自己维护的starter，如果要使用这些库，可以选用这些starter，但由于和Spring Boot工程是分离的，Spring Boot Reference中没有讨论相关的版本问题，所以需要自己考察一下版本兼容性问题

# 14. Structuring Your Code

总领一句就是，确实是废话，但是还是得说的意思

## 14.1 Using the “default” Package

乍一看标题，吓一大跳，就这样还叫Best Practices，牌子大也不能这样，所以说起名得多种要，看正文明明就是Avoid Using么，估计是作者怕读者看睡着了，故意这么写吧，这一节貌似可以补充到java code style guide里面，原来通常避免是因为有一些其他的问题，比如JNI时候default包好像会有点问题，Spring这个理由更充分了

## 14.2 Locating the Main Application Class

如果说Spring Boot真有什么约束，这是一个，把启动类放在顶层包里面，用于隐式的声明要对哪些包做扫描；Tip里面的意思就是如果Developer就是不这么干，也是可以的，这时候就不能仅用@SpringBootApplication注解了，这样才能自己声明扫描的包的范围

下面是示例，说的很清楚

# 15. Configuration Classes

15 节导语主要强调了Spring Boot提倡的风格就是基于Java的配置类，而不是XML（尽管有这个能力），并且建议main方法的那个类当作一个@Configuration的主类（很有些卖关子的感觉）

@Configuration注解引入，没记错应该至少Spring 3就有了，当时选了它应该是STS的插件在xml撰写时候提示能力不足（或者干脆有的同学就不用插件），它原始的设计目的记不太清了，但是确实是Spring 4之后各种条件化的注解，进一步的释放了Java-Based Configuration的能力

再到Spring Boot里，后面到Auto-Configuration进来之后还可以这样个玩儿法，应该完全超出绝大多数人的想象了

## 15.1 Importing Additional Configuration Classes

提示说@Configuration可以不止写在一处，用@Import或者@ComponentScan可以用来组合起来，这个技巧或者说规则还是很重要的，特别是考虑用@ComponentScan，可以进一步的消除配置的集中化，避免形成另一个层面的依赖查找，目的是避免集中在同一个文件引发的代码冲突

> 这里插一个问题，后面再看是不是有更合适的地方讨论，就是当分散了配置时候，实际上缺少了一份单一的可参考的配置文档（Rod Johnson当年可还是委婉的将一份单一的xml文档当成一个优势来阐述的，当然他面对的场景是DI还非主流，EJB充其量有个依赖查找时候的Java世界），去掉这份聚合文档的好处在于几乎已经把唯一一个会在代码库提交时候产生冲突的点去掉了，除此之外当需要聚合浏览的时候，可以利用@Configuration注解来做搜索，是grep还是IDE就凭习惯了

## 15.2 Importing XML Configuration

这里也是讲的Spring的特性，提一下也是为了表明，这些经验依旧适用

# 16. Auto-configuration

终于来正格的了

导语国文翻译吧

> Spring Boot 自动装配功能（auto-configuration）试图根据依赖的jar包来完成Spring应用的自动配置；例如，如果classpath中包含HSQLDB，并且没有手动配置任何的数据库连接Bean，那么Spring Boot会自动配置（auto-configures）一个in-memory类型的数据库实例
>
> 需要通过在一个@Configuration注解过的类上添加@EnableAutoConfiguration或者@SpringBootApplication注解来开启自动装配功能（auto-configuration）
>
> Tip 只应该添加 @SpringBootApplication 或 @EnableAutoConfiguration 其中的一个，通常建议只加在最主要的那个@Configuration类上面

这里描述了几层意思：

+ Spring Boot 自动配置功能是干什么的（也基本上描述了他怎么做的）：
  - 它根据classpath里面的依赖和具体应用的配置情况来决定是否提供一个缺省配置
  - 换句话说如果应用自己配置了一个，那它就不会提供缺省配置了
+ Spring Boot 可以通过@EnableAutoConfiguration开启
+ Spring Boot 可以通过@SpringBootApplication 开启
+ @EnableAutoConfiguration 和 @SpringBootApplication 不要同时出现
+ 只出现一次也就够了，并且仅在最顶级的@Configuration注解修饰的类上出现就够了

## 16.1 Gradually Replacing Auto-configuration

讲述如何替换掉Auto-Configuration的行为：当出现了自定义的配置的时候，Auto-Configuration的行为就自然被替换掉了，这在前面导语里面也提到了，这里举了个例子，如果显式的配置了一个DataSource Bean，那缺省的嵌入式数据库将不被启用；从他这个描述来看，至少自动配置功能是会识别bean的名字的

如果想了解当前应用了哪些自动配置，并且为什么他们被启用了，那么可以通过在启动时增加一个--debug的开关；然后就能在控制台日志里面看到了（应当是仅在控制台日志中打印了，否则为什么说的这么绕？）

## 16.2 Disabling Specific Auto-configuration Classes

如题，讲述如何禁用特定的自动配置类，通过注解@EnableAutoConfiguration来排除，例子写的很清楚

然后又是Spring一项惯用的花活，一个事儿往往好几个方法来做：

+ 排除的时候可以直接排除类，也可以用全限定的名字来排除
+ 还可以通过属性值的配置来完成（那就意味着可以通过命令行参数来完成了？待验证）

# 17. Spring Beans and Dependency Injection

_to be continue..._





