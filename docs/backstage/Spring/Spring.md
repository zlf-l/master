# Spring

## 简介

Spring是目前最流行的Java框架，他里面集成了大量的工具以及一些开箱即用的解决方案。

Spring是一个轻量级的控制反转和面向切面的容器框架，用来解决企业项目开发的复杂问题——解耦。

* 轻量级：体积小，对代码没有入侵性
* 控制反转：IoC（Inverse of Control），把创建对象的工作交给Spring完成，Spring在创建对象的时候同时可以完成对象属性复制（DI）
* 面向切面：`AOP`（Aspect Oriented Programming）面向切面编程，可以再不改变原有业务逻辑的情况下实现对业务的增强
* 容器：实例（beans）的容器，管理创建的对象

## Spring架构

* Core Container

  Spring容器组件，用于完成实例的创建和管理

  > core
  >
  > beans实例管理
  >
  > context容器上下文

* AOP

  Spring AOP组件，实现面向切面编程

* Web

  Spring Web 组件实际指的是SpringMVC框架，实现Web项目MVC控制

  > web（Spring对web项目的支持）
  >
  > webmvc (SpringMVC组件)

* Data Access

  Spring数据访问组件，也是⼀个基于JDBC封装的持久层框架（即使没有mybatis， Spring也可以完成 持久化操作）

* Test

  Spring的单元测试组件，提供了Spring环境下的单元测试⽀持

## Spring Projects

* Spring Boot 脚手架
* Spring Framework 基础核心框架
* Spring Data 数据持久化的方案
* Spring Cloud 微服务
* Spring Security 权限框架

针对不同的技术领域，Spring都提供了非常完善的解决方案，不光是官方的还是第三方的，都可以使用Spring的规范接入进来。

## Spring Framework

### Spring Core

Spring是一个Bean（实例化）的容器框架。（bean就是能提供服务的或者功能的类）

Spring主要在系统中承担这样的一些职责：

* 管理bean的生命周期（负责创建和销毁这些bean）
* 负责调度bean来提供服务
* 维护和管理多个bean之间的关系

由此Spring官宣的重要特性：

* IoC：Inverce of Control（控制反转）
* DI：Dependency Injection （依赖注入）
* AOP：Aspect Oriented Programming （面向切面编程）

### IoC

`IoC`( `Inversion-of-Control`)模式是关于提供任何类型的`callback`（控制反应），而不是直接行动（换句话说，反转和/或将控制重定向到外部处理程序/控制器）。`DI`( `Dependency-Injection`)模式是 `IoC`模式的一个更具体的版本，旨在从代码中移除依赖项。

> 每个`DI`实现都可以考虑`IoC`，但不应该调用它`IoC`，因为实现依赖注入比回调更难（不要通过使用通用术语“`IoC`”来降低产品的价值）。

IoC（控制反转），以前是由开发人员自己来创建和销毁对象，但使用Spring的时候，可以把这个工作交给Spring容器来处理。

Spring IoC 容器组件，可以完成对象的创建、对象属性赋值、对象管理

#### 基于XML风格

配置文件

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!-- 对于⼀个xml⽂件如果作为框架的配置⽂件，需要遵守框架的配置规则 -->
    <!-- 通常⼀个框架为了让开发者能够正确的配置，都会提供xml的规范⽂件（dtd\xsd） -->

    <!--    配置service这个bean-->
    <bean id="helloService" class="com.example.springbootdemo.ioc.xml.HelloService"></bean>
</beans>
~~~

~~~java
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("spring/config.xml");
// 根据id来获取对应bean的实例
HelloService helloService = (HelloService) context.getBean("helloService");
helloService.hello();
~~~

容器还提供了一些其他功能特性：

- 单例模式
- 根据配置调用指定的初始化和销毁方法

#### 基于注解

Spring IoC的使⽤，需要我们通过XML将类声明给Spring容器进⾏管理，从⽽通过Spring⼯⼚完成对象 的创建及属性值的注⼊； 

Spring除了提供基于XML的配置⽅式，同时提供了基于注解的配置：直接在实体类中添加注解声明给 Spring容器管理，以简化开发步骤

配置文件

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd">
    <!-- 声明使⽤注解配置 -->
    <context:annotation-config/>
    <!-- 声明Spring⼯⼚注解的扫描范围 -->
    <context:component-scan base-package="com.qfedu.beans"/>
</beans>
~~~

常用注解

* @Component

  类注解，声明此类被Spring容器进⾏管理，相当于bean标签的作⽤

  @Component(value="stu") value属性⽤于指定当前bean的id，相当于bean标签的id属性； value属性也可以省略，如果省略当前类的id默认为类名⾸字⺟改⼩写

  除了@Component之外 @Service、 @Controller、 @Repository这三个注解也可以将类声明给 Spring管理，他们主要是语义上的区别 

  >  @Controller 注解主要声明将控制器类配置给Spring管理，例如Servlet
  >
  > @Service 注解主要声明业务处理类配置Spring管理， Service接⼝的实现类
  >
  > @Repository 直接主要声明持久化类配置给Spring管理， DAO接⼝
  >
  > @Component 除了控制器、 servcie和DAO之外的类⼀律使⽤此注解声明

* @Scope 

  类注解，⽤于声明当前类单例模式还是 ⾮单例模式，相当于bean标签的scope属性 

  @Scope("prototype") 表⽰声明当前类为⾮单例模式（默认单例模式） 

* @Lazy 

  类注解，⽤于声明⼀个单例模式的Bean是否为懒汉模式 

  @Lazy(true) 表⽰声明为懒汉模式，默认为饿汉模式 

* @PostConstruct 

  ⽅法注解，声明⼀个⽅法为当前类的初始化⽅法（在构造器之后执⾏），相当于bean标签的init-method属性 

* @PreDestroy 

  ⽅法注解，声明⼀个⽅法为当前类的销毁⽅法（在对象从容器中释放之前执⾏），相当于bean标 签的destorymethod属性 

* @Autowired 

  属性注解、⽅法注解（set⽅法），声明当前属性⾃动装配，默认byType 

  @Autowired(required = false) 通过requried属性设置当前⾃动装配是否为必须（默认必须⸺如 果没有找到类型与属性类型匹配的bean则抛出异常） •

  > byType、ref引⽤

* @Resource 

  属性注解，也⽤于声明属性⾃动装配 

  默认装配⽅式为byName，如果根据byName没有找到对应的bean，则继续根据byType寻找对应 的bean，根据byType如果依然没有找到Bean或者找到不⽌⼀个类型匹配的bean,则抛出异常。
