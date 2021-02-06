- [1. SpringBoot基本知识](#1-springboot基本知识)
  - [1.1. 常用注解](#11-常用注解)
  - [1.2. 静态资源](#12-静态资源)
  - [1.3. 自定义静态资源访问](#13-自定义静态资源访问)
  - [1.4. SpringBoot属性配置](#14-springboot属性配置)
    - [1.4.1. 自定义属性及读取](#141-自定义属性及读取)
    - [1.4.2. 多环境配置文件](#142-多环境配置文件)
  - [1.5. SpringBoot 构建 RESTful API](#15-springboot-构建-restful-api)
  - [1.6. SpringBoot 使用 Swagger2构建 API文档](#16-springboot-使用-swagger2构建-api文档)
  - [1.7. JPA](#17-jpa)
    - [1.7.1. 优势](#171-优势)
    - [1.7.2. SpringBoot 使用JPA使用@Query实现自定义查询语句](#172-springboot-使用jpa使用query实现自定义查询语句)
  - [1.8. SpringBoot使用Thymeleaf 模板引擎](#18-springboot使用thymeleaf-模板引擎)
# 1. SpringBoot基本知识

## 1.1. 常用注解
@requestBody
注解常用来处理content-type不是默认的application/x-www-form-urlcoded编码的内容，比如说：application/json或者是application/xml等。一般情况下来说常用其来处理application/json类型。
@RequestParam   获取查询参数。即url?name=value   这种形式
@PathVariable      获取路径参数。即url/{id}        这种形式


## 1.2. 静态资源

Spring Boot 对静态资源映射提供了默认配置
Spring Boot 默认将 /** 所有访问映射到以下目录：
classpath:/static 
classpath:/public 
classpath:/resources 
classpath:/META-INF/resources

## 1.3. 自定义静态资源访问
1. 配置类实现WebMvcConfigurer类

```java
@Configuration
public class WebMvcConfig implements WebMvcConfigurer {
    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        //将所有D:\\springboot\\pic\\ 访问都映射到/myPic/** 路径下
        registry.addResourceHandler("/myPic/**").addResourceLocations("file:D:\\springboot\\pic\\");
    }
}
```
2. 配置application.properties

```java
web.upload-path=D:/springboot/pic/
spring.mvc.static-path-pattern=/**
spring.resources.static-locations=classpath:/META-INF/resources/,classpath:/resources/,classpath:/static/,classpath:/public/,file:${web.upload-path}
```

web.upload-path：这个属于自定义的属性，指定了一个路径，注意要以/结尾；

spring.mvc.static-path-pattern=/**：表示所有的访问都经过静态资源路径；

spring.resources.static-locations：在这里配置静态资源路径，前面说了这里的配置是覆盖默认配置，所以需要将默认的也加上否则static、public等这些路径将不能被当作静态资源路径，在这个最末尾的file:${web.upload-path}之所有要加file:是因为指定的是一个具体的硬盘路径，其他的使用classpath指的是系统环境变量。

## 1.4. SpringBoot属性配置

创建Spring Boot项目时，会默认生成一个全局配置文件application.properties(可以修改后缀为.yml)，在src/main/resources目录下或者类路径的/config下。我们可以通过修改该配置文件来对一些默认配置的配置值进行修改。

### 1.4.1. 自定义属性及读取
我们可以在application.yml文件中，配置一些常量或者其他参数配置。读取的时候通过Spring的@Value(“${属性名}”)注解即可。

### 1.4.2. 多环境配置文件
使用多个yml配置文件进行配置属性文件
可以使用多个yml来配置属性，将于环境无关的属性放置到application.yml文件里面；通过与配置文件相同的命名规范，创建application-{profile}.yml文件 存放不同环境特有的配置，例如 application-test.yml 存放测试环境特有的配置属性，application-prod.yml 存放生产环境特有的配置属性。

通过这种形式来配置多个环境的属性文件，在application.yml文件里面spring.profiles.active=xxx来指定加载不同环境的配置,如果不指定，则默认只使用application.yml属性文件，不会加载其他的profiles的配置。

## 1.5. SpringBoot 构建 RESTful API

RESTful 是一种软件架构风格！
REST 就是指对同一个 URI 的资源的不同请求方式（GET，POST，PUT，DELETE）（表述）下
的做出的不同的操作（查，增，改，删），改变的是资源的状态，即表述性状态转移。 一
个符合 REST 风格的 URI 就可以称之一个 RESTful 的接口

## 1.6. SpringBoot 使用 Swagger2构建 API文档

采用 Swagger2 这套自动化文档工具来生
成文档，它可以轻松的整合到 Spring Boot 中，并与 Spring MVC 程序配合组织出强大 RESTful API 文档。



## 1.7. JPA
JPA顾名思义就是Java Persistence API的意思，是JDK 5.0注解或XML描述对象－关系表的映射关系，并将运行期的实体对象持久化到数据库中。

### 1.7.1. 优势

1. 标准化
   JPA 是 JCP 组织发布的 Java EE 标准之一，因此任何声称符合 JPA 标准的框架都遵循同样的架构，提供相同的访问API，这保证了基于JPA开发的企业应用能够经过少量的修改就能够在不同的JPA框架下运行。
2. 容器级特性的支持
   JPA框架中支持大数据集、事务、并发等容器级事务，这使得 JPA 超越了简单持久化框架的局限，在企业应用发挥更大的作用。
3. 简单方便
   JPA的主要目标之一就是提供更加简单的编程模型：在JPA框架下创建实体和创建Java 类一样简单，没有任何的约束和限制，只需要使用 javax.persistence.Entity进行注释，JPA的框架和接口也都非常简单，没有太多特别的规则和设计模式的要求，开发者可以很容易的掌握。JPA基于非侵入式原则设计，因此可以很容易的和其它框架或者容器集成。
4. 查询能力
   JPA的查询语言是面向对象而非面向数据库的，它以面向对象的自然语法构造查询语句，可以看成是Hibernate HQL的等价物。JPA定义了独特的JPQL（Java Persistence Query Language），JPQL是EJB QL的一种扩展，它是针对实体的一种查询语言，操作对象是实体，而不是关系数据库的表，而且能够支持批量更新和修改、JOIN、GROUP BY、HAVING 等通常只有 SQL 才能够提供的高级查询特性，甚至还能够支持子查询。
5. 高级特性
   JPA 中能够支持面向对象的高级特性，如类之间的继承、多态和类之间的复杂关系，这样的支持能够让开发者最大限度的使用面向对象的模型设计企业应用，而不需要自行处理这些特性在关系数据库的持久化。

### 1.7.2. SpringBoot 使用JPA使用@Query实现自定义查询语句
Jpa提供了非常大的自由度给开发者，我们可以在接口方法中通过定义@Query 注解自定义接口方法的JPQL语句。

## 1.8. SpringBoot使用Thymeleaf 模板引擎
Thymeleaf是一个Java类库，它是一个xml/xhtml/html5的模板引擎，可以作为MVC的Web应用的View层。Thymeleaf还提供了额外的模块与Spring MVC集成，因此我们可以使用Thymeleaf完全替代JSP。




