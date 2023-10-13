# Servlet

Servlet中的核心方法：init(), service(), destroy

```java
public interface Servlet {
    
    void init(ServletConfig var1) throws ServletException;

    void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;

    void destroy();
}
```



# 转发请求

在Servlet中，使用`RequestDispatcher`对象来进行请求转发。以下是一个简单的请求转发

```java
// 获取RequestDispatcher对象，参数是转发的目标路径
RequestDispatcher dispatcher = request.getRequestDispatcher("/targetServlet");

// 执行请求转发
dispatcher.forward(request, response);
```

