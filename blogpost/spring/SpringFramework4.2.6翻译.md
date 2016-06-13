##Part I. Spring Framework概述
http://docs.spring.io/spring/docs/4.2.6.RELEASE/spring-framework-reference/htmlsingle/#overview-getting-started-with-spring

Spring Framework是一个轻量级的解决方案,在构建一站式企业级应用上有很大的潜能。然而,Spring是模块化的,允许你只用你需要的模块,而不需要引用其余部分。你可以使用IoC容器,可以选择它支持的任何web框架,你也可以仅仅整合Hibernate或者JDBC抽象层使用。
Spring Framework支持声明式的事务管理,通过RMI或者web services进行远程访问业务逻辑,并且提供多种数据持久化解决方案。它提供一个全功能的MVC框架,允许你透明的整合AOP到你的软件中。

Spring被设计为非入侵式的,也就是说你的业务逻辑代码通常不需要依赖Spring框架自身。在整合层面(例如数据访问层),一些依赖于数据访问技术和Spring的类库会存在。但是,也很容易将这些依赖从你剩余的代码中分离出来。

本文档是Spring Framework特性的参考指南。如果你对这份文档有任何的要求,意见,问题,请联系列表上的人员(https://groups.google.com/forum/#!forum/spring-framework-contrib).框架的问题可以在StackOverflow上进行提问(see https://spring.io/questions)。

### 1. 开始Spring
这份文档提供Spring Framework的详细信息。它提供所有功能的全面文档,以及一些Spring有关的概念(例如"依赖注入")。如果你刚开始使用Spring,你可能想要通过创建一个Spring Boot基础应用来使用Spring Framework。Spring Boot提供一个快速的(并且opinionated)的方式来创建production-ready的Spring基础应用。它基于 Spring Framework,约定优于配置的特点,使得你能够最高效的创建运行你的应用。


### 2. 介绍Spring Framework
Spring Framework是一个Java平台,它提供了对开发Java应用程序的一种广泛的基础支持。Spring负责控制这个基础,使得你可以集中精力于你的应用。

Spring允许你从"普通Java对象(POJO)"来构建应用程序,并且将应用企业级服务非入侵的应用于POJ。此功能适用于Java SE编程模型并且部分获取全部适用于Java EE。

作为一个应用开发者,下面是你可以通过使用Spring平台带来的一些好处的例子。
* 让一个Java方法执行数据库事务而不需要处理事务api;
* 让一个本地Java方法来访问远程程序而不需要处理远程访问api;
* 让一个本地Java方法来执行管理操作而不需要处理JMX的api;
* 让一个本地Java方法处理消息而不需要处理JMS的api。

####2.1 依赖注入与控制反转
A Java application — a loose term that runs the gamut from constrained, embedded applications to n-tier, server-side enterprise applications — typically consists of objects that collaborate to form the application proper. Thus the objects in an application have dependencies on each other.
Java应用程序--一个宽松的术语

尽管Java平台提供了丰富的应用的程序开发功能,但是它缺乏组织基本模块到一个整体的方式,而把这个任务留给了架构师和开发者。尽管你可以使用设计模式例如工厂模式,抽象工厂模式,构建模式,装饰模式,和服务定位模式来组合各个类和构成应用程序的对象实例来创建一个应用,然而这些设计模式是简单的:最佳方式是给定一个名称,并且描述这个设计模式做了什么,在哪里使用了它,它所强调的问题是什么等等。模式是形式化的最佳实践,你必须在你自己的应用里实现。

Spring Framework的控制反转(IoC)组件提供组合不同的组件到完整可用的应用程序的形式化方法来强调这个问题。Spring Framework编写了形式化的设计模式作为顶级对象,你可用用来整合到你的应用程序中。很多组织和研究机构使用Spring Framework的这个方式来设计健壮的,可维护的应用程序。

> **背景** "问题是, 反向控制哪一方面?" 在2004年, Martin Fowler 在他的个人网站上提出了这个关系控制反转(IoC)问题. Fowler 建议重新命名控制反转, 使得它更清晰的解释说明,同时提出了依赖注入的概念。

#### 2.2 模块
Spring Framework由大约20个功能模块构成。这些模块包含Core Container, Data Access/Integration,  Web, AOP(Aspect Oriented Programming),Instrumentation, Messaging, 和Test,参见下图
![pic2](https://github.com/chlsmile/blogfile/blob/master/blogfile/spring-overview.png)

The following sections list the available modules for each feature along with their artifact names and the topics they cover.
Artifact names correlate to artifact IDs used in Dependency Management tools.

##### 2.2.1 核心容器
核心容器包含spring-core,spring-beans,spring-context,spring-context-support,和spring-expression(Spring Expression Language)模块。

spring-core和spring-beans模块提供spring框架的基础功能,包含控制反转和依赖注入特性。BeanFactory是一个复杂的工厂设计模式的实现。它消除了编程式的单例方式,允许你解除配置与你实际程序逻辑之间的耦合。

Context(spring-context)模块稳固的构建在Core和Beans模块之上:意味着采用框架类似于JNDI注册的方式来访问对象。Context模块继承了Beans模块的特性并且增加了国际化支持(应用在,例如,资源包),事件传播,资源加载,和透明的创建上下文,例如,Servlet容器。Context模块也支持Java EE特性,例如, EJB, JMX和基本的远程处理。ApplicationContext接口是Context模块的核心接口。spring-context-support 提供了对第三方类库的与Spring应用上下文的支持例如缓存(EhCache, Guava, JCache),邮件(JavaMail),调度(CommonJ, Quartz)和模版引擎(FreeMarker, JasperReports, Velocity)。

spring-expression模块为查询和运行时操作的对象图提供一个功能强大的表达式语言。它是作为JSP2.1规范的一个统一语言表达式的一个扩展(unified EL)。该语言支持设置与获取属性值,属性赋值,方法调用,访问数组内容,集合和索引,逻辑和算术运算符,命名变量的内容,从Spring的控制反转容器通过name检索对象。它还支持集合的映射,集合的获取,和集合的聚合。



2.2.2 AOP and Instrumentation

The spring-aop module provides an AOP Alliance-compliant aspect-oriented programming implementation allowing you to define, for example, method interceptors and pointcuts to cleanly decouple code that implements functionality that should be separated. Using source-level metadata functionality, you can also incorporate behavioral information into your code, in a manner similar to that of .NET attributes.

The separate spring-aspects module provides integration with AspectJ.

The spring-instrument module provides class instrumentation support and classloader implementations to be used in certain application servers. The spring-instrument-tomcat module contains Spring’s instrumentation agent for Tomcat.

##### 2.2.3 消息
Spring Framework 4 includes a spring-messaging module with key abstractions from the Spring Integration project such as Message, MessageChannel, MessageHandler, and others to serve as a foundation for messaging-based applications. The module also includes a set of annotations for mapping messages to methods, similar to the Spring MVC annotation based programming model.
Spring Framework 4包含了一个spring-messaging模块从Spring Integration

##### 2.2.4 数据访问/集成
数据访问/集成层包含JDBC, ORM, OXM, JMS和Transaction模块。

spring-jdbc模块提供一个JDBC抽象层,它移除了冗长的JDBC编码，并解析了数据库提供商特定的错误代码。

spring-tx 模块支持对实现特定接口的类和所有POJO（普通Java对象）的编程式和声明式的事务管理。

spring-orm模块提供了对流行的对象-实体映射API的整合层,包括 JPA, JDO和Hibernate。使用spring-orm模块你就可以使用全部的O/R-映射框架并使用其它Spring提供的特性。例如前面提到的简单声明式的事务管理特。

spring-oxm模块提供了支持JAXB，Castor，XMLBeans，JiBX和Xstream Object/XML映射实现的抽象层。

spring-jms模块(Java消息服务)包含生产和消费消息特性。自从Spring Framework 4.1,它集成了spring-messaging模块。



#####2.2.5 Web
Web层由spring-web,spring-webmvc,spring-websocket和spring-webmvc-portlet模块组成。

spring-web模块提供基础的面向web的集成特性,例如分段文件上传功能,使用Servlet监听器和面向web的应用上下文对IoC容器进行初始化。它也包含一个HTTP client和Spring远程调用相关的网络部分。

spring-webmvc模块(也被称作Web-Servlet模块)包含Spring的模型-视图-控制器(MVC)和REST Web风格服务实现的Web应用程序。Spring的MVC框架提供了一个在model代码和Web表单之间的整洁分离，并且整合了其它所有Spring框架的特性。

spring-webmvc-portlet模块(也被称作Web-Portlet模块)提供Portlet环境与spring-webmvc模块的镜像功能的mvc实现。

#####2.2.6 测试
spring-test模块支持单元测试并且集成了Spring JUnit和TestNG测试组件。它提供了与Spring ApplicationContexts和caching上下文一致的加载。它还提供了可用于隔离对代码进行测试的模拟对象。

