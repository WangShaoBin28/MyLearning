这是非常重要的一环，构成Spring Boot半壁江山

为什么叫actuator，这东西无从考证，总之是个很技术流的东西，很多基于Spring Boot的框架，比如Spring Cloud，也充分在利用actuator的特点，例如重要的基础设施，Spring Cloud Config合 Spring Cloud Netflix Zuul，都会缺省包含actuator的starter，意味着这两个服务实际上都不用在显式的包含starter在dependency中了，但是一些关键功能，还需要特别的激活，同时Spring Boot 2.0有一个改变，所有关于actuator的endpoints，都放置在了path /actuator下，这是需要注意的点

_**...to be continue...**_