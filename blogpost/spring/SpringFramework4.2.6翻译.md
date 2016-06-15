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

Part III. Core Technologies

This part of the reference documentation covers all of those technologies that are absolutely integral to the Spring Framework.

Foremost amongst these is the Spring Framework’s Inversion of Control (IoC) container. A thorough treatment of the Spring Framework’s IoC container is closely followed by comprehensive coverage of Spring’s Aspect-Oriented Programming (AOP) technologies. The Spring Framework has its own AOP framework, which is conceptually easy to understand, and which successfully addresses the 80% sweet spot of AOP requirements in Java enterprise programming.

Coverage of Spring’s integration with AspectJ (currently the richest - in terms of features - and certainly most mature AOP implementation in the Java enterprise space) is also provided.

- Chapter 6, The IoC container
- Chapter 7, Resources
- Chapter 8, Validation, Data Binding, and Type Conversion
- Chapter 9, Spring Expression Language (SpEL)
- Chapter 10, Aspect Oriented Programming with Spring
- Chapter 11, Spring AOP APIs

6. The IoC container

6.1 Introduction to the Spring IoC container and beans

This chapter covers the Spring Framework implementation of the Inversion of Control (IoC) [1] principle. IoC is also known as dependency injection (DI). It is a process whereby objects define their dependencies, that is, the other objects they work with, only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method. The container then injects those dependencies when it creates the bean. This process is fundamentally the inverse, hence the name Inversion of Control (IoC), of the bean itself controlling the instantiation or location of its dependencies by using direct construction of classes, or a mechanism such as the Service Locator pattern.

The org.springframework.beans and org.springframework.context packages are the basis for Spring Framework’s IoC container. The BeanFactory interface provides an advanced configuration mechanism capable of managing any type of object. ApplicationContext is a sub-interface of BeanFactory. It adds easier integration with Spring’s AOP features; message resource handling (for use in internationalization), event publication; and application-layer specific contexts such as the WebApplicationContext for use in web applications.

In short, the BeanFactory provides the configuration framework and basic functionality, and the ApplicationContext adds more enterprise-specific functionality. The ApplicationContext is a complete superset of the BeanFactory, and is used exclusively in this chapter in descriptions of Spring’s IoC container. For more information on using the BeanFactory instead of the ApplicationContext, refer to Section 6.16, “The BeanFactory”.

In Spring, the objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container. Otherwise, a bean is simply one of many objects in your application. Beans, and the dependencies among them, are reflected in the configuration metadata used by a container.

6.2 Container overview

The interface org.springframework.context.ApplicationContext represents the Spring IoC container and is responsible for instantiating, configuring, and assembling the aforementioned beans. The container gets its instructions on what objects to instantiate, configure, and assemble by reading configuration metadata. The configuration metadata is represented in XML, Java annotations, or Java code. It allows you to express the objects that compose your application and the rich interdependencies between such objects.

Several implementations of the ApplicationContext interface are supplied out-of-the-box with Spring. In standalone applications it is common to create an instance of ClassPathXmlApplicationContext or FileSystemXmlApplicationContext. While XML has been the traditional format for defining configuration metadata you can instruct the container to use Java annotations or code as the metadata format by providing a small amount of XML configuration to declaratively enable support for these additional metadata formats.

In most application scenarios, explicit user code is not required to instantiate one or more instances of a Spring IoC container. For example, in a web application scenario, a simple eight (or so) lines of boilerplate web descriptor XML in the web.xml file of the application will typically suffice (see Section 6.15.4, “Convenient ApplicationContext instantiation for web applications”). If you are using the Spring Tool Suite Eclipse-powered development environment this boilerplate configuration can be easily created with few mouse clicks or keystrokes.

The following diagram is a high-level view of how Spring works. Your application classes are combined with configuration metadata so that after the ApplicationContext is created and initialized, you have a fully configured and executable system or application.










