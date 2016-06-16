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


#### 2.3 使用场景
前面描述的构建模块使得Spring可以在很多场景中作为业务逻辑实现的选择,from embedded applications that run on resource-constrained devices to full-fledged enterprise applications that use Spring’s transaction management functionality and web framework integration.

图2.2. 典型的功能完善的Spring web应用
![pic](https://github.com/chlsmile/blogfile/blob/master/blogfile/overview-full.png)
Spring的声明式事务管理特性使得Web应用程序可以全部事务化，就好像使用了EJB容器管理的事务。你所有的自定义业务逻辑可以通过简单的POJO来实现，并通过Spring的IoC容器管理。额外的服务支持包括发送邮件,验证对Web层独立，这可以让你选择在哪里执行验证规则。Spring的ORM支持包括对JPA,Hibernate和JDO的支持;例如,在使用Hibernate时,你可以继续使用现在正在使用的mapping文件和标准的Hibernate SessionFactory配置。表单控制器无缝地整合了Web层和领域模型，移除了ActionForm或其它为领域模型转换HTTP参数的类需要。

图2.3. 通过使用Spring中间层来集成第三方web框架
![pic](https://github.com/chlsmile/blogfile/blob/master/blogfile/overview-thirdparty-web.png)

有些情况不允许你完全切换成另外一种框架。Spring框架不强迫你式使用它的全部api,它不是一个全有或者全无的解决方案。现有的一些使用了Struts,Tapestry,JSF或者其它的UI框架可以使用Spring基础中间件进行集成,从而允许你可以使用Spring事务管理特性。使用ApplicationContext和WebApplicationContext集成到你的web层,从而你只需要关注你的业务逻辑。


图2.4. 远程调用使用场景
![pic](https://github.com/chlsmile/blogfile/blob/master/blogfile/overview-remoting.png)

当你需要通过web服务来访问已有的code,你可以使用Spring的Hessian,Burlap,Rmi或者JaxRpcProxyFactory类。从而使得在应用里进行远程访问不再困难。

图2.5. EJBs - 包装已经存在的POJOs
![pic](https://github.com/chlsmile/blogfile/blob/master/blogfile/overview-ejb.png)

Spring Framework也提供了对企业级Java Bean的访问和抽象层,可扩展包装它们到无状态会话bean,不安全的Web应用可能需要声明式安全。

##### 2.3.1 依赖管理与命名约定
依赖管理与依赖注入是两个概念。要在应用程序中添加Spring的特性(例如依赖注入),你需要组合所需的类库(jar文件)并添加到在运行时环境的类路径中,而编译时也是需要的。这些依赖不是注入的虚拟组件,而是文件系统(通常是这样)的物理资源。依赖管理的过程包括定位那些资源，存储它们并将它们添加到类路径中。依赖可以是直接的(例如,我的应用在允许期间时依赖Spring),或者间接的(例如,我的应用依赖于commons-dbcp,而commons-dbcp依赖于commons-pool)。间接的依赖也被认为是“过度的”,而且那些依赖本身就难以识别和管理的。

如果你决定使用Spring你需要拷贝你需要的相应的Spring jar包。为了方便使用,Spring尽可能的按照模块的方式进行了打包,所以例如,如果你不需要开发一个web应用你就不需要使用spring-web模块jar包。为了参考Spring的类库模块在这份文档里用了一个简单方便的命名方式spring-*或者spring-*.jar，这里的“*”代表了模块的简短名称(比如,spring-core,spring-webmvc,spring-jms等)。真实的jar文件命名通常是带有版本号的(例如spring-core-4.2.6.RELEASE.jar)。



Each release of the Spring Framework will publish artifacts to the following places:
每个Spring Framework release版本通常发布在下面这些地方:



Maven Central(maven中央仓库),Maven仓库默认的地址,不需要进行特殊的配置,直接就可以获取。
许多Spring依赖的常用类库在Maven Central中也可以获取到,同时Spring社区大多数用户使用Maven作为依赖管理工具，这对于他们来说是很方便的。
这里jar包的命名是spring-*-<version>.jar格式的，并且Maven的groupId是org.springframework。
In a public Maven repository hosted specifically for Spring.
In addition to the final GA releases, this repository also hosts development snapshots and milestones.
The jar file names are in the same form as Maven Central, so this is a useful place to get development versions of Spring to use with other libraries deployed in Maven Central.
This repository also contains a bundle distribution zip file that contains all Spring jars bundled together for easy download.
所以首先你需要决定你如果管理你的依赖:我们通常建议你使用自动化的系统类似于Maven, Gradle或者Ivy,当然你也可以自己手动下载你需要的Spring jar包。




You will find bellow the list of Spring artifacts. For a more complete description of each modules, see Section 2.2, “Modules”.
在下面的列表重你将会看到
表格 2.1. Spring Framework Artifacts

GroupId | ArtifactId | Description
------------ | ------------- | ------------
org.springframework | spring-aop  | Proxy-based AOP support
org.springframework | spring-aspects  | AspectJ based aspects
org.springframework | spring-beans | Beans support, including Groovy
org.springframework | spring-context | Application context runtime, including scheduling and remoting abstractions
org.springframework | spring-context-support  | Support classes for integrating common third-party libraries into a Spring application context
org.springframework | spring-core  | Core utilities, used by many other Spring modules
org.springframework | spring-expression  | Spring Expression Language (SpEL)
org.springframework | spring-instrument  | Instrumentation agent for JVM bootstrapping
org.springframework | spring-instrument-tomcat  | Instrumentation agent for Tomcat
org.springframework | spring-jdbc | JDBC support package, including DataSource setup and JDBC access support
org.springframework | spring-jms| JMS support package, including helper classes to send and receive JMS messages
org.springframework | spring-messaging  | Support for messaging architectures and protocols
org.springframework | spring-orm  | Object/Relational Mapping, including JPA and Hibernate support
org.springframework | spring-oxm  | Object/XML Mapping
org.springframework | spring-test  | Support for unit testing and integration testing Spring components
org.springframework | spring-tx  | Transaction infrastructure, including DAO support and JCA integration
org.springframework | spring-web  | Web support packages, including client and web remoting
org.springframework | spring-webmvc  | REST Web Services and model-view-controller implementation for web applications
org.springframework | spring-webmvc-portlet  | MVC implementation to be used in a Portlet environment
org.springframework | spring-websocket  | WebSocket and SockJS implementations, including STOMP support


Spring依赖和基于Spring

Although Spring provides integration and support for a huge range of enterprise and other external tools,
it intentionally keeps its mandatory dependencies to an absolute minimum:
you shouldn’t have to locate and download (even automatically) a large number of jar libraries in order to use Spring for simple use cases.
For basic dependency injection there is only one mandatory external dependency, and that is for logging (see below for a more detailed description of logging options).



Next we outline the basic steps needed to configure an application that depends on Spring,
first with Maven and then with Gradle and finally using Ivy.
In all cases, if anything is unclear, refer to the documentation of your dependency management system,
or look at some sample code - Spring itself uses Gradle to manage dependencies when it is building, and our samples mostly use Gradle or Maven.

Maven依赖管理

If you are using Maven for dependency management you don’t even need to supply the logging dependency explicitly.
For example, to create an application context and use dependency injection to configure an application, your Maven dependencies will look like this:

```java
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>4.2.6.RELEASE</version>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

That’s it. Note the scope can be declared as runtime if you don’t need to compile against Spring APIs, which is typically the case for basic dependency injection use cases.

The example above works with the Maven Central repository. To use the Spring Maven repository (e.g. for milestones or developer snapshots), you need to specify the repository location in your Maven configuration. For full releases:
```java
<repositories>
    <repository>
        <id>io.spring.repo.maven.release</id>
        <url>http://repo.spring.io/release/</url>
        <snapshots><enabled>false</enabled></snapshots>
    </repository>
</repositories>
```

For milestones:
```java
<repositories>
    <repository>
        <id>io.spring.repo.maven.milestone</id>
        <url>http://repo.spring.io/milestone/</url>
        <snapshots><enabled>false</enabled></snapshots>
    </repository>
</repositories>
```

And for snapshots:
```java
<repositories>
    <repository>
        <id>io.spring.repo.maven.snapshot</id>
        <url>http://repo.spring.io/snapshot/</url>
        <snapshots><enabled>true</enabled></snapshots>
    </repository>
</repositories>
```

Maven "Bill Of Materials" Dependency

It is possible to accidentally mix different versions of Spring JARs when using Maven. For example, you may find that a third-party library, or another Spring project, pulls in a transitive dependency to an older release. If you forget to explicitly declare a direct dependency yourself, all sorts of unexpected issues can arise.

To overcome such problems Maven supports the concept of a "bill of materials" (BOM) dependency. You can import the spring-framework-bom in your dependencyManagement section to ensure that all spring dependencies (both direct and transitive) are at the same version.
```java
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-framework-bom</artifactId>
            <version>4.2.6.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

An added benefit of using the BOM is that you no longer need to specify the <version> attribute when depending on Spring Framework artifacts:
```java
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
    </dependency>
<dependencies>
```

Gradle Dependency Management
To use the Spring repository with the Gradle build system, include the appropriate URL in the repositories section:
```java
repositories {
    mavenCentral()
    // and optionally...
    maven { url "http://repo.spring.io/release" }
}
```
You can change the repositories URL from /release to /milestone or /snapshot as appropriate. Once a repository has been configured, you can declare dependencies in the usual Gradle way:
```java
dependencies {
    compile("org.springframework:spring-context:4.2.6.RELEASE")
    testCompile("org.springframework:spring-test:4.2.6.RELEASE")
}
```

Ivy Dependency Management

If you prefer to use Ivy to manage dependencies then there are similar configuration options.

To configure Ivy to point to the Spring repository add the following resolver to your ivysettings.xml:
```java
<resolvers>
    <ibiblio name="io.spring.repo.maven.release"
            m2compatible="true"
            root="http://repo.spring.io/release/"/>
</resolvers>
```

You can change the root URL from /release/ to /milestone/ or /snapshot/ as appropriate.

Once configured, you can add dependencies in the usual way. For example (in ivy.xml):
```java
<dependency org="org.springframework"
    name="spring-core" rev="4.2.6.RELEASE" conf="compile->runtime"/>
```

Distribution Zip Files

Although using a build system that supports dependency management is the recommended way to obtain the Spring Framework, it is still possible to download a distribution zip file.

Distribution zips are published to the Spring Maven Repository (this is just for our convenience, you don’t need Maven or any other build system in order to download them).

To download a distribution zip open a web browser to http://repo.spring.io/release/org/springframework/spring and select the appropriate subfolder for the version that you want. Distribution files end -dist.zip, for example spring-framework-{spring-version}-RELEASE-dist.zip. Distributions are also published for milestones and snapshots.

2.3.2 日志

日志对于Spring来说是非常重要的,有如下几个原因:
a)它是唯一的强制性的外部依赖;
b)每个人都希望看到他使用的工具有一些他想要的输出信息;
c)Spring整合了多种组件,这些组件都会选择一种日志依赖。应用程序开发人员的目标之一就是在核心位置对整个应用程序有一个统一的日志配置，包含对全部的外部组件。因为日志框架的种类有很多,所以变得有些难以选择。

Spring默认的日志依赖是Jakarta Commons Logging API (JCL). 我们的编译是基于JCL的, 并且我们使扩展Spring Framework的类对JCL的Log对象都是可见的。所有Spring的版本都使用相同的日志包是很重要的:因为向后兼容特性的保留,迁移是很容易的,扩展Spring的应用程序也是这样。我们这样做就使Spring中的模块明确地基于commons-logging(JCL的典型实现),在编译时也使得其它模块都基于它。如果你在使用Maven,并想知道在哪儿获取到的commons-logging依赖,那就是从Spring的spring-core模块中获取的。

关于commons-logging比较好的是你不需要做其它的操作就可以使应用程序工作。它有一个运行时的查找算法,在我们都知道的类路径下寻找其它日志框架,并且使用它认为是比较合适的(或者告诉它你需要使用的是哪一个)一个。如果没有可用的,那么你会得到一个来自JDK(java.util.logging或者简称为JUL)看起来还不错的日志。你应该发现Spring应用程序在运行时会有日志打印到控制台上,这是很重要的。

不要使用Commons Logging

不幸的是,在commons-logging中为了方便用户在运行时发现的算法是有问题的。如果我们可以让时光倒流,重新开发Spring框架,我们将换一个不同的日志依赖。我们首选可能会是Simple Logging Facade for Java (SLF4J)日志框架,它也被Spring的开发人员在它们的应用程序中很多其它的工具所使用。

有两种基本的方式来替换commons-logging:

a)对spring-core模块中进行排除依赖(spring-core模块是唯一对commons-logging进行依赖的);
b)依赖一个特殊的commons-logging依赖,使用空jar包来替代(更多信息可以参考SLF4J FAQ)
排除commons-logging依赖,添加如下的依赖排除配置


