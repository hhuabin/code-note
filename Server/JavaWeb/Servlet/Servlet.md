# Servlet

**Servlet (server applet) 是运行在服务端 tomcat 的 Java 小程序，是sun司提供一套定义动态资源规范；从代码层面上来进 Servlet 就是一个接口**

- 不是所有的JAVA类都能用于处理客户端请求，能处理客户端请求并做出响应的一套技术标准就是Servlet
- Servlet是运行在服务端的，所以 Servlet必须在WEB项目中开发且在Tomcat这样的服务容器中运行



## HttpServletRequest和HttpServletResponse

请求响应与HttpServletRequest和HttpServletResponse之间的对应关系：

1. tomcat 接收到请求后，会将请求报文的信息转换一个`HttpServletRequest`对象该对象中包含了请求中的**所有信息**、**请求行**、**请求头**、**请求体**

2.  tomcat 同时创建了一个`HttpServletResponse`对象，该对象用于承装要响应给客户端的信息，后面，该对象会被转换成响应的**报文**、**响应行**、**响应头**、**响应体**

3. tomcat根据请求中的资源路径找到对应的servlet，将servlet实例化调用service方法，同时将HttpServletRequest 和HttpServletResponse对象传入

   ```java
   package com.boot.servlet;
   
   public class userServlet extends HttpServlet {
   
       // http://localhost:5000/demo_war_exploded/servlet?username=bin
       @Override
       protected void service(HttpServletRequest request, HttpServletResponse response) throws IOException {
           String username = request.getParameter("username");
           PrintWriter writer = response.getWriter();
           writer.write(username);
       }
   }
   ```
   
   1. 从request对象中获取请求的所有信息（参数）
   2. 根据参数生成要响应给客户端的数据
   3. 将响应的数据放入`response`对象



# Searvlet 的生命周期

1. 实例化 **ServletLifeCycle()**
2. 初始化 **init()**
3. 接收请求、处理请求（服务）**service()**
4. 销毁 **destroy()**

Servlet 在 `Tomcat` 中是单例的，不建议在 `service ` 方法中修改成员变量，会引发线程安全问题



Servlet中的核心方法：`init()` `service()` `destroy()`

```java
public interface Servlet {
    
    void init(ServletConfig var1) throws ServletException;

    void service(ServletRequest request, ServletResponse response) throws ServletException, IOException;

    void destroy();
}
```



一般每个请求会执行相对应的 servlet。

**DefaultServlet**：默认的 servlet，当匹配不上其他的 servlet，默认匹配上它，一般用于处理静态资源。

```xml
<servlet>
    <servlet-name>default</servlet-name>
    <servlet-class>org.apache.catalina.servlets.DefaultServlet</servlet-class>
</servlet>
```





# HttpServletRequest

1. 转发请求

   在Servlet中，使用`RequestDispatcher`对象来进行请求转发。以下是一个简单的请求转发

   ```java
   // 获取RequestDispatcher对象，参数是转发的目标路径
   RequestDispatcher dispatcher = request.getRequestDispatcher("/targetServlet");
   
   // 执行请求转发
   dispatcher.forward(request, response);
   ```

   



# HttpServletResponse

1. 设置响应头的`Content-Type`

   ```java
   @Override
   protected void service(HttpServletRequest request, HttpServletResponse response) throws IOException {
       String _html = "<h1>hhaubin</h1>";
       response.setHeader("Content-Type", "text/html");
       PrintWriter writer = response.getWriter();
       writer.write(_html);
   }
   ```

   


