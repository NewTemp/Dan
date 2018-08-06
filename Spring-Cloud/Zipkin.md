# 一、zipkin

## 快速启动

zipkin分为服务器端和客户端，客户端就是微服务中的应用.

在 Spring Cloud Sleuth 中对 Zipkin 的整合进行了自动化配置的封装，我们可以很轻松的引入和使用它。

### 服务器端

首先搭建个Zipkin的工程

POM文件

```

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.utech.trace</groupId>
    <artifactId>trace</artifactId>
    <version>1.0-SNAPSHOT</version>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.9.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>io.zipkin.java</groupId>
            <artifactId>zipkin-server</artifactId>
            <version>2.5.0</version>
        </dependency>
        <dependency>
            <groupId>io.zipkin.java</groupId>
            <artifactId>zipkin-autoconfigure-ui</artifactId>
            <version>2.5.0</version>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-deploy-plugin</artifactId>
                <version>2.8.2</version>
                <configuration>
                    <skip>true</skip>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>

```

启动类

```
package com.utech.trace;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import zipkin.server.EnableZipkinServer;

@SpringBootApplication
@EnableZipkinServer
public class TraceApplication {
    public static void main(String[] args) {
        SpringApplication.run(TraceApplication.class,args);
    }
}

```

配置文件

```

spring:
  application:
    name: trace
   # 表示当前程序不使用sleuth
  sleuth:
    enabled: false

server:
  port: 9411

```

启动后访问 http://localhost:9411/zipkin/ 就能看到界面

### 客户端

默认我们已经有了基本的微服务工程，想要微服务之间的调用被zipkin发现，需要在服务工程的POM中引入依赖、修改配置文件


添加依赖

```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-zipkin</artifactId>
</dependency>
```

添加配置

```

spring:
  sleuth:
    web:
      client:
        enabled: true
    sampler:
      probability: 1.0 # 将采样比例设置为 1.0，也就是全部都需要。默认是 0.1
  zipkin:
    base-url: http://localhost:9411/ # 指定 Zipkin 服务器的地址

```

> Spring Cloud Sleuth 有一个 Sampler 策略，可以通过这个实现类来控制采样算法。采样器不会阻碍 span 相关 id 的产生，但是会对导出以及附加事件标签的相关操作造成影响。 Sleuth 默认采样算法的实现是 Reservoir sampling，具体的实现类是 PercentageBasedSampler，默认的采样比例为: 0.1(即 10%)。不过我们可以通过spring.sleuth.sampler.percentage来设置，所设置的值介于 0.0 到 1.0 之间，1.0 则表示全部采集。


## 存储方式
Zipkin 提供了可插拔数据存储方式：In-Memory、MySql、Cassandra 以及 Elasticsearch。
上面示例的存储方式就是In-Memory，下面我们介绍下MySql的存储方式。

只需要添加服务端依赖、配置，不需要修改客户端


```
<!--保存到数据库需要如下依赖-->
<dependency>
    <groupId>io.zipkin.java</groupId>
    <artifactId>zipkin-autoconfigure-storage-mysql</artifactId>
    <version>2.5.0</version>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

配置文件

```

spring:
  datasource:
    url: jdbc:mysql://${MYSQL_HOST:localhost}:${MYSQL_PORT:3306}/zipkin?autoReconnect=true&useUnicode=true&characterEncoding=UTF-8&zeroDateTimeBehavior=convertToNull&useSSL=false
    username: root
    password: 123456
    driver-class-name: com.mysql.jdbc.Driver
    continue-on-error: true
  application:
    name: trace
  # 表示当前程序不使用sleuth
  sleuth:
    enabled: false

# zipkin数据保存到数据库中需要进行如下配置
zipkin:
  # 表示zipkin数据存储方式是mysql
  storage:
    type: mysql
server:
  port: 9411

```

## 发送方式

客户端发送链路调用的方式主要有两种，一种是 HTTP 报文的方式，还有一种是消息总线的方式如 RabbitMQ。

上面示例的发送方式就是HTTP的，下面我们介绍下RabbitMQ的存储方式。

修改服务端POM、配置文件

添加依赖

```
<!-- 使用消息的方式收集数据（使用rabbitmq） -->
<dependency>
    <groupId>io.zipkin.java</groupId>
    <artifactId>zipkin-autoconfigure-collector-rabbitmq</artifactId>
    <version>2.5.0</version>
</dependency>
```

相关配置

```
# zipkin数据保存到数据库中需要进行如下配置
zipkin:
  # 表示zipkin数据存储方式是mysql
  storage:
    type: mysql
  collector:
    rabbitmq:
      addresses: ${RABBIT_MQ_HOST:127.0.0.1}
      port: ${RABBIT_MQ_PORT:5672}
      password: guest
      username: guest
      queue: zipkin2
```

修改客户端POM、配置文件

添加依赖

```
<dependency>
    <groupId>org.springframework.amqp</groupId>
    <artifactId>spring-rabbit</artifactId>
</dependency>
```

相关配置

```
spring:
  zipkin:
    rabbitmq:
      # 默认队列名为zipkin，需要修改队列名可以修改此配置
      queue: zipkin2
```

示例：http://gitlab.utech.com/Vick.Zeng/trace.git




# 二、SpringBoot2.0后版本zipkin

关于 Zipkin 的服务端，在使用 Spring Boot 2.x 版本后，官方就不推荐自行定制编译了，反而是直接提供了编译好的 jar 包来给我们使用，详情请看 [upgrade to Spring Boot 2.0 NoClassDefFoundError UndertowEmbeddedServletContainerFactory · Issue #1962 · openzipkin/zipkin · GitHub](https://github.com/openzipkin/zipkin/issues/1962)

并且以前的```@EnableZipkinServer```也已经被打上了```@Deprecated```

示例：TODO

# 三、参考

https://windmt.com/2018/04/24/spring-cloud-12-sleuth-zipkin/

http://cloud.spring.io/spring-cloud-static/Finchley.RELEASE/multi/multi__introduction.html#_sleuth_with_zipkin_over_rabbitmq_or_kafka

https://gitee.com/minull/ace-security
