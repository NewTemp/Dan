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

三、服务化

通过url映射来转发

