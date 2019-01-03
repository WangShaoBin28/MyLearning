Spring Cloud 官方文档开篇除了基本概念，第一个是Spring Cloud Config，这多少令天朝贱民有些惊讶，毕竟这里的各家财主有着诸如diamond，disconf，appollo这般百花齐放的景象，也难怪不鸟Spring Cloud这个看起来如此简陋（没有界面？还是用git？）的玩意儿

但这应该并非能说明Spring Cloud就弱到不能用，待考察过Spring Cloud Config官方文档介绍的功能后，再形成自己的判断应该也不迟

pivotal的工程师上来就讲他，因为这是所谓外化配置的一个具体实践，应用服务将持久化数据和配置都与程序分离了，自然就一点状态都没有了，可以随意地起停，增删，做水平扩容——这么说也许有点武断，毕竟有本地缓存还需要维护

和Finchey.SR1 版相匹配的（Spring Cloud Release train）Config版本是2.0.1，文档在[此](http://cloud.spring.io/spring-cloud-static/spring-cloud-config/2.0.1.RELEASE/single/spring-cloud-config.html)

总共7个章节，

1. Quick Start
2. Spring Cloud Config Server
3. Serving Alternative Formats
4. Serving Plain Text
5. Embedding the Config Server
6. Push Notifications and Spring Cloud Bus
7. Spring Cloud Config Client

比重极不均衡，3456都很短，也可以理解，主要是介绍服务端（2）和客户端（7）

# 1. Quick Start

按说先2后7的思路是很正常的，但是Quick Start部分实在有点不知所云，莫非没有人问一下这东西到底怎么回事？哪里就来一个spring-cloud-config-server去让我cd呢？看起来还是个spring boot的，而且告诉我们主类叫configServerApplication，这有鼻子有眼的，但是东西到底在哪儿呢？

所以说这份文档真是骨骼清奇，Spring Boot文档内容充实结构良好的印象在这里一概不见，也算让我刮目相看了

经过多方对比，锁定这个spring-cloud-config-server应当是指官方给出的[sample 工程](https://github.com/spring-cloud-samples/configserver)，其实也没什么理由，就是觉得这个最像，考虑到这里我们版本已经更新，而这个sample还停留在史前时期，run都run不起来，所以需要点手段来把它运行起来：

首先 clone下来
然后 checkout 出 1.0.1.RELEASE分支或者v1.0.1.RELEASE的tag
```
git checkout 1.0.1.RELEASE
```
再然后再执行
```
mvn spring-boot:run
```
注意这个101r的tag或者分支里面还没有maven wrapper，所以说明这个mvnw是spring boot initializer的opinion

这下就能跑起来了，也是8888端口，如起所说，执行
```
curl localhost:8888/foo/development
```
内容和文档里面的是极不一样的，所以真不知道它这文档照着什么写的，这里主要是记录下，想要pretty的curl format输出，可以这样
```
curl localhost:8888/foo/development | python -m json.tool
```

接下来一段非常有用，介绍怎么通过HTTP来实际取得配置的内容，copy如下
```
/{application}/{profile}[/{label}]
/{application}-{profile}.yml
/{label}/{application}-{profile}.yml
/{application}-{profile}.properties
/{label}/{application}-{profile}.properties
```
可以看出就是三个要素来回来去的捣鼓，这三个要素分别标识的含义在后面2.1节有详细描述，为了强调，也不妨copy一下：

>    {application}, which maps to spring.application.name on the client side.
>
>    {profile}, which maps to spring.profiles.active on the client (comma-separated list).
>
>    {label}, which is a server side feature labelling a "versioned" set of config files.

application 和 profile 熟悉spring boot的同学都会很快理解是什么，那么label是什么呢？

2.1.1节正文有明确说明，{label}用来映射一个`a git label`，一个git label就是指commit id, branch name, or tag

所以说么我就觉得奇怪，明明是版本化的，为什么很多和diamond之流对比说不能支持灰度发布？只是去做对比的人没有理解这里面的内在设计吧

然后讲的是最重要的一个服务端的配置项：spring.cloud.config.server.git.uri

## 1.1 Client Side Usage

这节明显是一个客户端的quick start，不妨跟着来一遍，但是估计是假设读者非常熟悉spring boot的每个细节，所以给出的配置文件，代码都是片段，那这里补全

首先搞一个project的骨架

```bash
spring init -d=web,cloud-config-client --description="a cloud config client app" -g io.leizh -a cloud-config -n cloud-config-client cloud-config-client
```

这样好像pom里面就不用补充文档里面的东西了

然后按文档把启动类里面的东西放进去...可是这样行吗？能说明什么问题呢？所以我们不妨按[官网](https://cloud.spring.io/spring-cloud-config/)里面的quick start来改，补充上这两段

```
    @Value("${config.name:There}")
    String name = "World";

    @RequestMapping("/")
    public String home() {
        return "Hello " + name;
    }
```

熟悉Spring的同学一定也知道为什么这里的属性值为什么那么写

可是这样并不能表示client和config server连起来了，文档中给出了一个验证的方法，用localhost:8080/env，但是这下又一次表明文档写的不全

_**...to be continue...**_