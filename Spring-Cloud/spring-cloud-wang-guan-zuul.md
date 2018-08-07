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

serviceId为微服务名称，path为路由地址

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

##### 四、跨域问题

##### 转发过滤器前，在HttpServletResponse添加跨域头

1.创建CorsFilter .java

```
@Component
public class CorsFilter extends ZuulFilter {

    @Override
    public String filterType() {
        return "pre"; // 可以在请求被路由之前调用
    }

    @Override
    public int filterOrder() {
        return 0;// filter执行顺序，通过数字指定 ,优先级为0，数字越大，优先级越低
    }

    @Override
    public boolean shouldFilter() {
        return true;// 是否执行该过滤器，此处为true，说明需要过滤
    }

    @Override
    public Object run() {
        RequestContext ctx = RequestContext.getCurrentContext();
            HttpServletResponse res= ctx.getResponse();
            res.setHeader("Access-Control-Allow-Origin", "*");
            res.setHeader("Access-Control-Allow-Methods", "POST, GET, OPTIONS, DELETE ,PUT");
            res.setHeader("Access-Control-Max-Age", "3600");
            res.setHeader("Access-Control-Allow-Headers", "Origin, No-Cache, X-Requested-With, If-Modified-Since,"
                + " Pragma, Last-Modified, Cache-Control, Expires, Content-Type, "
                + "X-E4M-With,userId,token,Authorization,deviceId,Access-Control-Allow-Origin,Access-Control-Allow-Headers,Access-Control-Allow-Methods");
            res.setHeader("Access-Control-Allow-Credentials", "true");
            return null;
    }
}
```

2.启动类ZuulApplication.java，添加如下

```
    @Bean
    public CorsFilter corsFilter(){
        return new CorsFilter();
    }
```

3.测试

重新启动，即可解决跨域问题。

4.注意

* 如果zuul配置了cors跨域问题，则不能在微服务下面在配置cors跨域，不然会继续存在跨域问题。
* Filter是Zuul的核心，用来实现对外服务的控制。Filter的生命周期有4个，分别是“pre”、“routing”、“post”、“error”。具体请看教程：[springcloud\(十一\)：服务网关Zuul高级篇](https://blog.csdn.net/u011820505/article/details/79373594)

##### 五、网关权限

核心框架为Spring Cloud security。所有微服务经过网关zuul，进行权限控制。

前提：

1.添加依赖pom.xml

```
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-security</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-openfeign</artifactId>
        </dependency>
```

```
dependency
>


<
groupId
>
org.springframework.cloud
<
/groupId
>


<
artifactId
>
spring-cloud-starter-security
<
/artifactId
>


<
/dependency
>
```