```java
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.2.6.RELEASE</version>
        <exclusions>
            <exclusion>
                <groupId>commons-logging</groupId>
                <artifactId>commons-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>
```

现在可能因为在classpath下没有JCL API的实现,导致应用不能正常运行,要想解决这个问题需要提供一个新的日志实现。


使用SLF4J

SLF4J是一个干净的依赖并且在运行时比commons-logging更有效, 因为他使用了编译期绑定来替代其它日志组件运行期动态查找机制。这也意味着你必须明确的知道在运行期去做什么,并声明配置它。SLF4J为很多通用的日志框架提供绑定,所以你可以从中选择一个你正在使用的并绑定管理。

SLF4J提供对很多常用日志框架的绑定,包括JCL,它提供反向的功能:桥接其它日志框架和它自己。所以如果要在Spring中使用SLF4J,你需要使用SLF4J-JCL桥接来代替commons-logging依赖。一旦你已经进行了替换,在Spring日志日志调用会转行成SLF4J的API,如果在你应用程序的其它类库使用那个API，那么你需要有一个单独的地方来配置和管理日志。

一个常用的选择可能是桥接Spring的log到SLF4J,并提供一个明确从SLF4J到Log4J的桥接。你需要提供4个依赖(并排除已经存在的commons-logging):桥接工具,SLF4J API,绑定到Log4J,还有Log4J本身的实现。

在Maven中你可以这样配置:
```java
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.2.6.RELEASE</version>
        <exclusions>
            <exclusion>
                <groupId>commons-logging</groupId>
                <artifactId>commons-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>jcl-over-slf4j</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-log4j12</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.14</version>
    </dependency>
</dependencies>
```

这似乎有很多依赖只是为了获取日志。确实是这样,但它是可选的,而且它的性能要比由于类加载器问题的commons-logging好很多,尤其是如果你使用了一个严格限制的容器,比如OSGi平台。据称那也有性能优势,因为绑定是编译时的而不是运行时的。

在SLF4J用户中一个更为常见的选择是使用步骤少并产生更少的依赖的方案,就是直接绑定到Logback。它消除了额外的绑定操作步骤因为Logback直接实现了SLF4J,所以你只需要依赖两个类库(jcl-over-slf4j和logback)而不是四个。如果你要这样做你也需求从其它依赖中(不是Spring)排除对slf4j-api的依赖,因为你仅仅想在classpath中的日志API只有一个版本。

使用Log4J

很多人出于配置和管理目的而使用Log4j作为日志框架。这也很有效率并且易于创建,而且事实上它也是我们构建和测试Spring时在运行时环境中使用的。Spring也提供一些工具来配置和初始化Log4j,所以在某些模块中它也提供了可选的编译时对Log4j的依赖。

要让Log4j和默认的JCL依赖(commons-logging)起作用,你所要做的就是将Log4j放置到classpath下,并且提供配置文件(在classpath的根路径下放置log4j.properties或log4j.xml)而对于Maven用户来说,可以采用下面的maven依赖配置:

```java
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.2.6.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.14</version>
    </dependency>
</dependencies>
```

下面是log4j.properties打印到控制台的日志的配置示例：

```java
log4j.rootCategory=INFO, stdout
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %t %c{2}:%L - %m%n、
log4j.category.org.springframework.beans.factory=DEBUG
```

运行时容器和本地的JCL

Many people run their Spring applications in a container that itself provides an implementation of JCL.
IBM Websphere Application Server (WAS) is the archetype.
This often causes problems, and unfortunately there is no silver bullet solution;
simply excluding commons-logging from your application is not enough in most situations.



To be clear about this: the problems reported are usually not with JCL per se, or even with commons-logging:
rather they are to do with binding commons-logging to another framework (often Log4J).
This can fail because commons-logging changed the way they do the runtime discovery in between the older versions (1.0) found in some containers and the modern versions that most people use now (1.1).
Spring does not use any unusual parts of the JCL API, so nothing breaks there,
but as soon as Spring or your application tries to do any logging you can find that the bindings to Log4J are not working.

In such cases with WAS the easiest thing to do is to invert the class loader hierarchy (IBM calls it "parent last") so that the application controls the JCL dependency, not the container.
That option isn’t always open,
but there are plenty of other suggestions in the public domain for alternative approaches,
and your mileage may vary depending on the exact version and feature set of the container.


Part II. What’s New in Spring Framework 4.x
3. New Features and Enhancements in Spring Framework 4.0
The Spring Framework was first released in 2004; since then there have been significant major revisions: Spring 2.0 provided XML namespaces and AspectJ support; Spring 2.5 embraced annotation-driven configuration; Spring 3.0 introduced a strong Java 5+ foundation across the framework codebase, and features such as the Java-based @Configuration model.

Version 4.0 is the latest major release of the Spring Framework and the first to fully support Java 8 features. You can still use Spring with older versions of Java, however, the minimum requirement has now been raised to Java SE 6. We have also taken the opportunity of a major release to remove many deprecated classes and methods.

A migration guide for upgrading to Spring 4.0 is available on the Spring Framework GitHub Wiki.

3.1 Improved Getting Started Experience
The new spring.io website provides a whole series of "Getting Started" guides to help you learn Spring. You can read more about the guides in the Chapter 1, Getting Started with Spring section in this document. The new website also provides a comprehensive overview of the many additional projects that are released under the Spring umbrella.

If you are a Maven user you may also be interested in the helpful bill of materials POM file that is now published with each Spring Framework release.

3.2 Removed Deprecated Packages and Methods
All deprecated packages, and many deprecated classes and methods have been removed with version 4.0. If you are upgrading from a previous release of Spring, you should ensure that you have fixed any deprecated calls that you were making to outdated APIs.

For a complete set of changes, check out the API Differences Report.

Note that optional third-party dependencies have been raised to a 2010/2011 minimum (i.e. Spring 4 generally only supports versions released in late 2010 or later now): notably, Hibernate 3.6+, EhCache 2.1+, Quartz 1.8+, Groovy 1.8+, and Joda-Time 2.0+. As an exception to the rule, Spring 4 requires the recent Hibernate Validator 4.3+, and support for Jackson has been focused on 2.0+ now (with Jackson 1.8/1.9 support retained for the time being where Spring 3.2 had it; now just in deprecated form).

3.3 Java 8 (as well as 6 and 7)
Spring Framework 4.0 provides support for several Java 8 features. You can make use of lambda expressions and method references with Spring’s callback interfaces. There is first-class support for java.time (JSR-310), and several existing annotations have been retrofitted as @Repeatable. You can also use Java 8’s parameter name discovery (based on the -parameters compiler flag) as an alternative to compiling your code with debug information enabled.

Spring remains compatible with older versions of Java and the JDK: concretely, Java SE 6 (specifically, a minimum level equivalent to JDK 6 update 18, as released in January 2010) and above are still fully supported. However, for newly started development projects based on Spring 4, we recommend the use of Java 7 or 8.

3.4 Java EE 6 and 7
Java EE version 6 or above is now considered the baseline for Spring Framework 4, with the JPA 2.0 and Servlet 3.0 specifications being of particular relevance. In order to remain compatible with Google App Engine and older application servers, it is possible to deploy a Spring 4 application into a Servlet 2.5 environment. However, Servlet 3.0+ is strongly recommended and a prerequisite in Spring’s test and mock packages for test setups in development environments.

[Note]
If you are a WebSphere 7 user, be sure to install the JPA 2.0 feature pack. On WebLogic 10.3.4 or higher, install the JPA 2.0 patch that comes with it. This turns both of those server generations into Spring 4 compatible deployment environments.
On a more forward-looking note, Spring Framework 4.0 supports the Java EE 7 level of applicable specifications now: in particular, JMS 2.0, JTA 1.2, JPA 2.1, Bean Validation 1.1, and JSR-236 Concurrency Utilities. As usual, this support focuses on individual use of those specifications, e.g. on Tomcat or in standalone environments. However, it works equally well when a Spring application is deployed to a Java EE 7 server.

Note that Hibernate 4.3 is a JPA 2.1 provider and therefore only supported as of Spring Framework 4.0. The same applies to Hibernate Validator 5.0 as a Bean Validation 1.1 provider. Neither of the two are officially supported with Spring Framework 3.2.

3.5 Groovy Bean Definition DSL
Beginning with Spring Framework 4.0, it is possible to define external bean configuration using a Groovy DSL. This is similar in concept to using XML bean definitions but allows for a more concise syntax. Using Groovy also allows you to easily embed bean definitions directly in your bootstrap code. For example:

```java
def reader = new GroovyBeanDefinitionReader(myApplicationContext)
reader.beans {
    dataSource(BasicDataSource) {
        driverClassName = "org.hsqldb.jdbcDriver"
        url = "jdbc:hsqldb:mem:grailsDB"
        username = "sa"
        password = ""
        settings = [mynew:"setting"]
    }
    sessionFactory(SessionFactory) {
        dataSource = dataSource
    }
    myService(MyService) {
        nestedBean = { AnotherBean bean ->
            dataSource = dataSource
        }
    }
}
```
For more information consult the GroovyBeanDefinitionReader javadocs.

3.6 Core Container Improvements

There have been several general improvements to the core container:
- Spring now treats generic types as a form of qualifier when injecting Beans. For example, if you are using a Spring Data Repository you can now easily inject a specific implementation: @Autowired Repository<Customer> customerRepository.
- If you use Spring’s meta-annotation support, you can now develop custom annotations that expose specific attributes from the source annotation.
- Beans can now be ordered when they are autowired into lists and arrays. Both the @Order annotation and Ordered interface are supported.
- The @Lazy annotation can now be used on injection points, as well as on @Bean definitions.
- The @Description annotation has been introduced for developers using Java-based configuration.
- A generalized model for conditionally filtering beans has been added via the @Conditional annotation. This is similar to @Profile support but allows for user-defined strategies to be developed programmatically.
- CGLIB-based proxy classes no longer require a default constructor. Support is provided via the objenesis library which is repackaged inline and distributed as part of the Spring Framework. With this strategy, no constructor at all is being invoked for proxy instances anymore.
- There is managed time zone support across the framework now, e.g. on LocaleContext.

3.7 General Web Improvements
Deployment to Servlet 2.5 servers remains an option, but Spring Framework 4.0 is now focused primarily on Servlet 3.0+ environments. If you are using the Spring MVC Test Framework you will need to ensure that a Servlet 3.0 compatible JAR is in your test classpath.

In addition to the WebSocket support mentioned later, the following general improvements have been made to Spring’s Web modules:

- You can use the new @RestController annotation with Spring MVC applications, removing the need to add @ResponseBody to each of your @RequestMapping methods.
- The AsyncRestTemplate class has been added, allowing non-blocking asynchronous support when developing REST clients.
- Spring now offers comprehensive timezone support when developing Spring MVC applications.

