title: spring-boot使用
date: 2016-08-10 20:22:25
toc: true
categories:
- 学习
tags:
- Java
---

因公司项目重构，记录下spring-boot构建spring-mvc工程。
<!--more-->
## 工程的结构，使用maven java工程
![](http://120.24.60.216:4000/img/20160810202223.png)

## 添加工程依赖的mvnbao

```bash
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>${org.springframework-boot-version}</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <version>${org.springframework-boot-version}</version>
            <scope>test</scope>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.apache.httpcomponents/httpclient -->
        <dependency>
            <groupId>org.apache.httpcomponents</groupId>
            <artifactId>httpclient</artifactId>
            <version>4.5.2</version>
        </dependency>
```
## spring配置文件
```bash
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>
    <context:property-placeholder/>

</beans>
```
## 工程启动入口
```bash
@SpringBootApplication
@ImportResource("classpath:application-context.xml")
public class SpringBoot {
    public static void main(String[] args) {
        SpringApplication.run(SpringBoot.class, args);
    }
}
```
## spring controller 配置
```bash
@RestController
public class DisonController {

    @RequestMapping("/dison")
    public String test() {
        return "hello, dison";
    }

}
```

好了，到这就实现了spring-boot！


转发表明出现，谢谢！