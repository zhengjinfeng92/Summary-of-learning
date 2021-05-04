## spring  cloud

### 什么是微服务架构

### 架构演变

单体架构-> SOA 面向服务架构-> 微服务架构

#### 单体架构

所有的处理包括数据库连接、业务逻辑处理、展示逻辑等都放在单体运用中；

转变成多层架构，是按照技术职责将应用做水平拆分，每一层解决的技术问题相对集中，层与层之间做单向依赖。这样做可以帮助我们更好的管理我们的代码，大大提升了后期的维护效率；但仍然是单体架构

优点：

- 开发简单，不需要在多个运用中来回调用
- 测试简单
- 部署简单
- 开发迅速

缺点：

- 应用膨胀
- 团队合作冲突
- 运行效率&稳定:单个功能影响整个系统

单体架构原有的迅速、简单的优点，随着规模的扩大（功能、团队），会变得荡然无存

解决：

分而治之 ->拆分->如何拆分



#### SOA架构

Service-Oriented Architecture直译为“面向服务的架构”

> 面向服务的架构（SOA）是一个组件模型，它将应用程序的不同功能单元（称为服务）
> 进行拆分，并通过这些服务之间定义良好的接口和协议联系起来。接口是采用中立的方
> 式进行定义的，它应该独立于实现服务的硬件平台、操作系统和编程语言。这使得构件
> 在各种各样的系统中的服务可以以一种统一和通用的方式进行交互

与单体架构按照技术职责进行水平拆分不同，SOA 会按照业务领域对应用进行粗粒度
的垂直拆分，至于拆分到什么程度，哪些领域可以放在一起等类似问题，可以参考一下康威
定理

问题：

服务间的依赖和调用

解决技术方案：

XML,SOAP,WSDL,UDDI,ESB

soa架构的问题：

- 高门槛：系统复杂
- 厂商绑定：标准不统一
- 不适应云环境
- 中心化

#### 微服务架构

![](.\pic\soa与微服务架构区别.png)

SOA 解决的核心问题是复用，而微服务解决的核心问题是扩展

***什么是微服务架构：***

> The microservice architectural style is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API. These services are built around business capabilities and independently deployable by fully automated deployment machinery. There is a bare minimum of centralized management of these services, which may be written in different programming languages and use different data storage technologies.?

> 微服务体系结构风格，是一种将单个应用程序开发为一套小型服务的方法，每个进程都在自己的进程中运行，并与轻量级机制(通常是HTTP资源API)通信。这些服务是围绕业务功能构建的，可以通过完全自动化的部署机制独立部署。这些服务可能是用不同的编程语言编写的，使用不同的数据存储技术，对这些服务的集中管理是最低限度的。

微服务的架构要考虑的问题:

通过服务实现组件化

- 根据业务组织系统
- 做产品而不是做项目
- 简单高效的通信协议
- 自动化基础设施
- 面向失败的设计
- 具备进化能力的设计

今天我们所说的“微服务”是一个庞大且复杂的概念集合，它既是一种架构模式，也是
实现这种架构模式时所使用的技术方案的集合。

微服务不是银弹

微服务的缺点：

- 分布式的代价。原本在单体应用中，很多简单的问题都会在分布式环境下被几何级的放
  大。例如分布式事务、分布式锁、远程调用等，不光要考虑如何实现他们，相关场景的
  异常处理也是必须要考虑到的问题。
- 协同代价。如果你经历过一个项目上线需要发布十几个应用，而这些应用又分别由多个
  团队在维护。你就能深刻的体会到协同是一件多么痛苦的事情了。
- 服务拆分需要很强的设计功力。微服务的各种优势，其中一个重要的基础是对服务领域
  的正确切分。如果使用了不合适的切分粒度，或者是错误的切分方法，都会让服务不能
  很好的实现高内聚低耦合的要求。