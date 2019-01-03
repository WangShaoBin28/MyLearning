## 参考导读推荐：

[阮一峰 - Docker 入门教程](http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html)，这算是一篇手把手的导读

[官方的中文文档](https://docs.docker-cn.com/)，停留在1706上，同时缺失不少高级主题的翻译

## 关注重点

起步：安装、上手、以及通向生存之路的指引，面向0起点

### 安装

docker基本上是个单机的玩意儿，所以安装起来并不复杂，看官方文档即可，阮老师的文章也是直接引官方文档，因为过程实在没什么特别再额外强调的

我这里给一个非常个人化的建议，看官根据自己的学习习惯来参考，那就是不要用docker for windows这类bundle产品来入门，详述如下

+ 首先是必须要明白docker说的容器就是linux容器而不是其他，所以docker for windows/mac这类产品本质上也就是个虚拟机加个周边
+ 然后就是周边，其实就是docker的客户端服务器架构的能力，win/mac上装一个docker客户端，操控另一台机器上的docker引擎而已
+ 任何非linux平台上的docker产品解决方案不是它们不能用，而是涉及了一些docker公司自身战略利益的鸡肋产品，而这些东西估计现实中除非特别的原因，否则碰她意义也不大，比如docker-machine，当然多了解学习一下也没坏处
+ 所以建议一开始为了后面上手直接装个虚拟机，省掉复杂的docker for win/mac 产品理解，直接linux里去耍docker完事了

另外，关注下官方文档安装中```yum list docker-ce --showduplicates | sort -r```的上下文，可以指引安装一个非最新版本

### 上手

对于docker，阮老师那篇不错，基本涵盖了常用的命令和基本概念，所以这一节基本内容参考该篇即可

但是阮老师举得例子是那个官方的hello-world，没什么鸟用，这里以redis为例，启动并访问一下

+ 启动 ```docker run -d --rm --name myredis redis```
+ 连上去看一看手法一 ```docker run -it --rm --link myredis:rs redis redis-cli -h rs```
+ 连上去看一看手法二 ```docker exec -it myredis redis-cli```

如果想从另外一台机器上连呢？那启动时候得映射一个主机端口

+ 先把刚那个关了 ```docker stop myredis```
+ 如果一开始忘了加--rm，光关了容器还会保留，想清的干干净净需要这么关```docker stop myredis | xargs docker rm```

来正格得了，启动时候映射一个主机端口
+ 启动 ```docker run -d --rm --name myredis -p 6379:6379 redis```
+ 假设另外一台机器也装了docker，那么```docker run -it --rm redis redis-cli -h 10.0.2.15```

要记得，本机启动一个容器来跑redis-cli但是非link方式来连这个redis-server，不能用本地回环地址

大致是这些，应该比阮老师那个更实用主义一点

除此之外，值得再了解下docker-compose的用法，因为他可以把docker 的命令、子命令、option等文档化（也就是更利于版本化），符合通常的配置管理实践原则，只是从其产品目的上看，也是主要关注开发和测试的流程，而不是生产环境，本质上是一个提高个人生产力的工具（事实上，docker试图将其作为另服务编排工具的努力失败了，现在这个产品很尴尬）；可以把玩一下

### 生存

这里还是只设目标不列举细节

+ 使用docker来把redis、nginx、mysql等所有自己经常要用到的基础设施run起来用于开发的调试，上面上手的redis很初级
+ 自定义上述环境的配置，了解二者如何挂卷——数据、配置，如何设置环境变量——另一个主要的配置值来源
+ 逐渐将上述环境应用于日常开发测试，这里有个例子，[平台侧调试用相关工程](http://10.1.32.31/lzh/platform-debug-workspace)，这是UAT之前的一个版本，当时只做到能run起来，但还是需要额外的安装node和maven来执行构建，内有详细说明；在这个过程中会涉及到
  - 大致了解docker image的制作，Dockerfile中的各种指令用途（其实真正有用的Dockerfile也不一定多复杂，参照我们自己的）
  - javaer可以了解一下JDK8关于容器cpu和内存限制支持的[混乱历史](http://www.concurrent.work/docker/java/jvm/gc/pitfalls-about-running-java-inside-container/)
  - 使用spring boot的javaer还要关注下如何[启动容器时传入](https://medium.com/@cl4r1ty/docker-spring-boot-and-java-opts-ba381c818fa2)必要的虚拟机参数
  - 还是javaer，还得注意如何在容器内[使用jmap -heap这类传统扳手](https://blog.csdn.net/kinginblue/article/details/78078028)
+ 了解下docker registry世界的命名规则

### 一些可能会用到的工具脚本（只适用于centos）

+ [安装docker](https://raw.githubusercontent.com/leizhnxp/dotfiles/master/tools/installer-scripts/install_docker_ce.sh)，这只是安装最新的
+ [安装docker-compose](https://raw.githubusercontent.com/leizhnxp/dotfiles/master/tools/installer-scripts/install_docker_compose.sh)，从我个人使用经验来看，新版算是有bug，所以我自己工具箱里面的维持了一个旧版本号

