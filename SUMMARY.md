# Summary

## 一堆规范

* [Introduction](README.md)
* [项目搭建合规指引](xiang-mu-da-jian-he-gui-zhi-yin.md)
  * [集成Eureka](xiang-mu-da-jian-he-gui-zhi-yin/ji-cheng-eureka.md)
  * [GIT提交规范](xiang-mu-da-jian-he-gui-zhi-yin/gitti-jiao-gui-fan.md)
  * [集成Log](xiang-mu-da-jian-he-gui-zhi-yin/ji-cheng-log.md)
  * [集成Config](xiang-mu-da-jian-he-gui-zhi-yin/ji-chengconfig.md)
  * [多环境配置](xiang-mu-da-jian-he-gui-zhi-yin/duo-huan-jing-pei-zhi.md)
  * [提供Actuactor集成](xiang-mu-da-jian-he-gui-zhi-yin/ti-gong-actuactor-ji-cheng.md)
  * [集成Redis](xiang-mu-da-jian-he-gui-zhi-yin/ji-cheng-redis.md)
* [Drools规则引擎](droolsgui-ze-yin-qing.md)

## API

* [Agg\(Flight\)](api/aggflight.md)
  * [API V1](api/aggflight/api.md)
    * [flightSerach](api/aggflight/api/flightserach.md)
    * [flightRoll](api/aggflight/api/flightroll.md)
* [Travelport](api/travelport.md)
  * [wiki](api/travelport/wiki.md)
    * [LowFareSearch](api/travelport/wiki/lowfaresearch.md)
    * [AirPrice](api/travelport/wiki/airprice.md)
    * [Action Status](api/travelport/wiki/action-status.md)
    * [Connection Segment Logic](api/travelport/wiki/Connection&Segment.md)
    * [Form of Payment](api/travelport/wiki/form-of-payment.md)
    * [UR&PNR](api/travelport/wiki/UR&PNR.md)
    * [SSR](api/travelport/wiki/ssr.md)
      * [护照\(DOCS\)](api/travelport/wiki/ssr/hu-716728-docs.md)
      * [地址\(DOCA\)](api/travelport/wiki/ssr/di-574028-doca.md)
      * [签证\(DOCO\)](api/travelport/wiki/ssr/qian-8bc128-doco.md)
      * [状态码](api/travelport/wiki/ssr/zhuang-tai-ma.md)
      * [BookTravelName](api/travelport/wiki/ssr/booktravelname.md)
    * [运价](api/travelport/wiki/yun-jia.md)
    * [Queue](api/travelport/wiki/queue.md)
    * 乘客数据传递
  * [shopping](api/travelport/shopping.md)
  * [V1](api/travelport/v1.md)
* [Kount](api/kount.md)
  * [V1](api/kount/v1.md)
    * [Starter](api/kount/starter.md)
    * [Khash](api/kount/v1/khash.md)
    * [TSA Interfaces](api/kount/tsa-interfaces.md)
    * [risk-ms设计](api/kount/risk-msshe-ji.md)
* [CouponCode](api/couponcode.md)
  * [V1](api/couponcode/v1.md)
    * [业务规则](api/couponcode/v1/ye-wu-gui-ze.md)
    * [架构设计](api/couponcode/v1/jia-gou-she-ji.md)
    * [技术点](api/couponcode/v1/ji-zhu-dian.md)
* [Voucher](api/voucher.md)
  * [V1](api/voucher/v1.md)
    * [API接口](api/voucher/v1/apijie-kou.md)
    * [TSA接口逻辑](api/voucher/v1/tsajie-kou-luo-ji.md)
    * [加密解密服务](api/voucher/v1/jia-mi-jie-mi-fu-wu.md)
    * [架构设计](api/voucher/v1/jia-gou-she-ji.md)
* [Insurance Api](insurance.md)

## DEV Service

* [DEV Service](DEV-Service/README.md)
  * [Linux Command](DEV-Service/Linux-Command/Linux-Command.md)
  * [Service Building](DEV-Service/Service-Building/README.md)
  * [Redis](DEV-Service/Linux-Command/redis.md)
  * [Rabbit](DEV-Service/Linux-Command/rabbit.md)
  * [Mongo](DEV-Service/Linux-Command/mongo.md)
  * [ELK](DEV-Service/Linux-Command/elk.md)
  * [Zookeeper](DEV-Service/Linux-Command/zookeeper.md)
  * [Jenkins](DEV-Service/Linux-Command/jenkins.md)
  * [Mysql](DEV-Service/Linux-Command/mysql.md)
  * [docker](DEV-Service/Linux-Command/docker.md)

## Spring Boot

* [Spring Boot](Spring-Boot/README.md)
  * [Spring boot 注解](Spring-Boot/Spring-boot注解.md)
  * [Spring Security使用](Spring-Boot/spring-security.md)

## Spring Cloud

* [Spring Cloud](Spring-Cloud/README.md)
  * [Spring Cloud 网关Zuul](Spring-Cloud/spring-cloud-wang-guan-zuul.md)
  * [Spring Cloud 负载均衡Ribbon、服务熔断Hystrix](Spring-Cloud/Feign.md)
  * [Spring Cloud 链路跟踪Zipkin](Spring-Cloud/Zipkin.md)
  * [Spring Cloud 服务实时监控Hystrix Dashboard、Turbine](Spring-Cloud/Turbine.md)

## RabbitMq

* [原理篇](rabbitmq/yuan-li.md)
* [操作篇](rabbitmq/cao-zuo-pian.md)
  * [Start](rabbitmq/cao-zuo-pian/start.md)
  * [RabbitMQ的安装及使用](DEV-Service/Linux-Command/linuxxia-an-zhuang-rabbitmq.md)

