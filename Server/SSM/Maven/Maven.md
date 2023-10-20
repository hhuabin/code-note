# 官网

[Maven官网](https://maven.apache.org "Maven")

[Maven仓库](https://mvnrepository.com "mvnrepository")



# 配置

1. 下载`Maven`解压
2. 在`/conf/settings.xml`下修改，仓库存储地址，阿里云镜像等3处
3. 改变`idea`的Maven配置 



# Maven的GAVP

Maven 中的 GAVP 是指 Groupld、Artifactld、 Version、Packaging 等四个性的缩写，其中前三个是必要的，而 Packaging 属性为可选项

- **GroupID**：表示项目所属的组织或公司的标识符；格式：com.[公司/BUJ.业务线.[子业务线]，最多 4 级
-  **ArtifactID**：表示项目的唯一标识符，格式：通常是项目的名称；产品线名-模块名
- **Version**：表示项目的当前版本号；格式：主版本号.次版本号.修订 号
- **Packaging**：表示项目的打包方式，即输出的文件类型
  - **jar**：Java项目的标准打包方式，包含Java类和资源文件。
  - **war**：用于Web应用程序的打包方式，包含了Web应用所需的所有文件。
  - **pom**：用于打包Maven项目本身的信息，包含了项目的依赖、插件等信息。
  - **ear**：用于企业级Java应用程序的打包方式，包含了多个模块的JAR、WAR等文件。



# 第三方依赖



## 第三方依赖信息声明

```xml
<groupId></groupId>
<artifactId></artifactId>
<version></version>
<scope></scope>
```

- 可选属性`scope`：引入依赖的作用域
  - **compile（默认值）**：依赖在编译、测试、运行阶段都有效
  - **provided**：依赖在编译阶段有效，但在打包阶段（例如WAR包构建）不会被包含
  - **runtime**：依赖在运行和测试阶段有效，但不会被编译
  - **test**：依赖仅在测试编译和运行测试时有效，不会被打包



## 第三方依赖导入失败

原因：

1. 网络不好
2. 版本号错误
3. 本地仓库被污染

解决办法：

3. 找到本地仓库对应的包文件，删除即可（.lastUpdated文件）

