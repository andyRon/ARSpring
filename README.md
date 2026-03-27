ARSpring
---

实现迷你版Spring框架。


ARSpring设计目标如下：

- context模块：实现ApplicationContext容器与Bean的管理；
- aop模块：实现AOP功能；
- jdbc模块：实现JdbcTemplate，以及声明式事务管理；
- web模块：实现Web MVC和REST API；
- boot模块：实现一个简化版的“Spring Boot”，用于打包运行。

## 1 实现IoC容器

Spring的核心就是能管理一组Bean，并能自动配置依赖关系的IoC容器。ARSpring核心context模块就是要实现IoC容器。

### 设计目标

Spring的IoC容器分两类：
- BeanFactory，延迟创建Bean
- ApplicationContext，在启动时初始化所有Bean

实际使用时，99%都采用ApplicationContext，因此，ARSpring仅实现ApplicationContext，不支持BeanFactory。

ARSpring仅实现Annotation配置+`@ComponentScan`扫描方式完成容器的配置。

ARSpring仅支持Singleton类型的Bean，不支持Prototype类型的Bean，因为实际使用中，99%都采用Singleton。依赖注入则与Spring保持一致，支持构造方法、Setter方法与字段注入。支持`@Configuration`和`BeanPostProcessor`。至于Spring的其他功能，例如，层级容器、MessageSource、一个Bean允许多个名字等功能，一概不支持！

最终ARSpring在IOC方面与Spring的异同：

| 功能     | Spring Framework                    | ARSpring                       |
| -------- | ----------------------------------- | ------------------------------ |
| IoC容器  | 支持BeanFactory和ApplicationContext | 仅支持ApplicationContext       |
| 配置方式 | 支持XML与Annotation                 | 仅支持Annotation               |
| 扫描方式 | 支持按包名扫描                      | 支持按包名扫描                 |
| Bean类型 | 支持Singleton和Prototype            | 仅支持Singleton                |
| Bean工厂 | 支持FactoryBean和@Bean注解          | 仅支持@Bean注解                |
| 定制Bean | 支持BeanPostProcessor               | 支持BeanPostProcessor          |
| 依赖注入 | 支持构造方法、Setter方法与字段      | 支持构造方法、Setter方法与字段 |
| 多容器   | 支持父子容器                        | 不支持                         |

### Annotation配置



### 实现ResourceResolver

