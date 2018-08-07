##### **一、简单介绍**

##### Spring Cloud Zuul的作用就是路由转发和过滤， 即将请求转发到微服务或拦截请求； Zuul默认集成了负载均衡功能。

##### **二、简单使用**

##### **本项目基于Springboot2.0.3和Spring Cloud Finchley进行部署。**

1.添加依赖pom.xml

```java
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-zuul</artifactId>
        </dependency>
```

2.配置文件application.yml

```
spring:
  application:
    name: zuul
server:
  port: 8040
```

3.启动类ZuulApplication.java

启动类添加@EnableZuulProxy，即可支持网关路由

```
@EnableZuulProxy
@SpringBootApplication
public class ZuulApplication {
    public static void main(String[] args) {
        SpringApplication.run(ZuulApplication.class, args);
    }

}
```

4.测试

用浏览器访问localhost:8040，即可测试是否启动项目。

##### 三、服务化

##### Zuul注册到eureka server，通过url的映射转化为服务名ServiceId进行映射。

前提：

* 先启动eureka，端口号为8761
* 再启动微服务account，端口号为9090，注册到eureka，并存在请求localhost:9090/account/test

1.添加依赖pom.xml

添加组建服务eureka注册、发现

```
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>
```

2.配置文件application.yml

注册到eureka,并且配置路由转发。

stripPrefix为false时，则保留account前缀，再转发url到微服务

```
eureka:
  client:
    service-url:
      defaultZone:   http://localhost:8761/eureka
zuul:
  routes:
    account:
      path: /account/**
      serviceId: account
      stripPrefix: false
```

3.测试

用浏览器访问localhost:8040/account/test，如果通过zuul路由，能访问account服务（端口是9090）的请求，则为成功。

网关zuul服务和account服务注册到eureka，如下图：

![](/assets/QQ截图20180807170054.jpg)

