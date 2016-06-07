##第一部分. Spring Framework概述

Spring Framework是一个轻量级的解决方案,在构建一站式企业级应用上有很大的潜能。然而,Spring是模块化的,允许你只用你需要的模块,而不需要引用其余部分。你可以使用IoC容器,可以选择它支持的任何web框架,你也可以仅仅整合Hibernate或者JDBC抽象层使用。
Spring Framework支持声明式的事务管理,通过RMI或者web services进行远程访问业务逻辑,并且提供多种数据持久化解决方案。它提供一个全功能的MVC框架,允许你透明的整合AOP到你的软件中。



Spring is designed to be non-intrusive, meaning that your domain logic code generally has no dependencies on the framework itself.
In your integration layer (such as the data access layer), some dependencies on the data access technology and the Spring libraries will exist.
However, it should be easy to isolate these dependencies from the rest of your code base.

This document is a reference guide to Spring Framework features.
If you have any requests, comments, or questions on this document, please post them on the user mailing list.
Questions on the Framework itself should be asked on StackOverflow (see https://spring.io/questions).