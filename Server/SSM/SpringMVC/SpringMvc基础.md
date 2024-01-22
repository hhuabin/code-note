# 使用

1. Controller

   ```java
   @Controller
   public class HelloController {
   
       // http://localhost:5000/springmvc/hello
       @RequestMapping("springmvc/hello")
       @ResponseBody
       public String hello() {
           System.out.println("Hello Controller");
           return "hello springmvc";
       }
   }
   ```

2. 配置文件

   ```java
   @Configuration
   @ComponentScan("com.springmvc")
   public class MvcConfig {
   
       @Bean
       public RequestMappingHandlerMapping handlerMapping() {
           return new RequestMappingHandlerMapping();
       }
   
       @Bean
       public RequestMappingHandlerAdapter handlerAdapter() {
           return new RequestMappingHandlerAdapter();
       }
   }
   ```

3. Tomcat引入配置文件使用(**Tomcat10以上**)

   ```java
   //TODO: SpringMVC提供的接口,是替代web.xml的方案,更方便实现完全注解方式ssm处理!
   //TODO: Springmvc框架会自动检查当前类的实现类,会自动加载 getRootConfigClasses / getServletConfigClasses 提供的配置类
   //TODO: getServletMappings 返回的地址 设置DispatherServlet对应处理的地址
   public class SpringMvcInt extends AbstractAnnotationConfigDispatcherServletInitializer {
   
       @Override
       protected Class<?>[] getRootConfigClasses() {
           return new Class[0];
       }
   
       @Override
       protected Class<?>[] getServletConfigClasses() {
           return new Class[]{MvcConfig.class};
       }
   
       @Override
       protected String[] getServletMappings() {
           return new String[]{"/"};
       }
   }
   ```

4. 配置Tomcat即可运行项目

   ```java
   // http://localhost:5000/springmvc/hello
   ```

   