title: spring-boot加入自定义拦截器 
date: 2016-08-11 23:35:24
categories:
- Spring
tags:
- Java
---

使用spring-boot做Web开发中，我们除了使用 Filter 来过滤请求外，还可以使用Spring提供的HandlerInterceptor（拦截器）。
<!--more-->
HandlerInterceptor 的功能跟过滤器类似，但是提供更精细的的控制能力：在request被响应之前、request被响应之后、视图渲染之前以及request全部结束之后。我们不能通过拦截器修改request内容，但是可以通过抛出异常（或者返回false）来暂停request的执行。

下面是实现过程：
## 创建我们自己的拦截器类并实现 HandlerInterceptor 接口。
```bash
package com.dison.spring.boot.interceptor;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * 自定义spring-mvc拦截器
 */
public class SpringMvcInterceptor implements HandlerInterceptor {
    /**
     * 在请求处理之前进行调用（Controller方法调用之前）
     *
     * @param httpServletRequest
     * @param httpServletResponse
     * @param o
     * @return
     * @throws Exception
     */
    @Override
    public boolean preHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o) throws Exception {
        System.out.println("SpringMvcInterceptor.preHandle");
        return true;
    }

    /**
     *
     * 请求处理之后进行调用，但是在视图被渲染之前（Controller方法调用之后）
     *
     * @param httpServletRequest
     * @param httpServletResponse
     * @param o
     * @param modelAndView
     * @throws Exception
     */
    @Override
    public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {
        System.out.println("SpringMvcInterceptor.postHandle");
    }

    /**
     * 在整个请求结束之后被调用，也就是在DispatcherServlet 渲染了对应的视图之后执行（主要是用于进行资源清理工作）
     *
     * @param httpServletRequest
     * @param httpServletResponse
     * @param o
     * @param e
     * @throws Exception
     */
    @Override
    public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {
        System.out.println("SpringMvcInterceptor.afterCompletion");
    }
}
```
## 创建一个Java类继承WebMvcConfigurerAdapter，并重写 addInterceptors 方法。并实例化我们自定义的拦截器，然后将对像手动添加到拦截器链中（在addInterceptors方法中添加）
```bash
package com.dison.spring.boot.interceptor;

import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurerAdapter;

/**
 *
 */
@Configuration
public class WebAppConfigurer extends WebMvcConfigurerAdapter {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        // 多个拦截器组成一个拦截器链
        registry.addInterceptor(new SpringMvcInterceptor()).addPathPatterns("/**");
        super.addInterceptors(registry);
    }
}
```