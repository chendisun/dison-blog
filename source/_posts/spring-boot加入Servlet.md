title: spring-boot加入Servlet
date: 2016-08-10 22:02:20
categories:
- 学习
tags:
- Java
---

因公司项目重构，之前使用mvn-web工程创建项目，现在使用spring-boot创建项目，现在的新接口都是使用spring-mvc写，但是之前的大部分的接口是使用Servlet作为入口的，使用在迁移代码无可避免用使用Servlet，所以在这记录下spring-boot使用Servlet的方法。
<!--more-->
## 在 SpringBootApplication 上使用@ServletComponentScan 注解

```bash
@ServletComponentScan
@SpringBootApplication
@ImportResource("classpath:application-context.xml")
public class SpringBoot {
    public static void main(String[] args) {
        SpringApplication.run(SpringBoot.class, args);
    }
}
```
## 使用注解注册Servlet
```bash
@WebServlet(urlPatterns="/test", description="Servlet的说明") // 不指定name的情况下，name默认值为类全路径，即com.dison.spring.boot.servlet.TestServlet
public class TestServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletOutputStream outputStream = resp.getOutputStream();
        outputStream.write("sussecc".getBytes());
        outputStream.close();
    }
}
```
这简单的两步，就实现了在spring-boot中使用Servlet


# 转发表明出现，谢谢！