3.8 WebSocket, SockJS, and STOMP Messaging
A new spring-websocket module provides comprehensive support for WebSocket-based, two-way communication between client and server in web applications. It is compatible with JSR-356, the Java WebSocket API, and in addition provides SockJS-based fallback options (i.e. WebSocket emulation) for use in browsers that don’t yet support the WebSocket protocol (e.g. Internet Explorer < 10).

A new spring-messaging module adds support for STOMP as the WebSocket sub-protocol to use in applications along with an annotation programming model for routing and processing STOMP messages from WebSocket clients. As a result an @Controller can now contain both @RequestMapping and @MessageMapping methods for handling HTTP requests and messages from WebSocket-connected clients. The new spring-messaging module also contains key abstractions formerly from the Spring Integration project such as Message, MessageChannel, MessageHandler, and others to serve as a foundation for messaging-based applications.

For further details, including a more thorough introduction, see the Chapter 25, WebSocket Support section.

3.9 Testing Improvements
In addition to pruning of deprecated code within the spring-test module, Spring Framework 4.0 introduces several new features for use in unit and integration testing.

- Almost all annotations in the spring-test module (e.g., @ContextConfiguration, @WebAppConfiguration, @ContextHierarchy, @ActiveProfiles, etc.) can now be used as meta-annotations to create custom composed annotations and reduce configuration duplication across a test suite.
- Active bean definition profiles can now be resolved programmatically, simply by implementing a custom ActiveProfilesResolver and registering it via the resolver attribute of @ActiveProfiles.
- A new SocketUtils class has been introduced in the spring-core module which enables you to scan for free TCP and UDP server ports on localhost. This functionality is not specific to testing but can prove very useful when writing integration tests that require the use of sockets, for example tests that start an in-memory SMTP server, FTP server, Servlet container, etc.
- As of Spring 4.0, the set of mocks in the org.springframework.mock.web package is now based on the Servlet 3.0 API. Furthermore, several of the Servlet API mocks (e.g., MockHttpServletRequest, MockServletContext, etc.) have been updated with minor enhancements and improved configurability.

4. New Features and Enhancements in Spring Framework 4.1

4.1 JMS Improvements
Spring 4.1 introduces a much simpler infrastructure to register JMS listener endpoints by annotating bean methods with @JmsListener. The XML namespace has been enhanced to support this new style (jms:annotation-driven), and it is also possible to fully configure the infrastructure using Java config (@EnableJms, JmsListenerContainerFactory). It is also possible to register listener endpoints programmatically using JmsListenerConfigurer.

Spring 4.1 also aligns its JMS support to allow you to benefit from the spring-messaging abstraction introduced in 4.0, that is:

- Message listener endpoints can have a more flexible signature and benefit from standard messaging annotations such as @Payload, @Header, @Headers, and @SendTo. It is also possible to use a standard Message in lieu of javax.jms.Message as method argument.
- A new JmsMessageOperations interface is available and permits JmsTemplate like operations using the Message abstraction.

Finally, Spring 4.1 provides additional miscellaneous improvements:

- Synchronous request-reply operations support in JmsTemplate
- Listener priority can be specified per <jms:listener/> element
- Recovery options for the message listener container are configurable using a BackOff implementation
- JMS 2.0 shared consumers are supported

4.2 Caching Improvements
Spring 4.1 supports JCache (JSR-107) annotations using Spring’s existing cache configuration and infrastructure abstraction; no changes are required to use the standard annotations.

Spring 4.1 also improves its own caching abstraction significantly:

- Caches can be resolved at runtime using a CacheResolver. As a result the value argument defining the cache name(s) to use is no longer mandatory.
- More operation-level customizations: cache resolver, cache manager, key generator
- A new @CacheConfig class-level annotation allows common settings to be shared at the class level without enabling any cache operation.
- Better exception handling of cached methods using CacheErrorHandler

Spring 4.1 also has a breaking change in the CacheInterface as a new putIfAbsent method has been added.

4.3 Web Improvements
- The existing support for resource handling based on the ResourceHttpRequestHandler has been expanded with new abstractions ResourceResolver, ResourceTransformer, and ResourceUrlProvider. A number of built-in implementations provide support for versioned resource URLs (for effective HTTP caching), locating gzipped resources, generating an HTML 5 AppCache manifests, and more. See Section 21.16.9, “Serving of Resources”.
- JDK 1.8’s java.util.Optional is now supported for @RequestParam, @RequestHeader, and @MatrixVariable controller method arguments.
- ListenableFuture is supported as a return value alternative to DeferredResult where an underlying service (or perhaps a call to AsyncRestTemplate) already returns ListenableFuture.
- @ModelAttribute methods are now invoked in an order that respects inter-dependencies. See SPR-6299.
- Jackson’s @JsonView is supported directly on @ResponseBody and ResponseEntity controller methods for serializing different amounts of detail for the same POJO (e.g. summary vs. detail page). This is also supported with View-based rendering by adding the serialization view type as a model attribute under a special key. See the section called “Jackson Serialization View Support” for details.
- JSONP is now supported with Jackson. See the section called “Jackson JSONP Support”.
- A new lifecycle option is available for intercepting @ResponseBody and ResponseEntity methods just after the controller method returns and before the response is written. To take advantage declare an @ControllerAdvice bean that implements ResponseBodyAdvice. The built-in support for @JsonView and JSONP take advantage of this. See Section 21.4.1, “Intercepting requests with a HandlerInterceptor”.
- There are three new HttpMessageConverter options:
    - Gson — lighter footprint than Jackson; has already been in use in Spring Android.
    - Google Protocol Buffers — efficient and effective as an inter-service communication data protocol within an enterprise but can also be exposed as JSON and XML for browsers.
    - Jackson based XML serialization is now supported through the jackson-dataformat-xml extension. When using @EnableWebMvc or <mvc:annotation-driven/>, this is used by default instead of JAXB2 if jackson-dataformat-xml is in the classpath.
- Views such as JSPs can now build links to controllers by referring to controller mappings by name. A default name is assigned to every @RequestMapping. For example FooController with method handleFoo is named "FC#handleFoo". The naming strategy is pluggable. It is also possible to name an @RequestMapping explicitly through its name attribute. A new mvcUrl function in the Spring JSP tag library makes this easy to use in JSP pages. See Section 21.7.2, “Building URIs to Controllers and methods from views”.
- ResponseEntity provides a builder-style API to guide controller methods towards the preparation of server-side responses, e.g. ResponseEntity.ok().
- RequestEntity is a new type that provides a builder-style API to guide client-side REST code towards the preparation of HTTP requests.
- MVC Java config and XML namespace:
    - View resolvers can now be configured including support for content negotiation, see Section 21.16.8, “View Resolvers”.
    - View controllers now have built-in support for redirects and for setting the response status. An application can use this to configure redirect URLs, render 404 responses with a view, send "no content" responses, etc. Some use cases are listed here.
    - Path matching customizations are frequently used and now built-in. See Section 21.16.11, “Path Matching”.
- Groovy markup template support (based on Groovy 2.3). See the GroovyMarkupConfigurer and respecitve ViewResolver and `View' implementations.

4.4 WebSocket Messaging Improvements

- SockJS (Java) client-side support. See SockJsClient and classes in same package.
- New application context events SessionSubscribeEvent and SessionUnsubscribeEvent published when STOMP clients subscribe and unsubscribe.
- New "websocket" scope. See Section 25.4.14, “WebSocket Scope”.
- @SendToUser can target only a single session and does not require an authenticated user.
- @MessageMapping methods can use dot "." instead of slash "/" as path separator. See SPR-11660.
- STOMP/WebSocket monitoring info collected and logged. See Section 25.4.16, “Runtime Monitoring”.
- Significantly optimized and improved logging that should remain very readable and compact even at DEBUG level.
- Optimized message creation including support for temporary message mutability and avoiding automatic message id and timestamp creation. See Javadoc of MessageHeaderAccessor.
- Close STOMP/WebSocket connections that have no activity within 60 seconds after the WebSocket session is established. See SPR-11884.

4.5 Testing Improvements

- Groovy scripts can now be used to configure the ApplicationContext loaded for integration tests in the TestContext framework.
    - See the section called “Context configuration with Groovy scripts” for details.
- Test-managed transactions can now be programmatically started and ended within transactional test methods via the new TestTransaction API.
    - See the section called “Programmatic transaction management” for details.
- SQL script execution can now be configured declaratively via the new @Sql and @SqlConfig annotations on a per-class or per-method basis.
    - See Section 14.5.7, “Executing SQL scripts” for details.
- Test property sources which automatically override system and application property sources can be configured via the new @TestPropertySource annotation.
    - See the section called “Context configuration with test property sources” for details.
- Default TestExecutionListeners can now be automatically discovered.
    - See the section called “Automatic discovery of default TestExecutionListeners” for details.
- Custom TestExecutionListeners can now be automatically merged with the default listeners.
    - See the section called “Merging TestExecutionListeners” for details.
- The documentation for transactional testing support in the TestContext framework has been improved with more thorough explanations and additional examples.
    - See Section 14.5.6, “Transaction management” for details.
- Various improvements to MockServletContext, MockHttpServletRequest, and other Servlet API mocks.
- AssertThrows has been refactored to support Throwable instead of Exception.
- In Spring MVC Test, JSON responses can be asserted with JSON Assert as an extra option to using JSONPath much like it has been possible to do for XML with XMLUnit.
- MockMvcBuilder recipes can now be created with the help of MockMvcConfigurer. This was added to make it easy to apply Spring Security setup but can be used to encapsulate common setup for any 3rd party framework or within a project.
- MockRestServiceServer now supports the AsyncRestTemplate for client-side testing.

5. New Features and Enhancements in Spring Framework 4.2

5.1 Core Container Improvements

- Annotations such as @Bean get detected and processed on Java 8 default methods as well, allowing for composing a configuration class from interfaces with default @Bean methods.
- Configuration classes may declare @Import with regular component classes now, allowing for a mix of imported configuration classes and component classes.
- Configuration classes may declare an @Order value, getting processed in a corresponding order (e.g. for overriding beans by name) even when detected through classpath scanning.
- @Resource injection points support an @Lazy declaration, analogous to @Autowired, receiving a lazy-initializing proxy for the requested target bean.
- The application event infrastructure now offers an annotation-based model as well as the ability to publish any arbitrary event.
    - Any public method in a managed bean can be annotated with @EventListener to consume events.
    - @TransactionalEventListener provides transaction-bound event support.
- Spring Framework 4.2 introduces first-class support for declaring and looking up aliases for annotation attributes. The new @AliasFor annotation can be used to declare a pair of aliased attributes within a single annotation or to declare an alias from one attribute in a custom composed annotation to an attribute in a meta-annotation.
    - The following annotations have been retrofitted with @AliasFor support in order to provide meaningful aliases for their value attributes: @Cacheable, @CacheEvict, @CachePut, @ComponentScan, @ComponentScan.Filter, @ImportResource, @Scope, @ManagedResource, @Header, @Payload, @SendToUser, @ActiveProfiles, @ContextConfiguration, @Sql, @TestExecutionListeners, @TestPropertySource, @Transactional, @ControllerAdvice, @CookieValue, @CrossOrigin, @MatrixVariable, @RequestHeader, @RequestMapping, @RequestParam, @RequestPart, @ResponseStatus, @SessionAttributes, @ActionMapping, @RenderMapping, @EventListener, @TransactionalEventListener.
    - For example, @ContextConfiguration from the spring-test module is now declared as follows:

```java
public @interface ContextConfiguration {

    @AliasFor("locations")
    String[] value() default {};

    @AliasFor("value")
    String[] locations() default {};

