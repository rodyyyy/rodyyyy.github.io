---
layout: post
author: Chris Rody
title: Springmvc记录
---

一些Springmvc的学习笔记

##  Springmvc的学习笔记

**1、在springmvc框架中，想要使用mvc，就要使用< mvc:annotation-driven/ >mvc的注解驱动，springmvc工作需要处理器映射器和处理器适配器，使用了这个配置就可以直接使用@Controller，进行web层的注解。 **

**2、在整个项目的流程中，spring对类的实例化，以及类和类之间的关系就需要< context:component-scan/ > 组件扫描，使用组件扫描可以扫描指定包下面的注解类，以及成员变量，也就是实例化类，同时完成spring的注入功能。**

**3、最后一个在spring配置事物的过程中，一般建议的还是使用手动配置事物，因为手动配置可以约定很多方法的前缀，想select，find，get，insert，delete、update等，在开发过程中便于统一所有人的命名方式。**

如果使用的事物的注解<tx:annotation-driven transaction-manager="transactionManager" />，就可以直接在指定的类或者方法上使用@Transactional注解。

