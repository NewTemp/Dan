### 什么是Spring boot

Spring Boot是由Pivotal团队提供的全新框架，其设计目的是用来简化新Spring应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。

### Spring boot 的优点

Spring Boot是基于Spring的一个轻量级框架，其特点是简单、快速和方便，非常适合用于微服务开发。

* 轻松创建独立的Spring应用程序。

* 内嵌Tomcat、jetty等web容器，不需要部署WAR文件。

* 提供一系列的“starter” 来简化的Maven配置。

* 开箱即用，尽可能自动配置Spring。

### 创建项目（IDEA）

\*\*1.创建一个项目 \*\*

!\[新建项目\]\([https://upload-images.jianshu.io/upload\_images/12984892-0012c9a3f389c68f.png?imageMogr2/auto-orient/strip\|imageView2/2/w/1240\](https://upload-images.jianshu.io/upload_images/12984892-0012c9a3f389c68f.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240\)\)

!\[选择Spring Initializr\]\([https://upload-images.jianshu.io/upload\_images/12984892-64ddbe088d8dac62.png?imageMogr2/auto-orient/strip\|imageView2/2/w/1240\](https://upload-images.jianshu.io/upload_images/12984892-64ddbe088d8dac62.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240\)\)

!\[填写项目名称，选择maven和java版本\]\([https://upload-images.jianshu.io/upload\_images/12984892-2ab53f58968250e9.png?imageMogr2/auto-orient/strip\|imageView2/2/w/1240\](https://upload-images.jianshu.io/upload_images/12984892-2ab53f58968250e9.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240\)\)

!\[选择Web\]\([https://upload-images.jianshu.io/upload\_images/12984892-25544c49cd835de8.png?imageMogr2/auto-orient/strip\|imageView2/2/w/1240\](https://upload-images.jianshu.io/upload_images/12984892-25544c49cd835de8.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240\)\)

创建完成后项目结构如下

!\[image.png\]\([https://upload-images.jianshu.io/upload\_images/12984892-02864b253e259fee.png?imageMogr2/auto-orient/strip\|imageView2/2/w/1240\](https://upload-images.jianshu.io/upload_images/12984892-02864b253e259fee.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240\)\)

---

\*\*2.添加依赖\*\*

找到pom.xml文件，加入依赖\(一般创建项目时会自动生成\)：

\`\`\`

&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;project xmlns="[http://maven.apache.org/POM/4.0.0](http://maven.apache.org/POM/4.0.0)" xmlns:xsi="[http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)"

```
     xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"&gt;

&lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;



&lt;groupId&gt;com.example&lt;/groupId&gt;

&lt;artifactId&gt;demo&lt;/artifactId&gt;

&lt;version&gt;0.0.1-SNAPSHOT&lt;/version&gt;

&lt;packaging&gt;jar&lt;/packaging&gt;



&lt;name&gt;demo&lt;/name&gt;

&lt;description&gt;Demo project for Spring Boot&lt;/description&gt;



&lt;parent&gt;

    &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;

    &lt;artifactId&gt;spring-boot-starter-parent&lt;/artifactId&gt;

    &lt;version&gt;2.0.3.RELEASE&lt;/version&gt;

    &lt;relativePath/&gt; &lt;!-- lookup parent from repository --&gt;

&lt;/parent&gt;



&lt;properties&gt;

    &lt;project.build.sourceEncoding&gt;UTF-8&lt;/project.build.sourceEncoding&gt;

    &lt;project.reporting.outputEncoding&gt;UTF-8&lt;/project.reporting.outputEncoding&gt;

    &lt;java.version&gt;1.8&lt;/java.version&gt;

&lt;/properties&gt;



&lt;dependencies&gt;

    &lt;dependency&gt;

        &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;

        &lt;artifactId&gt;spring-boot-starter-web&lt;/artifactId&gt;

    &lt;/dependency&gt;



    &lt;dependency&gt;

        &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;

        &lt;artifactId&gt;spring-boot-starter-test&lt;/artifactId&gt;

        &lt;scope&gt;test&lt;/scope&gt;

    &lt;/dependency&gt;

&lt;/dependencies&gt;



&lt;build&gt;

    &lt;plugins&gt;

        &lt;plugin&gt;

            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;

            &lt;artifactId&gt;spring-boot-maven-plugin&lt;/artifactId&gt;

        &lt;/plugin&gt;

    &lt;/plugins&gt;

&lt;/build&gt;
```

&lt;/project&gt;

\`\`\`

其他依赖根据项目需求添加。

\*\*\*

\*\*3.创建目录和配置文件\*\*

创建 src/main/resources 源文件目录，并在该目录下创建 application.properties 文件、static 和 templates 的文件夹。

* application.properties：用于配置项目运行所需的配置数据。

* static：用于存放静态资源，如：css、js、图片等。

* templates：用于存放模板文件。

!\[resources文件\]\([https://upload-images.jianshu.io/upload\_images/12984892-f3826161bcbf0e41.png?imageMogr2/auto-orient/strip\|imageView2/2/w/1240\](https://upload-images.jianshu.io/upload_images/12984892-f3826161bcbf0e41.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240\)\)

---

\*\*4.创建启动类\*\*

在 src&gt;&gt;main&gt;&gt;java&gt;&gt;com.example.demo&gt;&gt;DemoApplication中编写以下代码：

\`\`\`

package com.example.demo;

import org.springframework.boot.SpringApplication;

import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication

public class DemoApplication {

```
public static void main\(String\[\] args\) {

    SpringApplication.run\(DemoApplication.class, args\);

}
```

}

\`\`\`

---

\*\*5.案例演示\*\*

\`\`\`

@RestController

public class hello {

```
@GetMapping\("/helloworld"\)

public String helloworld\(\){

    return "helloworld";

}
```

}

\`\`\`

!\[案例演示\]\([https://upload-images.jianshu.io/upload\_images/12984892-1ee0575b28fc5693.png?imageMogr2/auto-orient/strip\|imageView2/2/w/1240\](https://upload-images.jianshu.io/upload_images/12984892-1ee0575b28fc5693.png?imageMogr2/auto-orient/strip|imageView2/2/w/1240\)\)

