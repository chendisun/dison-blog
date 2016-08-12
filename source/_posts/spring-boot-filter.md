title: spring-boot加入自定义过滤器
date: 2016-08-12 10:20:17
categories:
- Spring
tags:
- Java
---

使用spring-boot做Web开发中，我们大多情况下会添加自己的过滤器过滤一些数据。
<!--more-->
以下面是记录实现filter的过程：
## 创建我们自己的filter类并实现 Filter 接口。
```java
import javax.servlet.*;
import java.io.IOException;

public class DisonFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("初始化DisonFilter");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("执行DisonFilter");
        filterChain.doFilter(servletRequest, servletResponse);
    }

    @Override
    public void destroy() {
        System.out.println("销毁DisonFilter");
    }
}
```
## 在spring配置文件中配置filter和注册filter
```java
<bean id="disonFilter" class="com.dison.spring.boot.filter.DisonFilter" />
<bean class="org.springframework.boot.web.servlet.FilterRegistrationBean">
    <property name="filter" ref="disonFilter"/>
    <property name="urlPatterns" value="/dison"/>
    <property name="name" value="disonFilter"/>
</bean>
```

# 转发表明出现，谢谢！