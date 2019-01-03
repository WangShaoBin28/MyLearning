## 24. Externalized Configuration

所谓外化配置，是对[12factor](https://12factor.net/zh_cn/)的一种引申回应，heroku在配置建议放在环境变量上确实比较粗暴，这里连opinionated的Spring Boot都看不下去了，所以搞了这么一套复杂的规则来给喜爱它的开发者以近乎有点过火的甜蜜...真的他么的选择太多了，怎么整呢？

在这里Spring Boot说，可以通过

+ properties，YAML
+ 环境变量
+ 命令行

来外化配置，看起来还好，接下来就可怖了，列出了一个优先级列表来说明它内部工作的一个大概机制，几个重要的项目：

+ 生产时候，命令行的优先级最高
+ 然后是执行java启动前的SPRING_APPLICATION_JSON，tip里面详细介绍了这种形式
+ 考虑到实用性，接下来一个可以记住是OS级的环境变量
+ 我们最熟悉的application文件，依次是：
  - jar包外的profile类型的
  - jar包内的profile类型的
  - jar包外的不带profile的
  - jar包内的不带profile的

然后举了栗子说明如何应用配置值在程序中，都很熟悉的Spring侵入注解@Value("${name}")

### 24.1 一个有用的随机属性值配置器，测试时利器啊

### 24.2 命令行参数怎么用，还有怎么禁用掉命令行参数

### 24.3 指明老朋友application属性文件会从哪些目录去找，或者怎么传入给程序

### 24.4 

_to be continue..._
