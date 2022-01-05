---
title: "Spring cloud 微服务架构"
date: "2020-09-23"
tags: [ "spring cloud","架构"]
categories:
  - "后端" 
---

## 结构

### [Eureka](https://github.com/Netflix/eureka)

>微服务注册表可实现弹性的中间层负载平衡和故障转移。.

微服务发现框架

- `Eureka Client`：负责将这个服务的信息注册到Eureka Server中
- `Eureka Server`：注册中心，里面有一个注册表，保存了各个服务所在的机器和端口号

### [Feign](https://github.com/OpenFeign/feign)

>使编写Java HTTP客户端更加容易

简化微服务之间的请求代码

### [Ribbon](https://github.com/Netflix/ribbon)

>Ribbon 是一个进程间通信（远程过程调用）库，具有内置的软件负载平衡器。主要使用模型涉及具有各种序列化方案支持的REST调用

负载均衡工具

场景：

请求一个服务（有多个主机），可以均衡的请求

### [Hystrix](https://github.com/Netflix/Hystrix)

>Hystrix 是一个延迟和容错库，旨在隔离对远程系统，服务和第三方库的访问点，停止级联故障，并在不可避免发生故障的复杂分布式系统中实现弹性。

熔断器

- `雪崩`：因某个请求失败而影响其他微服务，最终导致真个系统崩溃
- `熔断`：隔离请求服务，将其失败不在影响其他服务
- `降级`：请求失败后，采用备选方案处理

### [Zuul](https://github.com/Netflix/zuul)

>Zuul是一项网关服务，可提供动态路由，监视，弹性，安全性等

微服务网关

任何请求通过该网关转发至对应的服务
