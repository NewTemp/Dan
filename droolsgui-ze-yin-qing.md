## **一、Drools简介**

        Drools 是用Java语言编写的开放源码规则引擎，使用Rete算法对所编写的规则求值。Drools允许使用声明方式表达业务逻辑。可以使用非XML的本地语言编写规则，从而便于学习和理解。并且，还可以将Java代码直接嵌入到规则文件中。

Drools相关概念：

* 事实（Fact）：对象之间及对象属性之间的关系。
* 规则（rule）：是由条件和结论构成的推理语句，一般表示为if...Then。一个规则的if部分称为LHS，then部分称为RHS。
* 模式（module）：就是指IF语句的条件。这里IF条件可能是有几个更小的条件组成的大条件。模式就是指的不能在继续分割下去的最小的原子条件。

## **二、Drools简单实例**

1、在pom.xml文件中添加相关的依赖包。

```
<parent>
       <groupId>org.drools</groupId>
       <artifactId>drools</artifactId>
       <version>7.10.0-SNAPSHOT</version>
</parent>
<dependencies>
        <!-- Internal dependencies -->
        <dependency>
            <groupId>org.kie</groupId>
            <artifactId>kie-api</artifactId>
        </dependency>
        <dependency>
            <groupId>org.drools</groupId>
            <artifactId>drools-core</artifactId>
        </dependency>
        <dependency>
            <groupId>org.drools</groupId>
            <artifactId>drools-compiler</artifactId>
        </dependency>
        <dependency>
            <groupId>org.drools</groupId>
            <artifactId>drools-decisiontables</artifactId>
        </dependency>
        <dependency>
            <groupId>org.drools</groupId>
            <artifactId>drools-templates</artifactId>
        </dependency>
        <dependency>
            <groupId>org.kie</groupId>
            <artifactId>kie-internal</artifactId>
        </dependency>
</dependencies>
```

2、创建一个Person实体类

```
package org.drools.examples.test;

public class Person {
    private String name;
    private int age;
    private String desc;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getDesc() {
        return desc;
    }

    public void setDesc(String desc) {
        this.desc = desc;
    }

    public String toString() {
        return "[name=" + name + ",age=" + age + ",desc=" + desc + "]";
    }
}
```

3、在 resources 目录下创建一个package存放创建的规则文件PersonRule.drl，内容如下：

```
package com.example.person;

import org.drools.examples.test.Person;
function void printName(String name, String desc) {
	System.out.println("name:" + name + " desc:" + desc);
}

rule "boy"
   salience 1
   when
      $p: Person(age > 0);
   then
      $p.setDesc("少年");
      retract($p);
      printName($p.getName(), $p.getDesc());
end

rule "youth"
    salience 2
    when
      $p: Person(age > 12);
    then
      $p.setDesc("青年");
      retract($p);
      printName($p.getName(), $p.getDesc());
end

rule "midlife"
    salience 3
    when
      $p: Person(age > 24);
    then
      $p.setDesc("中年");
      retract($p);
      printName($p.getName(), $p.getDesc());
end

rule "old"
    lock - on - active true
    salience 5
    when
      $p: Person(age > 60 && age < 80)
    then
      $p.setDesc("老年");
      update($p);
      printName($p.getName(), $p.getDesc());
end
```

4、在 src/main/resources/META-INF/ 目录下创建 kmodule.xml 文件，kmodule.xml 用来描述知识库资源的选择及知识库与会话的配置，内容如下：

```
<?xml version="1.0" encoding="UTF-8"?>
<kmodule xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://www.drools.org/xsd/kmodule">
    <kbase name="simpleRuleTest" packages="org.drools.examples.test">
        <ksession name="simpleRuleKSession"/>
    </kbase>
</kmodule>
```

（1）可以包含多个kbase,但是name的值不能重名；

（2）packages：对应src/main/resources/下存放规则文件的文件夹名称，可定义多个包，用逗号隔开；

（3）每个kbase里的ksession都有一个name，任意字符串但不能重名，可以有多个；

5、创建测试类PersonTest，内容如下：

```
package org.drools.examples.test;

import org.kie.api.KieServices;
import org.kie.api.runtime.KieContainer;
import org.kie.api.runtime.KieSession;

public class PersonTest {
    static KieSession getSession() {
        KieServices ks = KieServices.Factory.get();
        KieContainer kc = ks.getKieClasspathContainer();
        return kc.newKieSession("simpleRuleKSession");
    }


    public static void run() {
        KieSession ks = getSession();

        Person p1 = new Person("白展堂", 68);
        Person p2 = new Person("李大嘴", 32);
        Person p3 = new Person("佟湘玉", 18);
        Person p4 = new Person("郭芙蓉", 8);
        Person p5 = new Person("祝无双", 66);

        System.out.println("before p1 : " + p1);
        System.out.println("before p2 : " + p2);
        System.out.println("before p3 : " + p3);
        System.out.println("before p4 : " + p4);
        ks.insert(p1);
        ks.insert(p2);
        ks.insert(p3);
        ks.insert(p4);
        ks.insert(p5);

        int count = ks.fireAllRules();

        System.out.println("总执行了" + count + "条规则------------------------------");
        System.out.println("after p1 : " + p1);
        System.out.println("after p2 : " + p2);
        System.out.println("after p3 : " + p3);
        System.out.println("after p4 : " + p4);
        System.out.println("after p5 : " + p5);
        ks.dispose();
    }

    public static void main(String[] args) {
        run();
    }
}
```

6、运行结果如下：

![](/assets/1533797017%281%29.png)

## **三、Drools规则语法**

1、规则文件

一个标准的规则文件的结构代码包含如下部分：

（1）package package-name\(包名，必须的，不必和物理路径一致\)

（2）import 需要导入Java Bean的完整路径

（3）globals \(全局变量\)



















