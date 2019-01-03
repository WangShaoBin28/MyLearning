## 参考导读推荐：

[极客时间专栏 - 深入剖析kubernetes](https://time.geekbang.org/column/116)

[官方文档](https://kubernetes.io/zh/docs/home/)，有些连接是有中文的，但是它没列出来，尝试自己浏览器地址栏上加上zh就可以了，能不能出来凭运气

因为k8s的官方中文文档目录索引很奇怪，可以考虑参考中文社区维护的一份[文档](http://docs.kubernetes.org.cn/)

[wiki页](https://en.wikipedia.org/wiki/Kubernetes)包含一个不错的架构总述

[这里](https://jimmysong.io/kubernetes-handbook/)还有一组文章

总的来说，能搜到的中文资料，比较系统的较陈旧，较新的则偏零碎，注意甄别

## 与docker的关系

kubernetes学习曲线有点陡，如果预先了解一些docker的概念并且有一定的操作经验，会稍微轻松一些，但帮助有限；kubernetes的现实目标是以容器为基础的服务编排，它的着眼点是服务编排、集群管理，容器、docker只是它解决其目标问题得手段之一，真正困难的是从多大程度上了解和明白它要解决的问题

如果可能，相互比照着学习也会是一个不错的方法，按官方k8s的文档来学习，顺着指引就安装了docker，一开始在kubernetes里面跑服务也尽可以是些nginx，mysql之流，也不用一开始就花心思去学docker image如何制作，可以学到那里再开始也来得及

## 关注重点

这里的重点是起步：安装、上手、以及通向生存之路的指引

### 安装

安装指的是安装一个最小化可用的实例，不包括最终生产环境的高可用配置

kubernetes的安装是个大问题，按说最好的学习入口是minikube（这一点和docker正好相反，这个bundle很有价值，docker for win/mac更像把问题搞复杂了，minikube确实是简化了问题——一个易于上手的环境），但是因为有墙，打了点折扣，但还好有[好事者](https://yq.aliyun.com/articles/221687)解决了绝大多数的问题

另一个值得考虑使用[Rancher](https://www.cnrancher.com/)来执行安装kubernetes集群，而且Rancher号称自己产品是生产级别的，相比较起来，界面也比dashboard做了必要的增强，又没有添很多累赘的东西；另外，毕竟后面还有一些事情，Rancher也能起到很好的辅助作用，Rancher单机安装也很容易，几乎无门槛，可参考[这里](https://www.cnblogs.com/DaweiJ/articles/8984872.html)手把手

如果可能，还是应当尝试独立安装kubernetes，有助于更进一步的了解和理解k8s的架构；极客时间专栏推荐[kubeadm](https://kubernetes.io/zh/docs/setup/independent/install-kubeadm/)，这也是未来官方支持的面向生产的解决方案，但专栏对此没做过多细节描述，绕墙的技巧自然是不能多说，比较敏感，不方便公开的仔细地说；如果遇到任何拉镜像的问题，可以参考[这里](https://blog.csdn.net/jinguangliu/article/details/82792617?utm_source=blogxgwz0)，细节就不多细扯了，有洁癖的自己搭一个，没洁癖的用别人搭好的一样；如果说墙有什么好处，那也就是逼着不得不在这个阶段就先多明白一点docker image制作和使用的一些概念了

如果不想折腾梯子，又不想在境外花钱租个vps（其实GCP、AWS、Azure都有免费额度可用，也可以考虑），暂时想绕过去进入下一个阶段，首选阿里云修改版的minikube，或者Rancher

### 上手

这里上手指的是开始使用kubectl，这是正统用法；而不是 Rancher 或 dashboard的界面里面点点点

上手最重要的是要安装并配置kubectl，这有个前提就是要 _**能**_ 获取kubeconfig文件

+ minikube 简化了这个问题，安装时候会自动配置完成
+ 借助Rancher获取到kubeconfig文件，可仔细阅读[这里](https://www.cnblogs.com/DaweiJ/articles/8984872.html)寻找kubeconfig获取位置

kubectl本身的安装和配置

+ 直接参考[这个](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)，需要生活扶梯
+ 正确[放置](https://kubernetes.io/docs/tasks/tools/install-kubectl/#configure-kubectl)kubeconfig文件
  - 如果是minikube，去对应的路径看一下它确实在那里了！
+ 记得配置好[自动补全](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion)
  - 这一点windows下跑kubectl就差点了，但是还好有win10，因为win10有[WSL](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10)，所以可以看这里[试试](https://medium.com/@sandipchitale/command-completion-for-minikube-and-kubectl-on-windows-10-580710bc464c)

好了这时候就可以跑一把了

```
kubectl run myredis --image=redis
```

然后（最好要有自动补全，否则不保证能玩儿的转），敲下

```
kubectl exec -it myredis-669b775fcf-gtm27 redis-cli
```
就可以看见redis-cli的提示符了，其中myredis-669b775fcf-gtm27是要自动补全出来的，会和这里的不一样的，或者用```kubectl get pods```来看一下，这个pod到底叫什么

如果会那么一点docker，最好忍住了别用docker的命令来操作，否则无法领会kubectl的妙处

### 生存

由于社区的努力，安装和上手kubernetes没意外一天得时间就够了，但至于如何生存...

这个比较麻烦了，因人而异，只能靠自己多练习多学习，这里只帮忙寻找一些目标学习任务，不涉及细节

+ 上面上手篇使用的是所谓的[imperative commands](https://kubernetes.io/docs/concepts/overview/object-management-kubectl/overview/#imperative-commands)方式来操控kubernetes集群，但如果想登堂入室，是需要了解[其他的方式](https://kubernetes.io/docs/concepts/overview/object-management-kubectl/overview/#management-techniques)，其他两种，才能叫编排，编排文件怎么写，可以参考[官方文档](https://kubernetes.io/zh/docs/tasks/run-application/run-stateless-application-deployment/#%E5%88%9B%E5%BB%BA%E5%92%8C%E6%8E%A2%E7%A9%B6%E4%B8%80%E4%B8%AAnginx-deployment)来入门，然后一步一步慢慢来，如果说大概有个指引，那就是有个metadata，然后再指定个spec，然后balabala
+ 除了跑起来一个服务，还得能让服务对外是可用的，这就涉及到补概念的课了
+ [service](https://kubernetes.io/zh/docs/concepts/services-networking/service/)的用途和分类，[pod](https://kubernetes.io/docs/concepts/workloads/pods/pod/)得设计目的，等等

其他的一些常见主题，存储、网络，不是标准的应用研发视角内容，但都是非常重要的架构概念，具体的实施责任在系统工程师和运维角色的工程师那里，可以按需学习

### 案例

我们自己的持续集成环境是一个活生生得入门应用案例，使用的都是最粗浅的功夫搭建起来的，可以用于参考：

+ [编排文件](http://10.1.32.31/infra/deploy-rancher)
+ [操控编排文件的脚本](http://10.1.32.31/infra/jenkins)

