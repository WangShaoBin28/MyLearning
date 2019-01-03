# 概述

Spring Cloud 的文档整体来说，没有Spring Boot的那么...成熟？

或者它本身就面对的是更宏大的主题，是探索性的工程，至少和Spring Boot的团队的组织方式是不一样的，整个Spring Cloud作为一个整体应该是一个巨大的松散的团队，这个从Reference的组织形式中可以试图推测一下，它下面每一个部分都应该有着自己各自非常独立的目标，Spring Boot从这个角度看，也许称其为Spring Cloud的一部分也不为过

Spring Cloud和Spring Boot的联系紧密，除了特定大版本有强绑定的关系，很多细节也需要辨认，哪些是属于Spring Boot项目的，哪些是属于Cloud的，这不是为了纯粹性或什么理想，而纯是为了工作时候查找资料方便理解，比如，Spring Cloud引入了一个所谓的bootstrap上下文的概念，看这名字以为是Spring Boot的，但真的是Spring Cloud附加的内容，很多非一手资料往往这个地方都弄混了

# Spring Cloud的构成
Spring Cloud，可以认为由一票的子项目构成，这个可以从Spring Cloud的[首页](http://projects.spring.io/spring-cloud/)获知，但是这个页面的分类看起来又和Reference的不尽相同

## 先以 Reference 为参照来看Cloud的结构

## 主页的列表

+ Spring Cloud Config

我十分怀疑这是一个被广泛低估的组件，Spring Cloud所有官方文档开篇都会强调这个部分，目前看起来它的灵感来源就是对12 factor的外化配置部分的强化，这可能和国内一众的配置中心项目的侧重点都有所不同

+ Spring Cloud Netflix
+ Spring Cloud Bus
+ Spring Cloud for Cloud Foundry
+ Spring Cloud Open Service Broker
+ Spring Cloud Cluster
+ Spring Cloud Consul
+ Spring Cloud Security
+ Spring Cloud Sleuth
+ Spring Cloud Data Flow
+ Spring Cloud Stream
+ Spring Cloud Stream App Starters
+ Spring Cloud Task
+ Spring Cloud Task App Starters
+ Spring Cloud Zookeeper
+ Spring Cloud for Amazon Web Services
+ Spring Cloud Connectors
+ Spring Cloud Starters
+ Spring Cloud CLI
+ Spring Cloud Contract
+ Spring Cloud Gateway
+ Spring Cloud OpenFeign
+ Spring Cloud Pipelines
+ Spring Cloud Function

_to be continue..._

