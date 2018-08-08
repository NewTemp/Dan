# 一、Hystrix Dashboard应用

## Hystrix Dashboard服务

创建SpringBoot工程，SpringBoot版本2.0.3.RELEASE，SpringCloud版本Finchley.RELEASE

引入依赖

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-hystrix-dashboard</artifactId>
</dependency>
```

启动类

```
@EnableHystrixDashboard
@SpringBootApplication
public class DashboardApplication {

    public static void main(String[] args) {
        SpringApplication.run(DashboardApplication.class, args);
    }
}
```

配置文件

```
spring:
  application:
    name: dashboard
server:
  port: 11000
```

## 服务实例

通过访问服务的/actuator/hystrix.stream接口来实现监控，需要服务实例添加这个 endpoint。

添加依赖

```

<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

```

启动类

通过添加```@EnableCircuitBreaker```或者```@EnableHystrix```开启断路器功能


配置文件，添加配置

```
management:
  endpoints:
    web:
      exposure:
        include: hystrix.stream
```