    // ...
}
```
    - Similarly, composed annotations that override attributes from meta-annotations can now use @AliasFor for fine-grained control over exactly which attributes are overridden within an annotation hierarchy. In fact, it is now possible to declare an alias for the value attribute of a meta-annotation.
    - For example, one can now develop a composed annotation with a custom attribute override as follows.

```java
@ContextConfiguration
public @interface MyTestConfig {

    @AliasFor(annotation = ContextConfiguration.class, attribute = "value")
    String[] xmlFiles();

    // ...
}
```
    - See Spring Annotation Programming Model.

- Numerous improvements to Spring’s search algorithms used for finding meta-annotations. For example, locally declared composed annotations are now favored over inherited annotations.
- Composed annotations that override attributes from meta-annotations can now be discovered on interfaces and on abstract, bridge, & interface methods as well as on classes, standard methods, constructors, and fields.
- Maps representing annotation attributes (and AnnotationAttributes instances) can be synthesized (i.e., converted) into an annotation.
- The features of field-based data binding (DirectFieldAccessor) have been aligned with the current property-based data binding (BeanWrapper). In particular, field-based binding now supports navigation for Collections, Arrays, and Maps.
- DefaultConversionService now provides out-of-the-box converters for Stream, Charset, Currency, and TimeZone. Such converters can be added individually to any arbitrary ConversionService as well.
- DefaultFormattingConversionService comes with out-of-the-box support for the value types in JSR-354 Money & Currency (if the 'javax.money' API is present on the classpath): namely, MonetaryAmount and CurrencyUnit. This includes support for applying @NumberFormat.
- @NumberFormat can now be used as a meta-annotation.
- JavaMailSenderImpl has a new testConnection() method for checking connectivity to the server.
- ScheduledTaskRegistrar exposes scheduled tasks.
- Apache commons-pool2 is now supported for a pooling AOP CommonsPool2TargetSource.
- Introduced StandardScriptFactory as a JSR-223 based mechanism for scripted beans, exposed through the lang:std element in XML. Supports e.g. JavaScript and JRuby. (Note: JRubyScriptFactory and lang:jruby are deprecated now, in favor of using JSR-223.)


5.2 Data Access Improvements
- javax.transaction.Transactional is now supported via AspectJ.
- SimpleJdbcCallOperations now supports named binding.
- Full support for Hibernate ORM 5.0: as a JPA provider (automatically adapted) as well as through its native API (covered by the new org.springframework.orm.hibernate5 package).
- Embedded databases can now be automatically assigned unique names, and <jdbc:embedded-database> supports a new database-name attribute. See "Testing Improvements" below for further details.

5.3 JMS Improvements
- The autoStartup attribute can be controlled via JmsListenerContainerFactory.
- The type of the reply Destination can now be configured per listener container.
- The value of the @SendTo annotation can now use a SpEL expression.
- The response destination can be computed at runtime using JmsResponse
- @JmsListener is now a repeatable annotation to declare several JMS containers on the same method (use the newly introduced @JmsListeners if you’re not using Java8 yet).

5.4 Web Improvements
- HTTP Streaming and Server-Sent Events support, see the section called “HTTP Streaming”.
- Built-in support for CORS including global (MVC Java config and XML namespace) and local (e.g. @CrossOrigin) configuration. See Chapter 26, CORS Support for details.
- HTTP caching updates:
    - new CacheControl builder; plugged into ResponseEntity, WebContentGenerator, ResourceHttpRequestHandler.
    - improved ETag/Last-Modified support in WebRequest.
- Custom mapping annotations, using @RequestMapping as a meta-annotation.
- Public methods in AbstractHandlerMethodMapping to register and unregister request mappings at runtime.
- Protected createDispatcherServlet method in AbstractDispatcherServletInitializer to further customize the DispatcherServlet instance to use.
- HandlerMethod as a method argument on @ExceptionHandler methods, especially handy in @ControllerAdvice components.
- java.util.concurrent.CompletableFuture as an @Controller method return value type.
- Byte-range request support in HttpHeaders and for serving static resources.
- @ResponseStatus detected on nested exceptions.
- UriTemplateHandler extension point in the RestTemplate.
    - DefaultUriTemplateHandler exposes baseUrl property and path segment encoding options.
    - the extension point can also be used to plug in any URI template library.
- OkHTTP integration with the RestTemplate.
- Custom baseUrl alternative for methods in MvcUriComponentsBuilder.
- Serialization/deserialization exception messages are now logged at WARN level.
- Default JSON prefix has been changed from "{} && " to the safer ")]}', " one.
- New RequestBodyAdvice extension point and built-in implementation to support Jackson’s @JsonView on @RequestBody method arguments.
- When using GSON or Jackson 2.6+, the handler method return type is used to improve serialization of parameterized types like List<Foo>.
- Introduced ScriptTemplateView as a JSR-223 based mechanism for scripted web views, with a focus on JavaScript view templating on Nashorn (JDK 8).

5.5 WebSocket Messaging Improvements
- Expose presence information about connected users and subscriptions:
    - new SimpUserRegistry exposed as a bean named "userRegistry".
    - sharing of presence information across cluster of servers (see broker relay config options).
- Resolve user destinations across cluster of servers (see broker relay config options).
- StompSubProtocolErrorHandler extension point to customize and control STOMP ERROR frames to clients.
- Global @MessageExceptionHandler methods via @ControllerAdvice components.
- Heart-beats and a SpEL expression 'selector' header for subscriptions with SimpleBrokerMessageHandler.
- STOMP client for use over TCP and WebSocket; see Section 25.4.13, “STOMP Client”.
- @SendTo and @SendToUser can contain destination variable placeholders.
- Jackson’s @JsonView supported for return values on @MessageMapping and @SubscribeMapping methods.
- ListenableFuture and CompletableFuture as return value types from @MessageMapping and @SubscribeMapping methods.
- MarshallingMessageConverter for XML payloads.

5.6 Testing Improvements
- JUnit-based integration tests can now be executed with JUnit rules instead of the SpringJUnit4ClassRunner. This allows Spring-based integration tests to be run with alternative runners like JUnit’s Parameterized or third-party runners such as the MockitoJUnitRunner.
    - See the section called “Spring JUnit Rules” for details.
- The Spring MVC Test framework now provides first-class support for HtmlUnit, including integration with Selenium’s WebDriver, allowing for page-based web application testing without the need to deploy to a Servlet container.
    - See Section 14.6.2, “HtmlUnit Integration” for details.
- AopTestUtils is a new testing utility that allows developers to obtain a reference to the underlying target object hidden behind one or more Spring proxies.
    - See Section 13.2.1, “General testing utilities” for details.
- ReflectionTestUtils now supports setting and getting static fields, including constants.
- The original ordering of bean definition profiles declared via @ActiveProfiles is now retained in order to support use cases such as Spring Boot’s ConfigFileApplicationListener which loads configuration files based on the names of active profiles.
- @DirtiesContext supports new BEFORE_METHOD, BEFORE_CLASS, and BEFORE_EACH_TEST_METHOD modes for closing the ApplicationContext before a test — for example, if some rogue (i.e., yet to be determined) test within a large test suite has corrupted the original configuration for the ApplicationContext.
- @Commit is a new annotation that may be used as a direct replacement for @Rollback(false).
- @Rollback may now be used to configure class-level default rollback semantics.
    - Consequently, @TransactionConfiguration is now deprecated and will be removed in a subsequent release.
- @Sql now supports execution of inlined SQL statements via a new statements attribute.
- The ContextCache that is used for caching ApplicationContexts between tests is now a public API with a default implementation that can be replaced for custom caching needs.
- DefaultTestContext, DefaultBootstrapContext, and DefaultCacheAwareContextLoaderDelegate are now public classes in the support subpackage, allowing for custom extensions.
- TestContextBootstrappers are now responsible for building the TestContext.
- In the Spring MVC Test framework, MvcResult details can now be logged at DEBUG level or written to a custom OutputStream or Writer. See the new log(), print(OutputStream), and print(Writer) methods in MockMvcResultHandlers for details.
- The JDBC XML namespace supports a new database-name attribute in <jdbc:embedded-database>, allowing developers to set unique names for embedded databases –- for example, via a SpEL expression or a property placeholder that is influenced by the current active bean definition profiles.
- Embedded databases can now be automatically assigned a unique name, allowing common test database configuration to be reused in different ApplicationContexts within a test suite.
    - See Section 18.8.6, “Generating unique names for embedded databases” for details.
- MockHttpServletRequest and MockHttpServletResponse now provide better support for date header formatting via the getDateHeader and setDateHeader methods.

Part III. 核心技术

This part of the reference documentation covers all of those technologies that are absolutely integral to the Spring Framework.

Foremost amongst these is the Spring Framework’s Inversion of Control (IoC) container. A thorough treatment of the Spring Framework’s IoC container is closely followed by comprehensive coverage of Spring’s Aspect-Oriented Programming (AOP) technologies. The Spring Framework has its own AOP framework, which is conceptually easy to understand, and which successfully addresses the 80% sweet spot of AOP requirements in Java enterprise programming.

Coverage of Spring’s integration with AspectJ (currently the richest - in terms of features - and certainly most mature AOP implementation in the Java enterprise space) is also provided.

- Chapter 6, The IoC container
- Chapter 7, Resources
- Chapter 8, Validation, Data Binding, and Type Conversion
- Chapter 9, Spring Expression Language (SpEL)
- Chapter 10, Aspect Oriented Programming with Spring
- Chapter 11, Spring AOP APIs

#### 6. IoC 容器

#### 6.1 介绍Spring IoC容器和beans

本章节覆盖了Spring框架的控制反转(IoC)实现原理。IoC也被称作依赖注入(DI)。
It is a process whereby objects define their dependencies, that is, the other objects they work with, only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method.
当创建bean的时候容器注入bean的那些依赖。这个过程从根本上进行了反转,于是有了控制反转这个名字(IoC),of the bean itself controlling the instantiation or location of its dependencies by using direct construction of classes, or a mechanism such as the Service Locator pattern.

org.springframework.beans包和org.springframework.context包是Spring框架的基本Io容器。BeanFactory接口提供了能管理任何类型对象的高级配置机制。ApplicationContext是BeanFactory的一个子接口。它增加了更容易集成Spring AOP功能;消息资源管理(用于国际化),事件发布;和应用层特殊的上下文,例如在web应用中使用的WebApplicationContext。

简而言之,BeanFactory提供了Spring配置框架的基本功能,而ApplicationContext增加了更多的企业级应用功能。ApplicationContext是BeanFactory的一个完全超集,and is used exclusively in this chapter in descriptions of Spring’s IoC container.如果要用BeanFactory来代替ApplicationContext更新信息可以参考章节6.16"The BeanFactory"。

在Spring中构建应用程序的对象是由Spring IoC容器进行管理的,这些对象称作beans。一个bean就是一个对新,这个对新的创建,组装,和其它的生命周期都是由Spring IoC容器管理的。否则,bean就是应用程序中的众多对象中的一个。Beans,和他们之间的依赖,是有容器来来配置管理的。

#### 6.2 容器概述

org.springframework.context.ApplicationContext表示Spring IoC容器,来负责初始化,配置,和组装定义好的beans。容器通过读取配置信息来获取哪些bean需要实例化,配置,和组装。配置可以采用XML的方式,Java annotations方式,或者Java编码方式。It allows you to express the objects that compose your application and the rich interdependencies between such objects.

ApplicationContext接口的一些实现使用Spring开箱的支持。在独立的应用程序中,通常是来创建ClassPathXmlApplicationContext或FileSystemXmlApplicationContext的实例。XML是定义配置元数据的传统格式,你可以指示容器使用Java的注解或是代码作为元数据的格式,提供少量的XML配置声明来开启对这些额外的元数据格式的支持。

在大多数的应用场景中,用户并不需要自己明确的自己编码去获取一个Spring IoC容器实例。例如,一个web应用场景中,在web应用程序的web.xml配置文件中简单的八行左右的样板J2EE描述符XML文件通常就够了(参考6.15.4节“便捷的对Web应用程序应用上下文进行实例化”)。如果你正使用Spring的工具套件，Eclipse支持的开发环境样板配置，就可以容易地被创建，点几下鼠标或按键就可以了。

下文从更高角度来说明Spring是如何工作的。你的应用程序类和配置元数据相组合，所以在ApplicationContext被创建和实例化后，就得到了一个完全配置的可执行系统或程序。


**图Spring IoC容器**

![pic](https://github.com/chlsmile/blogfile/blob/master/blogfile/container-magic.png)


#### 6.2.1 配置元数据 metadata

如上图所示,Spring的IoC容器处理配置元数据的一种形式;这个配置元数据代表了应用开发人员是如何告诉Spring容器在你的应用程序中来实例化,配置并装配对象的。

配置元数据传统上是以直观的XML格式提供的，本章的大部分内容使用它来阐述Spring IoC容器关键概念和功能。

> **注意** 基于XML的元数据并不是唯一的配置元数据方式。这种配置元数据真正写入时,Spring的IoC容器本身和这种配置完全是解耦的。



XML-based metadata is not the only allowed form of configuration metadata.
The Spring IoC container itself is totally decoupled from the format in which this configuration metadata is actually written.
These days many developers choose Java-based configuration for their Spring applications.

For information about using other forms of metadata with the Spring container, see:

- Annotation-based configuration: Spring 2.5 introduced support for annotation-based configuration metadata.
- Java-based configuration: Starting with Spring 3.0, many features provided by the Spring JavaConfig project became part of the core Spring Framework. Thus you can define beans external to your application classes by using Java rather than XML files. To use these new features, see the @Configuration, @Bean, @Import and @DependsOn annotations.

Spring configuration consists of at least one and typically more than one bean definition that the container must manage.
XML-based configuration metadata shows these beans configured as <bean/> elements inside a top-level <beans/> element.
Java configuration typically uses @Bean annotated methods within a @Configuration class.

These bean definitions correspond to the actual objects that make up your application.
Typically you define service layer objects, data access objects (DAOs), presentation objects such as Struts Action instances, infrastructure objects such as Hibernate SessionFactories, JMS Queues, and so forth.
Typically one does not configure fine-grained domain objects in the container, because it is usually the responsibility of DAOs and business logic to create and load domain objects.
However, you can use Spring’s integration with AspectJ to configure objects that have been created outside the control of an IoC container.
See Using AspectJ to dependency-inject domain objects with Spring.

The following example shows the basic structure of XML-based configuration metadata:

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="..." class="...">
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <bean id="..." class="...">
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions go here -->

</beans>
```
The id attribute is a string that you use to identify the individual bean definition. The class attribute defines the type of the bean and uses the fully qualified classname. The value of the id attribute refers to collaborating objects. The XML for referring to collaborating objects is not shown in this example; see Dependencies for more information.

