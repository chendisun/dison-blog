title: spring-boot实现Servlet3.0异步请求
date: 2016-08-22 11:11:25
categories:
- 学习
tags:
- Java
---

在Spring3.2及以后版本中增加了对请求的异步处理，旨在提高请求的处理速度，降低服务端性能的消耗。
<!--more-->

在实际开发中，不可避免的会有一些请求是很耗时的，当在并发请求的情况下，为了避免服务端的连接池被长期占用而引起性能问题，servlet3之后在请求调用后生成一个非web的服务线程来处理，增加web服务器的吞吐量。这就是Servlet3.0新增的异步处理，而Spring也在此基础上做了封装处理。

下面简单记录一下如何在spring-boot中应用异步请求，分别实现原始servlet的异步请求和controller的异步请求实现。

## @WebFilter和@WebServlet注解中的要设置asyncSupported = true的属性
异步处理的servlet若存在过滤器，则过滤器的注解@WebFilter应设置asyncSupported=true，
不然会报错 A filter or servlet of the current chain does not support asynchronous operations. 
## 在spring-boot的启动入口加@EnableAsync注解 
```java
@ServletComponentScan
@SpringBootApplication
@ImportResource("classpath:application-context.xml")
@EnableAsync
public class SpringBoot {
    public static void main(String[] args) {
        SpringApplication.run(SpringBoot.class, args);
    }
}
```
## 原始servlet的实现方式
```java
@WebServlet(urlPatterns="/async", asyncSupported = true)
public class AsyncServlet extends HttpServlet {

    private final Queue<AsyncContext> asyncContexts = new LinkedBlockingDeque<>();

    private final Thread thread = new Thread() {
        @Override
        public void run() {
            while (!thread.isInterrupted()) {
                try {
                    while (!asyncContexts.isEmpty()) {
                        TimeUnit.SECONDS.sleep(5);
                        AsyncContext asyncContext = asyncContexts.poll();
                        HttpServletResponse res = (HttpServletResponse) asyncContext.getResponse();
                        res.getWriter().write("dison, async is ok!!!");
                        res.setStatus(HttpServletResponse.SC_OK);
                        asyncContext.complete();
                    }
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                    e.printStackTrace();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    };

    @Override
    public void init() throws ServletException {
        super.init();
        thread.start();
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        AsyncContext asyncContext = req.startAsync();
        asyncContext.setTimeout(20 * 1000L);
        asyncContexts.offer(asyncContext);
    }

    @Override
    public void destroy() {
        super.destroy();
        thread.interrupt();
    }
}
```
## Controller实现方式
```java
@RestController
public class AsyncController {

    @RequestMapping("/asyncDison")
    public Callable<String> asynDison() {
        return new Callable<String>() {
            @Override
            public String call() throws Exception {
                return "async dison is ok !!!!";
            }
        };
    }

}
```

转发表明出处，谢谢！