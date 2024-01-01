[Spring官网](https://spring.io/ “spring”)



# SpringFramework

主要功能模块

| 功能模块       | 功能介绍                              |
| -------------- | ------------------------------------- |
| Core Container | 环境下使用任何功能都必须基于 IOC 容器 |
| AOP&Aspects    | 面向切面编程                          |
| TX             | 声明式事务管理                        |
| Spring MVC     | 提供了面向Web应用程序的集成功能       |



# SpringIoC

**SpringIoC(Inversion of Control)控制反转**

Spring IoC 容器，负责实例化、配置和组装 bean（组件）。容器通过读取配置元数据来获取有关要实例化、配置和组装组件的指令。配置元数据以 XML、Java 注解或 Java 代码形式表现。它允许表达组成应用程序的组件以及这些组件之间丰富的相互依赖关系



## SpringIoC容器和容器实现类

**SpringIoc容器接口**：

`BeanFactory` 接口提供了一种高级配置机制，能够管理任何类型的对象，它是SpringIoC容器标准化超接口！

`ApplicationContext` 是 `BeanFactory` 的子接口。它**扩展**了以下功能：

| 类型名                                 | 简介                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| ClassPathXmlApplicationContext         | 通过读取类路径下的 XML 格式的**配置文件**创建 IOC 容器对象   |
| FileSystemXmlApplicationContext        | 通过文件系统路径读取 XML 格式的**配置文件**创建 IOC 容器对象 |
| **AnnotationConfigApplicationContext** | 通过读取**Java配置类**创建 IOC 容器对象                      |
| **WebApplicationContext**              | 专门为 Web 应用准备，基于 Web 环境创建 **IOC 容器对象**，并将对象引入存入 ServletContext 域中 |

```mermaid
graph TD
A[BeanFactory] --> B[ApplicationContext]
B --> C[ClassPathXmlApplicationContext]
B --> D[FileSystemXmlApplicationContext]
B --> E[AnnotationConfigApplicationContext]
B --> F[WebApplicationContext]

```



### Spring IoC 容器管理配置方式

Spring框架提供了多种配置方式：XML配置方式、**注解方式**和**Java配置类**方式

1. XML配置方式：是Spring框架最早的配置方式之一，通过在XML文件中定义Bean及其依赖关系、Bean的作用域等信息，让Spring IoC容器来管理Bean之间的依赖关系。该方式从Spring框架的第一版开始提供支持
2. 注解方式：从Spring 2.5版本开始提供支持，可以通过在Bean类上使用注解来代替XML配置文件中的配置信息。通过在Bean类上加上相应的注解（如@Component, @Service, @Autowired等），将Bean注册到Spring IoC容器中，这样Spring IoC容器就可以管理这些Bean之间的依赖关系
3. **Java配置类**方式：从Spring 3.0版本开始提供支持，通过Java类来定义Bean、Bean之间的依赖关系和配置信息，从而代替XML配置文件的方式。Java配置类是一种使用Java编写配置信息的方式，通过@Configuration、@Bean等注解来实现Bean和依赖关系的配置























# 自动装配

```xml
<!--
    scope: singleton | prototype
    singleton: 单例模式 （默认）
    prototype: 多例模式

    通过 userController 控制 userService 控制 userDao
    实现三层控制
    autowire: default | no | byType | byName
        default | no: 不装配(默认值)
        byType: 根据赋值属性的类型，在 IOC 容器中 匹配某个 bean (即class中返回的类型),为属性赋值 (用的最多)
            IOC 容器中有且只有一个类型一样的 bean 才可以
        byName: 根据将要赋值属性的属性名作为 bean 的 id 在 IOC 容器中匹配某个 bean, 为属性赋值
-->
<bean id="userController" class="com.spring.controller.UserController" autowire="byType">
    <!--原始方法，不使用装配-->
    <!--<property name="userService" ref="userService"></property>-->
</bean>

<bean id="userService" class="com.spring.service.impl.UserServiceImpl">
    <property name="userDao" ref="userDao"></property>
</bean>

<bean id="userDao" class="com.spring.dao.impl.UserDaoImpl"></bean>
```



# 组件扫描

```java
/**
 * 注解
 * @Component: 将类标识为普通组件
 * @Controller: 将类标识为控制层组件
 * @Service: 将类标识为业务层组件
 * @Repository: 将类标识为持久层层组件
 * 此时 bean 的 id 默认值为 类的小驼峰
 *
 * @Autowired 自动装配
 * 1. 标识在 成员变量上
 * 2. 标识在 有参构造方法上
 * 3. 标识在 成员变量的set方法上
 *
 * @Autowired 自动装配原理
 *  1. 默认使用 byType 的方式，在 IOC 容器中通过类型匹配某个 bean 为属性赋值
 *  2. 若 byType 无法匹配则自动转为 byName 的方式
 *  3. 若 byType 和 byName 都无法匹配 则在 @Autowired注解上使用 @Qualifier("")
 *      通过 value 值指定某个 bean 的id. 此时使用的是构造方法注入，注意构造方法的使用
 */
```

```xml
<!--
    context:exclude-filter 排除扫描
    type=annotation | assignable
        annotation: 根据 注解类型 排除
        assignable: 根据 类的类型 排除

    context:include-filter 包含扫描
        需要设置 use-default-filters="false"
            true: （默认值） 所设置的包下所有的类都需要扫描，此时使用 context:exclude-filter
            false: 所设置的包下所有的类都不需要扫描，此时使用 context:include-filter
-->

<!--扫描组件-->
<context:component-scan base-package="com.spring" use-default-filters="true">
    <!--<context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>-->
    <!--<context:exclude-filter type="assignable" expression="com.spring.controller.UserController"/>-->
    <!--<context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>-->
</context:component-scan>
```



# 属性注入(几乎不用)

```xml
<!--获取Student反射的无参构造-->
<bean id="student" class="com.spring.bean.Student">
    <!--
        属性依赖注入
        property: 通过成员变量的 set 方法赋值
        name: 属性名
        value: 值
    -->
    <property name="sid" value="1001"></property>
    <property name="sname" value="张三"></property>
    <property name="age" value="23"></property>
    <property name="gender" value="男"></property>

    <!--当属性是数组的时候-->
    <property name="hobby">
        <array>
            <value>打游戏</value>
            <value>吃鸡</value>
            <value>王者</value>
        </array>
    </property>

    <!--当属性是 Map 的时候-->
    <property name="teacherMap" ref="teacherMap"></property>
    <!--<property name="teacherMap">
        <map>
            <entry key="老师1" value-ref="teacher"></entry>
            <entry key="老师2" value-ref="teacher"></entry>
        </map>
    </property>-->

    <!--当属性是个类的时候-->
    <!--
        1. 引用外部 bean
        2. 使用内部 bean
    -->
    <!--<property name="clazz" ref="clazz"></property>-->
    <property name="clazz">
        <!--内部 bean 不属于 IOC 容器-->
        <bean id="clazzInner" class="com.spring.bean.Clazz">
            <property name="cid" value="1"></property>
            <property name="cname" value="电信"></property>
        </bean>
    </property>

    <!--
        构造方法注入
        <: <
        >: >
        null: <null/>
    -->
    <!--<constructor-arg value="1002"></constructor-arg>
    <constructor-arg value="李四"></constructor-arg>
    <constructor-arg value="18"></constructor-arg>
    <constructor-arg value="男" name="gender"></constructor-arg>-->
</bean>

<bean id="clazz" class="com.spring.bean.Clazz">
    <property name="cid" value="1"></property>
    <property name="cname" value="电信"></property>
    <!--当属性是个集合的时候-->
    <property name="student" ref="studentList"></property>
    <!--<property name="student">
        <list>
            <ref bean="student"></ref>
            <ref bean="student"></ref>
            <ref bean="student"></ref>
        </list>
    </property>-->
</bean>

<bean id="teacher" class="com.spring.bean.Teacher">
    <property name="tid" value="111"></property>
    <property name="tname" value="老师"></property>
</bean>

<util:list id="studentList">
    <ref bean="student"></ref>
    <ref bean="student"></ref>
    <ref bean="student"></ref>
</util:list>

<util:map id="teacherMap">
    <entry key="老师1" value-ref="teacher"></entry>
    <entry key="老师1" value-ref="teacher"></entry>
</util:map>
```



# 获取bean

```java
/**
 * 获取 bean
 * 1. 根据 id 获取， 需要强转类型
 * 2. 根据类型获取， 要求 IOC 容器中有且只有一个该类型的 bean (常用)
 * 3. 根据 id 和 类型 获取。
 *
 * 根据类型获取 bean 时，在满足 bean 唯一的前提下，其实只看： [对象 instanceof 指定类型] 的
 * 返回结果，只要返回 true 就可以和指定类型匹配，(即获取该类的实现接口也能获取到 bean)
 */

/**
 * bean 的生命周期
 *  实例化
 *  依赖注入
 *  初始化
 *  销毁
 *
 * 单例模式在 获取 IOC 容器的时候执行生命周期函数 前三个步骤
 * 多例模式在 获取 IOC 容器中的 bean 的时候执行 前三个步骤
 */
```



# 事务管理器

```java
/**
 * @Transactional
 *  isolation: 事务的隔离级别
 *  propagation: REQUIRED | REQUIRES_NEW 设置事务的传播行为
 *      REQUIRED: 默认值 利用 参照调用方法的事务
 *      REQUIRES_NEW: 以自身方法为一个事务
 */
@Override
@Transactional(
        readOnly = false,
        timeout = 3,
        isolation = Isolation.DEFAULT,
        propagation = Propagation.REQUIRES_NEW
)
```



# AOP

AOP (Aspect Oriented Programming) 是一种设计思想，是软件设计领域中的面向切面编程，它是面向对象编程的一种补充和完善，它以通过预编译方式和运行期动态代理方式实现在不修改源代码的情况下给程序动态统一添加额外功能的一种技术。

- 抽取一些非核心功能的公共代码（例如日志）放到一个类里面。这个类就是切面

@Aspect // 将当前组件标识为切面

@Order(1) // 切面优先级，值越小，优先级越高

- 切面：封装横切关注点的类