6.2.2 Instantiating a container
Instantiating a Spring IoC container is straightforward. The location path or paths supplied to an ApplicationContext constructor are actually resource strings that allow the container to load configuration metadata from a variety of external resources such as the local file system, from the Java CLASSPATH, and so on.

```java
ApplicationContext context=new ClassPathXmlApplicationContext(new String[] {"services.xml", "daos.xml"});
```
[Note]
After you learn about Spring’s IoC container, you may want to know more about Spring’s Resource abstraction, as described in Chapter 7, Resources, which provides a convenient mechanism for reading an InputStream from locations defined in a URI syntax. In particular, Resource paths are used to construct applications contexts as described in Section 7.7, “Application contexts and Resource paths”.

The following example shows the service layer objects (services.xml) configuration file:

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- services -->

    <bean id="petStore" class="org.springframework.samples.jpetstore.services.PetStoreServiceImpl">
        <property name="accountDao" ref="accountDao"/>
        <property name="itemDao" ref="itemDao"/>
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions for services go here -->

</beans>
```

The following example shows the data access objects daos.xml file:
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="accountDao"
        class="org.springframework.samples.jpetstore.dao.jpa.JpaAccountDao">
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <bean id="itemDao" class="org.springframework.samples.jpetstore.dao.jpa.JpaItemDao">
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions for data access objects go here -->

</beans>
```
In the preceding example, the service layer consists of the class PetStoreServiceImpl, and two data access objects of the type JpaAccountDao and JpaItemDao (based on the JPA Object/Relational mapping standard). The property name element refers to the name of the JavaBean property, and the ref element refers to the name of another bean definition. This linkage between id and ref elements expresses the dependency between collaborating objects. For details of configuring an object’s dependencies, see Dependencies.

Composing XML-based configuration metadata

It can be useful to have bean definitions span multiple XML files. Often each individual XML configuration file represents a logical layer or module in your architecture.

You can use the application context constructor to load bean definitions from all these XML fragments. This constructor takes multiple Resource locations, as was shown in the previous section. Alternatively, use one or more occurrences of the <import/> element to load bean definitions from another file or files. For example:
```java
<beans>
    <import resource="services.xml"/>
    <import resource="resources/messageSource.xml"/>
    <import resource="/resources/themeSource.xml"/>

    <bean id="bean1" class="..."/>
    <bean id="bean2" class="..."/>
</beans>
```
In the preceding example, external bean definitions are loaded from three files: services.xml, messageSource.xml, and themeSource.xml. All location paths are relative to the definition file doing the importing, so services.xml must be in the same directory or classpath location as the file doing the importing, while messageSource.xml and themeSource.xml must be in a resources location below the location of the importing file. As you can see, a leading slash is ignored, but given that these paths are relative, it is better form not to use the slash at all. The contents of the files being imported, including the top level <beans/> element, must be valid XML bean definitions according to the Spring Schema.

[Note]
It is possible, but not recommended, to reference files in parent directories using a relative "../" path. Doing so creates a dependency on a file that is outside the current application. In particular, this reference is not recommended for "classpath:" URLs (for example, "classpath:../services.xml"), where the runtime resolution process chooses the "nearest" classpath root and then looks into its parent directory. Classpath configuration changes may lead to the choice of a different, incorrect directory.
You can always use fully qualified resource locations instead of relative paths: for example, "file:C:/config/services.xml" or "classpath:/config/services.xml". However, be aware that you are coupling your application’s configuration to specific absolute locations. It is generally preferable to keep an indirection for such absolute locations, for example, through "${…​}" placeholders that are resolved against JVM system properties at runtime.

6.2.3 Using the container

The ApplicationContext is the interface for an advanced factory capable of maintaining a registry of different beans and their dependencies. Using the method T getBean(String name, Class<T> requiredType) you can retrieve instances of your beans.

The ApplicationContext enables you to read bean definitions and access them as follows:

```java
// create and configure beans
ApplicationContext context =
    new ClassPathXmlApplicationContext(new String[] {"services.xml", "daos.xml"});

// retrieve configured instance
PetStoreService service = context.getBean("petStore", PetStoreService.class);

// use configured instance
List<String> userList = service.getUsernameList();

```
You use getBean() to retrieve instances of your beans. The ApplicationContext interface has a few other methods for retrieving beans, but ideally your application code should never use them. Indeed, your application code should have no calls to the getBean() method at all, and thus no dependency on Spring APIs at all. For example, Spring’s integration with web frameworks provides for dependency injection for various web framework classes such as controllers and JSF-managed beans.

6.3 Bean overview

A Spring IoC container manages one or more beans. These beans are created with the configuration metadata that you supply to the container, for example, in the form of XML <bean/> definitions.
Within the container itself, these bean definitions are represented as BeanDefinition objects, which contain (among other information) the following metadata:
- A package-qualified class name: typically the actual implementation class of the bean being defined.
- Bean behavioral configuration elements, which state how the bean should behave in the container (scope, lifecycle callbacks, and so forth).
- References to other beans that are needed for the bean to do its work; these references are also called collaborators or dependencies.
- Other configuration settings to set in the newly created object, for example, the number of connections to use in a bean that manages a connection pool, or the size limit of the pool.

This metadata translates to a set of properties that make up each bean definition.

Table 6.1. The bean definition

Property | Explained in…​
------------ | -------------
class | Section 6.3.2, “Instantiating beans”
name | Section 6.3.1, “Naming beans”
scope | Section 6.5, “Bean scopes”
constructor arguments | Section 6.4.1, “Dependency Injection”
properties | Section 6.4.1, “Dependency Injection”
autowiring mode | Section 6.4.5, “Autowiring collaborators”
lazy-initialization mode | Section 6.4.4, “Lazy-initialized beans”
initialization method | the section called “Initialization callbacks”
destruction method | the section called “Destruction callbacks”

In addition to bean definitions that contain information on how to create a specific bean, the ApplicationContext implementations also permit the registration of existing objects that are created outside the container, by users. This is done by accessing the ApplicationContext’s BeanFactory via the method getBeanFactory() which returns the BeanFactory implementation DefaultListableBeanFactory. DefaultListableBeanFactory supports this registration through the methods registerSingleton(..) and registerBeanDefinition(..). However, typical applications work solely with beans defined through metadata bean definitions.

[Note]
Bean metadata and manually supplied singleton instances need to be registered as early as possible, in order for the container to properly reason about them during autowiring and other introspection steps. While overriding of existing metadata and existing singleton instances is supported to some degree, the registration of new beans at runtime (concurrently with live access to factory) is not officially supported and may lead to concurrent access exceptions and/or inconsistent state in the bean container.


6.3.1 Naming beans

Every bean has one or more identifiers. These identifiers must be unique within the container that hosts the bean. A bean usually has only one identifier, but if it requires more than one, the extra ones can be considered aliases.

In XML-based configuration metadata, you use the id and/or name attributes to specify the bean identifier(s). The id attribute allows you to specify exactly one id. Conventionally these names are alphanumeric ('myBean', 'fooService', etc.), but may contain special characters as well. If you want to introduce other aliases to the bean, you can also specify them in the name attribute, separated by a comma (,), semicolon (;), or white space. As a historical note, in versions prior to Spring 3.1, the id attribute was defined as an xsd:ID type, which constrained possible characters. As of 3.1, it is defined as an xsd:string type. Note that bean id uniqueness is still enforced by the container, though no longer by XML parsers.

You are not required to supply a name or id for a bean. If no name or id is supplied explicitly, the container generates a unique name for that bean. However, if you want to refer to that bean by name, through the use of the ref element or Service Locator style lookup, you must provide a name. Motivations for not supplying a name are related to using inner beans and autowiring collaborators.
> Bean Naming Conventions

  The convention is to use the standard Java convention for instance field names when naming beans. That is, bean names start with a lowercase letter, and are camel-cased from then on. Examples of such names would be (without quotes) 'accountManager', 'accountService', 'userDao', 'loginController', and so forth.

  Naming beans consistently makes your configuration easier to read and understand, and if you are using Spring AOP it helps a lot when applying advice to a set of beans related by name.

Aliasing a bean outside the bean definition

In a bean definition itself, you can supply more than one name for the bean, by using a combination of up to one name specified by the id attribute, and any number of other names in the name attribute. These names can be equivalent aliases to the same bean, and are useful for some situations, such as allowing each component in an application to refer to a common dependency by using a bean name that is specific to that component itself.

Specifying all aliases where the bean is actually defined is not always adequate, however. It is sometimes desirable to introduce an alias for a bean that is defined elsewhere. This is commonly the case in large systems where configuration is split amongst each subsystem, each subsystem having its own set of object definitions. In XML-based configuration metadata, you can use the <alias/> element to accomplish this.

```java
<alias name="fromName" alias="toName"/>
```
In this case, a bean in the same container which is named fromName, may also, after the use of this alias definition, be referred to as toName.

For example, the configuration metadata for subsystem A may refer to a DataSource via the name subsystemA-dataSource. The configuration metadata for subsystem B may refer to a DataSource via the name subsystemB-dataSource. When composing the main application that uses both these subsystems the main application refers to the DataSource via the name myApp-dataSource. To have all three names refer to the same object you add to the MyApp configuration metadata the following aliases definitions:
```java
<alias name="subsystemA-dataSource" alias="subsystemB-dataSource"/>
<alias name="subsystemA-dataSource" alias="myApp-dataSource" />
```

Now each component and the main application can refer to the dataSource through a name that is unique and guaranteed not to clash with any other definition (effectively creating a namespace), yet they refer to the same bean.

```java
Java-configuration

If you are using Java-configuration, the @Bean annotation can be used to provide aliases see Section 6.12.3, “Using the @Bean annotation” for details.
```

6.3.2 Instantiating beans

A bean definition essentially is a recipe for creating one or more objects. The container looks at the recipe for a named bean when asked, and uses the configuration metadata encapsulated by that bean definition to create (or acquire) an actual object.

If you use XML-based configuration metadata, you specify the type (or class) of object that is to be instantiated in the class attribute of the <bean/> element. This class attribute, which internally is a Class property on a BeanDefinition instance, is usually mandatory. (For exceptions, see the section called “Instantiation using an instance factory method” and Section 6.7, “Bean definition inheritance”.) You use the Class property in one of two ways:

- Typically, to specify the bean class to be constructed in the case where the container itself directly creates the bean by calling its constructor reflectively, somewhat equivalent to Java code using the new operator.
- To specify the actual class containing the static factory method that will be invoked to create the object, in the less common case where the container invokes a static factory method on a class to create the bean. The object type returned from the invocation of the static factory method may be the same class or another class entirely.

```java
Inner class names.  If you want to configure a bean definition for a static nested class, you have to use the binary name of the nested class.

For example, if you have a class called Foo in the com.example package, and this Foo class has a static nested class called Bar, the value of the 'class' attribute on a bean definition would be…​

com.example.Foo$Bar

Notice the use of the $ character in the name to separate the nested class name from the outer class name.
```

Instantiation with a constructor

When you create a bean by the constructor approach, all normal classes are usable by and compatible with Spring. That is, the class being developed does not need to implement any specific interfaces or to be coded in a specific fashion. Simply specifying the bean class should suffice. However, depending on what type of IoC you use for that specific bean, you may need a default (empty) constructor.

The Spring IoC container can manage virtually any class you want it to manage; it is not limited to managing true JavaBeans. Most Spring users prefer actual JavaBeans with only a default (no-argument) constructor and appropriate setters and getters modeled after the properties in the container. You can also have more exotic non-bean-style classes in your container. If, for example, you need to use a legacy connection pool that absolutely does not adhere to the JavaBean specification, Spring can manage it as well.

With XML-based configuration metadata you can specify your bean class as follows:

```java
<bean id="exampleBean" class="examples.ExampleBean"/>

<bean name="anotherExample" class="examples.ExampleBeanTwo"/>
```
For details about the mechanism for supplying arguments to the constructor (if required) and setting object instance properties after the object is constructed, see Injecting Dependencies.

Instantiation with a static factory method

When defining a bean that you create with a static factory method, you use the class attribute to specify the class containing the static factory method and an attribute named factory-method to specify the name of the factory method itself. You should be able to call this method (with optional arguments as described later) and return a live object, which subsequently is treated as if it had been created through a constructor. One use for such a bean definition is to call static factories in legacy code.

The following bean definition specifies that the bean will be created by calling a factory-method. The definition does not specify the type (class) of the returned object, only the class containing the factory method. In this example, the createInstance() method must be a static method.

```java
<bean id="clientService"
    class="examples.ClientService"
    factory-method="createInstance"/>
```
```java
public class ClientService {
    private static ClientService clientService = new ClientService();
    private ClientService() {}

    public static ClientService createInstance() {
        return clientService;
    }
}
```

For details about the mechanism for supplying (optional) arguments to the factory method and setting object instance properties after the object is returned from the factory, see Dependencies and configuration in detail.

Instantiation using an instance factory method

Similar to instantiation through a static factory method, instantiation with an instance factory method invokes a non-static method of an existing bean from the container to create a new bean. To use this mechanism, leave the class attribute empty, and in the factory-bean attribute, specify the name of a bean in the current (or parent/ancestor) container that contains the instance method that is to be invoked to create the object. Set the name of the factory method itself with the factory-method attribute.

```java
<!-- the factory bean, which contains a method called createInstance() -->
<bean id="serviceLocator" class="examples.DefaultServiceLocator">
    <!-- inject any dependencies required by this locator bean -->
</bean>

<!-- the bean to be created via the factory bean -->
<bean id="clientService"
    factory-bean="serviceLocator"
    factory-method="createClientServiceInstance"/>

```
```java
public class DefaultServiceLocator {

    private static ClientService clientService = new ClientServiceImpl();
    private DefaultServiceLocator() {}

    public ClientService createClientServiceInstance() {
        return clientService;
    }
}
```

One factory class can also hold more than one factory method as shown here:

```java
<bean id="serviceLocator" class="examples.DefaultServiceLocator">
    <!-- inject any dependencies required by this locator bean -->
</bean>

<bean id="clientService"
    factory-bean="serviceLocator"
    factory-method="createClientServiceInstance"/>

<bean id="accountService"
    factory-bean="serviceLocator"
    factory-method="createAccountServiceInstance"/>
```
```java
public class DefaultServiceLocator {

    private static ClientService clientService = new ClientServiceImpl();
    private static AccountService accountService = new AccountServiceImpl();

    private DefaultServiceLocator() {}

    public ClientService createClientServiceInstance() {
        return clientService;
    }

    public AccountService createAccountServiceInstance() {
        return accountService;
    }

}
```

This approach shows that the factory bean itself can be managed and configured through dependency injection (DI). See Dependencies and configuration in detail.

[Note]
In Spring documentation, factory bean refers to a bean that is configured in the Spring container that will create objects through an instance or static factory method. By contrast, FactoryBean (notice the capitalization) refers to a Spring-specific FactoryBean.

6.4 Dependencies
A typical enterprise application does not consist of a single object (or bean in the Spring parlance). Even the simplest application has a few objects that work together to present what the end-user sees as a coherent application. This next section explains how you go from defining a number of bean definitions that stand alone to a fully realized application where objects collaborate to achieve a goal.

6.4.1 Dependency Injection

Dependency injection (DI) is a process whereby objects define their dependencies, that is, the other objects they work with, only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method. The container then injects those dependencies when it creates the bean. This process is fundamentally the inverse, hence the name Inversion of Control (IoC), of the bean itself controlling the instantiation or location of its dependencies on its own by using direct construction of classes, or the Service Locator pattern.

Code is cleaner with the DI principle and decoupling is more effective when objects are provided with their dependencies. The object does not look up its dependencies, and does not know the location or class of the dependencies. As such, your classes become easier to test, in particular when the dependencies are on interfaces or abstract base classes, which allow for stub or mock implementations to be used in unit tests.

DI exists in two major variants, Constructor-based dependency injection and Setter-based dependency injection.

Constructor-based dependency injection

Constructor-based DI is accomplished by the container invoking a constructor with a number of arguments, each representing a dependency. Calling a static factory method with specific arguments to construct the bean is nearly equivalent, and this discussion treats arguments to a constructor and to a static factory method similarly. The following example shows a class that can only be dependency-injected with constructor injection. Notice that there is nothing special about this class, it is a POJO that has no dependencies on container specific interfaces, base classes or annotations.

```java
public class SimpleMovieLister {

    // the SimpleMovieLister has a dependency on a MovieFinder
    private MovieFinder movieFinder;

    // a constructor so that the Spring container can inject a MovieFinder
    public SimpleMovieLister(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // business logic that actually uses the injected MovieFinder is omitted...

}
```

Constructor argument resolution

Constructor argument resolution matching occurs using the argument’s type. If no potential ambiguity exists in the constructor arguments of a bean definition, then the order in which the constructor arguments are defined in a bean definition is the order in which those arguments are supplied to the appropriate constructor when the bean is being instantiated. Consider the following class:

```java
package x.y;

public class Foo {

    public Foo(Bar bar, Baz baz) {
        // ...
    }

}
```
No potential ambiguity exists, assuming that Bar and Baz classes are not related by inheritance. Thus the following configuration works fine, and you do not need to specify the constructor argument indexes and/or types explicitly in the <constructor-arg/> element.
```java
<beans>
    <bean id="foo" class="x.y.Foo">
        <constructor-arg ref="bar"/>
        <constructor-arg ref="baz"/>
    </bean>

    <bean id="bar" class="x.y.Bar"/>

    <bean id="baz" class="x.y.Baz"/>
</beans>
```
When another bean is referenced, the type is known, and matching can occur (as was the case with the preceding example). When a simple type is used, such as <value>true</value>, Spring cannot determine the type of the value, and so cannot match by type without help. Consider the following class:
```java
package examples;

public class ExampleBean {

    // Number of years to calculate the Ultimate Answer
    private int years;

    // The Answer to Life, the Universe, and Everything
    private String ultimateAnswer;

    public ExampleBean(int years, String ultimateAnswer) {
        this.years = years;
        this.ultimateAnswer = ultimateAnswer;
    }

}
```
In the preceding scenario, the container can use type matching with simple types if you explicitly specify the type of the constructor argument using the type attribute. For example:
```java
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg type="int" value="7500000"/>
    <constructor-arg type="java.lang.String" value="42"/>
</bean>
```
Use the index attribute to specify explicitly the index of constructor arguments. For example:
```java
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg index="0" value="7500000"/>
    <constructor-arg index="1" value="42"/>
</bean>
```
In addition to resolving the ambiguity of multiple simple values, specifying an index resolves ambiguity where a constructor has two arguments of the same type. Note that the index is 0 based.

You can also use the constructor parameter name for value disambiguation:
```java
<bean id="exampleBean" class="examples.ExampleBean">
    <constructor-arg name="years" value="7500000"/>
    <constructor-arg name="ultimateAnswer" value="42"/>
</bean>
```

Keep in mind that to make this work out of the box your code must be compiled with the debug flag enabled so that Spring can look up the parameter name from the constructor. If you can’t compile your code with debug flag (or don’t want to) you can use @ConstructorProperties JDK annotation to explicitly name your constructor arguments. The sample class would then have to look as follows:

```java
package examples;

public class ExampleBean {

    // Fields omitted

    @ConstructorProperties({"years", "ultimateAnswer"})
    public ExampleBean(int years, String ultimateAnswer) {
        this.years = years;
        this.ultimateAnswer = ultimateAnswer;
    }

}
```

Setter-based dependency injection

Setter-based DI is accomplished by the container calling setter methods on your beans after invoking a no-argument constructor or no-argument static factory method to instantiate your bean.

The following example shows a class that can only be dependency-injected using pure setter injection. This class is conventional Java. It is a POJO that has no dependencies on container specific interfaces, base classes or annotations.

```java
public class SimpleMovieLister {

    // the SimpleMovieLister has a dependency on the MovieFinder
    private MovieFinder movieFinder;

    // a setter method so that the Spring container can inject a MovieFinder
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // business logic that actually uses the injected MovieFinder is omitted...

}
```
The ApplicationContext supports constructor-based and setter-based DI for the beans it manages. It also supports setter-based DI after some dependencies have already been injected through the constructor approach. You configure the dependencies in the form of a BeanDefinition, which you use in conjunction with PropertyEditor instances to convert properties from one format to another. However, most Spring users do not work with these classes directly (i.e., programmatically) but rather with XML bean definitions, annotated components (i.e., classes annotated with @Component, @Controller, etc.), or @Bean methods in Java-based @Configuration classes. These sources are then converted internally into instances of BeanDefinition and used to load an entire Spring IoC container instance.

> Constructor-based or setter-based DI?

  Since you can mix constructor-based and setter-based DI, it is a good rule of thumb to use constructors for mandatory dependencies and setter methods or configuration methods for optional dependencies. Note that use of the @Required annotation on a setter method can be used to make the property a required dependency.

  The Spring team generally advocates constructor injection as it enables one to implement application components as immutable objects and to ensure that required dependencies are not null. Furthermore constructor-injected components are always returned to client (calling) code in a fully initialized state. As a side note, a large number of constructor arguments is a bad code smell, implying that the class likely has too many responsibilities and should be refactored to better address proper separation of concerns.

  Setter injection should primarily only be used for optional dependencies that can be assigned reasonable default values within the class. Otherwise, not-null checks must be performed everywhere the code uses the dependency. One benefit of setter injection is that setter methods make objects of that class amenable to reconfiguration or re-injection later. Management through JMX MBeans is therefore a compelling use case for setter injection.

  Use the DI style that makes the most sense for a particular class. Sometimes, when dealing with third-party classes for which you do not have the source, the choice is made for you. For example, if a third-party class does not expose any setter methods, then constructor injection may be the only available form of DI.

Dependency resolution process

The container performs bean dependency resolution as follows:

- The ApplicationContext is created and initialized with configuration metadata that describes all the beans. Configuration metadata can be specified via XML, Java code, or annotations.
- For each bean, its dependencies are expressed in the form of properties, constructor arguments, or arguments to the static-factory method if you are using that instead of a normal constructor. These dependencies are provided to the bean, when the bean is actually created.
- Each property or constructor argument is an actual definition of the value to set, or a reference to another bean in the container.
- Each property or constructor argument which is a value is converted from its specified format to the actual type of that property or constructor argument. By default Spring can convert a value supplied in string format to all built-in types, such as int, long, String, boolean, etc.

The Spring container validates the configuration of each bean as the container is created. However, the bean properties themselves are not set until the bean is actually created. Beans that are singleton-scoped and set to be pre-instantiated (the default) are created when the container is created. Scopes are defined in Section 6.5, “Bean scopes”. Otherwise, the bean is created only when it is requested. Creation of a bean potentially causes a graph of beans to be created, as the bean’s dependencies and its dependencies' dependencies (and so on) are created and assigned. Note that resolution mismatches among those dependencies may show up late, i.e. on first creation of the affected bean.

> Circular dependencies

  If you use predominantly constructor injection, it is possible to create an unresolvable circular dependency scenario.

  For example: Class A requires an instance of class B through constructor injection, and class B requires an instance of class A through constructor injection. If you configure beans for classes A and B to be injected into each other, the Spring IoC container detects this circular reference at runtime, and throws a BeanCurrentlyInCreationException.

  One possible solution is to edit the source code of some classes to be configured by setters rather than constructors. Alternatively, avoid constructor injection and use setter injection only. In other words, although it is not recommended, you can configure circular dependencies with setter injection.

  Unlike the typical case (with no circular dependencies), a circular dependency between bean A and bean B forces one of the beans to be injected into the other prior to being fully initialized itself (a classic chicken/egg scenario).

You can generally trust Spring to do the right thing. It detects configuration problems, such as references to non-existent beans and circular dependencies, at container load-time. Spring sets properties and resolves dependencies as late as possible, when the bean is actually created. This means that a Spring container which has loaded correctly can later generate an exception when you request an object if there is a problem creating that object or one of its dependencies. For example, the bean throws an exception as a result of a missing or invalid property. This potentially delayed visibility of some configuration issues is why ApplicationContext implementations by default pre-instantiate singleton beans. At the cost of some upfront time and memory to create these beans before they are actually needed, you discover configuration issues when the ApplicationContext is created, not later. You can still override this default behavior so that singleton beans will lazy-initialize, rather than be pre-instantiated.

If no circular dependencies exist, when one or more collaborating beans are being injected into a dependent bean, each collaborating bean is totally configured prior to being injected into the dependent bean. This means that if bean A has a dependency on bean B, the Spring IoC container completely configures bean B prior to invoking the setter method on bean A. In other words, the bean is instantiated (if not a pre-instantiated singleton), its dependencies are set, and the relevant lifecycle methods (such as a configured init method or the InitializingBean callback method) are invoked.

Examples of dependency injection

The following example uses XML-based configuration metadata for setter-based DI. A small part of a Spring XML configuration file specifies some bean definitions:

```java
<bean id="exampleBean" class="examples.ExampleBean">
    <!-- setter injection using the nested ref element -->
    <property name="beanOne">
        <ref bean="anotherExampleBean"/>
    </property>

    <!-- setter injection using the neater ref attribute -->
    <property name="beanTwo" ref="yetAnotherBean"/>
    <property name="integerProperty" value="1"/>
</bean>

<bean id="anotherExampleBean" class="examples.AnotherBean"/>
<bean id="yetAnotherBean" class="examples.YetAnotherBean"/>
```
```java
public class ExampleBean {

    private AnotherBean beanOne;
    private YetAnotherBean beanTwo;
    private int i;

    public void setBeanOne(AnotherBean beanOne) {
        this.beanOne = beanOne;
    }

    public void setBeanTwo(YetAnotherBean beanTwo) {
        this.beanTwo = beanTwo;
    }

    public void setIntegerProperty(int i) {
        this.i = i;
    }

}
```
In the preceding example, setters are declared to match against the properties specified in the XML file. The following example uses constructor-based DI:
```java
<bean id="exampleBean" class="examples.ExampleBean">
    <!-- constructor injection using the nested ref element -->
    <constructor-arg>
        <ref bean="anotherExampleBean"/>
    </constructor-arg>

    <!-- constructor injection using the neater ref attribute -->
    <constructor-arg ref="yetAnotherBean"/>

    <constructor-arg type="int" value="1"/>
</bean>

<bean id="anotherExampleBean" class="examples.AnotherBean"/>
<bean id="yetAnotherBean" class="examples.YetAnotherBean"/>
```
```java
public class ExampleBean {

    private AnotherBean beanOne;
    private YetAnotherBean beanTwo;
    private int i;

    public ExampleBean(
        AnotherBean anotherBean, YetAnotherBean yetAnotherBean, int i) {
        this.beanOne = anotherBean;
        this.beanTwo = yetAnotherBean;
        this.i = i;
    }

}
```
The constructor arguments specified in the bean definition will be used as arguments to the constructor of the ExampleBean.

Now consider a variant of this example, where instead of using a constructor, Spring is told to call a static factory method to return an instance of the object:

```java
<bean id="exampleBean" class="examples.ExampleBean" factory-method="createInstance">
    <constructor-arg ref="anotherExampleBean"/>
    <constructor-arg ref="yetAnotherBean"/>
    <constructor-arg value="1"/>
</bean>

<bean id="anotherExampleBean" class="examples.AnotherBean"/>
<bean id="yetAnotherBean" class="examples.YetAnotherBean"/>
```
```java
public class ExampleBean {

    // a private constructor
    private ExampleBean(...) {
        ...
    }

    // a static factory method; the arguments to this method can be
    // considered the dependencies of the bean that is returned,
    // regardless of how those arguments are actually used.
    public static ExampleBean createInstance (
        AnotherBean anotherBean, YetAnotherBean yetAnotherBean, int i) {

        ExampleBean eb = new ExampleBean (...);
        // some other operations...
        return eb;
    }

}
```

Arguments to the static factory method are supplied via <constructor-arg/> elements, exactly the same as if a constructor had actually been used. The type of the class being returned by the factory method does not have to be of the same type as the class that contains the static factory method, although in this example it is. An instance (non-static) factory method would be used in an essentially identical fashion (aside from the use of the factory-bean attribute instead of the class attribute), so details will not be discussed here.

6.4.2 Dependencies and configuration in detail

As mentioned in the previous section, you can define bean properties and constructor arguments as references to other managed beans (collaborators), or as values defined inline. Spring’s XML-based configuration metadata supports sub-element types within its <property/> and <constructor-arg/> elements for this purpose.

Straight values (primitives, Strings, and so on)

The value attribute of the <property/> element specifies a property or constructor argument as a human-readable string representation. Spring’s conversion service is used to convert these values from a String to the actual type of the property or argument.

```java
<bean id="myDataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
    <!-- results in a setDriverClassName(String) call -->
    <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
    <property name="url" value="jdbc:mysql://localhost:3306/mydb"/>
    <property name="username" value="root"/>
    <property name="password" value="masterkaoli"/>
</bean>
```
The following example uses the p-namespace for even more succinct XML configuration.

```java
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:p="http://www.springframework.org/schema/p"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="myDataSource" class="org.apache.commons.dbcp.BasicDataSource"
        destroy-method="close"
        p:driverClassName="com.mysql.jdbc.Driver"
        p:url="jdbc:mysql://localhost:3306/mydb"
        p:username="root"
        p:password="masterkaoli"/>

</beans>
```
The preceding XML is more succinct; however, typos are discovered at runtime rather than design time, unless you use an IDE such as IntelliJ IDEA or the Spring Tool Suite (STS) that support automatic property completion when you create bean definitions. Such IDE assistance is highly recommended.

You can also configure a java.util.Properties instance as:
```java
<bean id="mappings"
    class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">

    <!-- typed as a java.util.Properties -->
    <property name="properties">
        <value>
            jdbc.driver.className=com.mysql.jdbc.Driver
            jdbc.url=jdbc:mysql://localhost:3306/mydb
        </value>
    </property>
</bean>
```
The Spring container converts the text inside the <value/> element into a java.util.Properties instance by using the JavaBeans PropertyEditor mechanism. This is a nice shortcut, and is one of a few places where the Spring team do favor the use of the nested <value/> element over the value attribute style.

The idref element

The idref element is simply an error-proof way to pass the id (string value - not a reference) of another bean in the container to a <constructor-arg/> or <property/> element.

```java
<bean id="theTargetBean" class="..."/>

<bean id="theClientBean" class="...">
    <property name="targetName">
        <idref bean="theTargetBean" />
    </property>
</bean>
```

```java
<bean id="theTargetBean" class="..." />

<bean id="client" class="...">
    <property name="targetName" value="theTargetBean" />
</bean>
```
The first form is preferable to the second, because using the idref tag allows the container to validate at deployment time that the referenced, named bean actually exists. In the second variation, no validation is performed on the value that is passed to the targetName property of the client bean. Typos are only discovered (with most likely fatal results) when the client bean is actually instantiated. If the client bean is a prototype bean, this typo and the resulting exception may only be discovered long after the container is deployed.

[Note]
The local attribute on the idref element is no longer supported in the 4.0 beans xsd since it does not provide value over a regular bean reference anymore. Simply change your existing idref local references to idref bean when upgrading to the 4.0 schema.

A common place (at least in versions earlier than Spring 2.0) where the <idref/> element brings value is in the configuration of AOP interceptors in a ProxyFactoryBean bean definition. Using <idref/> elements when you specify the interceptor names prevents you from misspelling an interceptor id.

References to other beans (collaborators)

The ref element is the final element inside a <constructor-arg/> or <property/> definition element. Here you set the value of the specified property of a bean to be a reference to another bean (a collaborator) managed by the container. The referenced bean is a dependency of the bean whose property will be set, and it is initialized on demand as needed before the property is set. (If the collaborator is a singleton bean, it may be initialized already by the container.) All references are ultimately a reference to another object. Scoping and validation depend on whether you specify the id/name of the other object through the bean, local, or parent attributes.

Specifying the target bean through the bean attribute of the <ref/> tag is the most general form, and allows creation of a reference to any bean in the same container or parent container, regardless of whether it is in the same XML file. The value of the bean attribute may be the same as the id attribute of the target bean, or as one of the values in the name attribute of the target bean.

```java
<ref bean="someBean"/>
```

Specifying the target bean through the parent attribute creates a reference to a bean that is in a parent container of the current container. The value of the parent attribute may be the same as either the id attribute of the target bean, or one of the values in the name attribute of the target bean, and the target bean must be in a parent container of the current one. You use this bean reference variant mainly when you have a hierarchy of containers and you want to wrap an existing bean in a parent container with a proxy that will have the same name as the parent bean.

```java
<!-- in the parent context -->
<bean id="accountService" class="com.foo.SimpleAccountService">
    <!-- insert dependencies as required as here -->
</bean>
```
```java
<!-- in the child (descendant) context -->
<bean id="accountService" <!-- bean name is the same as the parent bean -->
    class="org.springframework.aop.framework.ProxyFactoryBean">
    <property name="target">
        <ref parent="accountService"/> <!-- notice how we refer to the parent bean -->
    </property>
    <!-- insert other configuration and dependencies as required here -->
</bean>
```
[Note]
The local attribute on the ref element is no longer supported in the 4.0 beans xsd since it does not provide value over a regular bean reference anymore. Simply change your existing ref local references to ref bean when upgrading to the 4.0 schema.

Inner beans

A <bean/> element inside the <property/> or <constructor-arg/> elements defines a so-called inner bean.
```java
<bean id="outer" class="...">
    <!-- instead of using a reference to a target bean, simply define the target bean inline -->
    <property name="target">
        <bean class="com.example.Person"> <!-- this is the inner bean -->
            <property name="name" value="Fiona Apple"/>
            <property name="age" value="25"/>
        </bean>
    </property>
</bean>
```

An inner bean definition does not require a defined id or name; if specified, the container does not use such a value as an identifier. The container also ignores the scope flag on creation: Inner beans are always anonymous and they are always created with the outer bean. It is not possible to inject inner beans into collaborating beans other than into the enclosing bean or to access them independently.

As a corner case, it is possible to receive destruction callbacks from a custom scope, e.g. for a request-scoped inner bean contained within a singleton bean: The creation of the inner bean instance will be tied to its containing bean, but destruction callbacks allow it to participate in the request scope’s lifecycle. This is not a common scenario; inner beans typically simply share their containing bean’s scope.

Collections

In the <list/>, <set/>, <map/>, and <props/> elements, you set the properties and arguments of the Java Collection types List, Set, Map, and Properties, respectively.

```java
<bean id="moreComplexObject" class="example.ComplexObject">
    <!-- results in a setAdminEmails(java.util.Properties) call -->
    <property name="adminEmails">
        <props>
            <prop key="administrator">administrator@example.org</prop>
            <prop key="support">support@example.org</prop>
            <prop key="development">development@example.org</prop>
        </props>
    </property>
    <!-- results in a setSomeList(java.util.List) call -->
    <property name="someList">
        <list>
            <value>a list element followed by a reference</value>
            <ref bean="myDataSource" />
        </list>
    </property>
    <!-- results in a setSomeMap(java.util.Map) call -->
    <property name="someMap">
        <map>
            <entry key="an entry" value="just some string"/>
            <entry key ="a ref" value-ref="myDataSource"/>
        </map>
    </property>
    <!-- results in a setSomeSet(java.util.Set) call -->
    <property name="someSet">
        <set>
            <value>just some string</value>
            <ref bean="myDataSource" />
        </set>
    </property>
</bean>
```
The value of a map key or value, or a set value, can also again be any of the following elements:
```java
bean | ref | idref | list | set | map | props | value | null
```

Collection merging

The Spring container also supports the merging of collections. An application developer can define a parent-style <list/>, <map/>, <set/> or <props/> element, and have child-style <list/>, <map/>, <set/> or <props/> elements inherit and override values from the parent collection. That is, the child collection’s values are the result of merging the elements of the parent and child collections, with the child’s collection elements overriding values specified in the parent collection.

This section on merging discusses the parent-child bean mechanism. Readers unfamiliar with parent and child bean definitions may wish to read the relevant section before continuing.

The following example demonstrates collection merging:

```java
<beans>
    <bean id="parent" abstract="true" class="example.ComplexObject">
        <property name="adminEmails">
            <props>
                <prop key="administrator">administrator@example.com</prop>
                <prop key="support">support@example.com</prop>
            </props>
        </property>
    </bean>
    <bean id="child" parent="parent">
        <property name="adminEmails">
            <!-- the merge is specified on the child collection definition -->
            <props merge="true">
                <prop key="sales">sales@example.com</prop>
                <prop key="support">support@example.co.uk</prop>
            </props>
        </property>
    </bean>
<beans>
```
Notice the use of the merge=true attribute on the <props/> element of the adminEmails property of the child bean definition. When the child bean is resolved and instantiated by the container, the resulting instance has an adminEmails Properties collection that contains the result of the merging of the child’s adminEmails collection with the parent’s adminEmails collection.

```java
administrator=administrator@example.com
sales=sales@example.com
support=support@example.co.uk
```

The child Properties collection’s value set inherits all property elements from the parent <props/>, and the child’s value for the support value overrides the value in the parent collection.

This merging behavior applies similarly to the <list/>, <map/>, and <set/> collection types. In the specific case of the <list/> element, the semantics associated with the List collection type, that is, the notion of an ordered collection of values, is maintained; the parent’s values precede all of the child list’s values. In the case of the Map, Set, and Properties collection types, no ordering exists. Hence no ordering semantics are in effect for the collection types that underlie the associated Map, Set, and Properties implementation types that the container uses internally.

Limitations of collection merging

You cannot merge different collection types (such as a Map and a List), and if you do attempt to do so an appropriate Exception is thrown. The merge attribute must be specified on the lower, inherited, child definition; specifying the merge attribute on a parent collection definition is redundant and will not result in the desired merging.

Strongly-typed collection

With the introduction of generic types in Java 5, you can use strongly typed collections. That is, it is possible to declare a Collection type such that it can only contain String elements (for example). If you are using Spring to dependency-inject a strongly-typed Collection into a bean, you can take advantage of Spring’s type-conversion support such that the elements of your strongly-typed Collection instances are converted to the appropriate type prior to being added to the Collection.

```java
public class Foo {

    private Map<String, Float> accounts;

    public void setAccounts(Map<String, Float> accounts) {
        this.accounts = accounts;
    }
}
```
```java
<beans>
    <bean id="foo" class="x.y.Foo">
        <property name="accounts">
            <map>
                <entry key="one" value="9.99"/>
                <entry key="two" value="2.75"/>
                <entry key="six" value="3.99"/>
            </map>
        </property>
    </bean>
</beans>
```
When the accounts property of the foo bean is prepared for injection, the generics information about the element type of the strongly-typed Map<String, Float> is available by reflection. Thus Spring’s type conversion infrastructure recognizes the various value elements as being of type Float, and the string values 9.99, 2.75, and 3.99 are converted into an actual Float type.

Null and empty string values

Spring treats empty arguments for properties and the like as empty Strings. The following XML-based configuration metadata snippet sets the email property to the empty String value ("").

```java
<bean class="ExampleBean">
    <property name="email" value=""/>
</bean>
```
The preceding example is equivalent to the following Java code:
```java
exampleBean.setEmail("")
```
The <null/> element handles null values. For example:
```java
<bean class="ExampleBean">
    <property name="email">
        <null/>
    </property>
</bean>
```
The above configuration is equivalent to the following Java code:
```java
exampleBean.setEmail(null)
```
XML shortcut with the p-namespace

The p-namespace enables you to use the bean element’s attributes, instead of nested <property/> elements, to describe your property values and/or collaborating beans.

Spring supports extensible configuration formats with namespaces, which are based on an XML Schema definition. The beans configuration format discussed in this chapter is defined in an XML Schema document. However, the p-namespace is not defined in an XSD file and exists only in the core of Spring.

The following example shows two XML snippets that resolve to the same result: The first uses standard XML format and the second uses the p-namespace.

```java
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:p="http://www.springframework.org/schema/p"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean name="classic" class="com.example.ExampleBean">
        <property name="email" value="foo@bar.com"/>
    </bean>

    <bean name="p-namespace" class="com.example.ExampleBean"
        p:email="foo@bar.com"/>
</beans>
```

The example shows an attribute in the p-namespace called email in the bean definition. This tells Spring to include a property declaration. As previously mentioned, the p-namespace does not have a schema definition, so you can set the name of the attribute to the property name.

This next example includes two more bean definitions that both have a reference to another bean:

```java
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:p="http://www.springframework.org/schema/p"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean name="john-classic" class="com.example.Person">
        <property name="name" value="John Doe"/>
        <property name="spouse" ref="jane"/>
    </bean>

    <bean name="john-modern"
        class="com.example.Person"
        p:name="John Doe"
        p:spouse-ref="jane"/>

    <bean name="jane" class="com.example.Person">
        <property name="name" value="Jane Doe"/>
    </bean>
</beans>
```
As you can see, this example includes not only a property value using the p-namespace, but also uses a special format to declare property references. Whereas the first bean definition uses <property name="spouse" ref="jane"/> to create a reference from bean john to bean jane, the second bean definition uses p:spouse-ref="jane" as an attribute to do the exact same thing. In this case spouse is the property name, whereas the -ref part indicates that this is not a straight value but rather a reference to another bean.

[Note]
The p-namespace is not as flexible as the standard XML format. For example, the format for declaring property references clashes with properties that end in Ref, whereas the standard XML format does not. We recommend that you choose your approach carefully and communicate this to your team members, to avoid producing XML documents that use all three approaches at the same time.

XML shortcut with the c-namespace

Similar to the the section called “XML shortcut with the p-namespace”, the c-namespace, newly introduced in Spring 3.1, allows usage of inlined attributes for configuring the constructor arguments rather then nested constructor-arg elements.

Let’s review the examples from the section called “Constructor-based dependency injection” with the c: namespace:

```java
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:c="http://www.springframework.org/schema/c"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="bar" class="x.y.Bar"/>
    <bean id="baz" class="x.y.Baz"/>

    <!-- traditional declaration -->
    <bean id="foo" class="x.y.Foo">
        <constructor-arg ref="bar"/>
        <constructor-arg ref="baz"/>
        <constructor-arg value="foo@bar.com"/>
    </bean>

    <!-- c-namespace declaration -->
    <bean id="foo" class="x.y.Foo" c:bar-ref="bar" c:baz-ref="baz" c:email="foo@bar.com"/>

</beans>
```
The c: namespace uses the same conventions as the p: one (trailing -ref for bean references) for setting the constructor arguments by their names. And just as well, it needs to be declared even though it is not defined in an XSD schema (but it exists inside the Spring core).

For the rare cases where the constructor argument names are not available (usually if the bytecode was compiled without debugging information), one can use fallback to the argument indexes:

```java
<!-- c-namespace index declaration -->
<bean id="foo" class="x.y.Foo" c:_0-ref="bar" c:_1-ref="baz"/>
```
[Note]
Due to the XML grammar, the index notation requires the presence of the leading _ as XML attribute names cannot start with a number (even though some IDE allow it).

In practice, the constructor resolution mechanism is quite efficient in matching arguments so unless one really needs to, we recommend using the name notation through-out your configuration.

Compound property names

You can use compound or nested property names when you set bean properties, as long as all components of the path except the final property name are not null. Consider the following bean definition.

```java
<bean id="foo" class="foo.Bar">
    <property name="fred.bob.sammy" value="123" />
</bean>
```
The foo bean has a fred property, which has a bob property, which has a sammy property, and that final sammy property is being set to the value 123. In order for this to work, the fred property of foo, and the bob property of fred must not be null after the bean is constructed, or a NullPointerException is thrown.

6.4.3 Using depends-on






























