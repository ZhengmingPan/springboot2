Spring Boot快速入门
## 1、简介
   Spring Boot 是由Pivotal团队提供的全新框架，其设计目的是用来简化新Spring应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。通过这种方式，Spring Boot致力于在蓬勃发展的快速应用开发领域(rapid application development)成为领导者。
##### Spring Boot的特点：
         1、可以完全不使用XML配置文件，只需要自动配置和Java Config； 
         2、提供starter，能够非常方便的进行包管理，简化MAVEN或Gradle的依赖配置
         3、提供热部署插件devtools的使用，节省开发时间
         4、内嵌Tomcat、Jetty等容器，无需部署WAR包
         5、内嵌容器，使得我们可以执行运行项目的主程序main函数，实现项目的快速运行
         6、提供Junit等测试框架的使用，简化代码测试工作
         7、提供应用监控功能
         ·········
         
## 2、开发工具
       Java1.8+、IntelliJ IDEA  2018.3.x、Maven 3.x

## 3、快速构建工程并运行

1、打开Creat New Project ——  Spring Initializr  —— 填写group、artifact  —— 钩上web(开启web功能）->点下一步就行了。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190225172907114.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3BhbjE5OTQ2Mg==,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20190225172936715.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3BhbjE5OTQ2Mg==,size_16,color_FFFFFF,t_70)
构建完成后，目录结构如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190225180029123.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3BhbjE5OTQ2Mg==,size_16,color_FFFFFF,t_70)
项目结构还是看上去挺清爽的，少了很多配置文件，我们来了解一下默认生成的有什么：

SpringbootdemoApplication： 一个带有 main() 方法的类，用于启动应用程序
SpringbootdenoApplicationTests：一个空的 Junit 测试了，它加载了一个使用 Spring Boot 字典配置功能的 Spring 应用程序上下文
application.properties：一个空的 properties 文件，可以根据需要添加配置属性
pom.xml： Maven 构建说明文件

1.maven配置（pom.xml）
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- Spring boot 父依赖 使用它之后，常用的包依赖就可以省去 version 标签。 -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.3.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.springbootdemo</groupId>
    <artifactId>springbootdemo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>springbootdemo</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
       <!--  引入Web框架 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

       <!--  引入Junit测试框架 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies> 
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>

```
2、启动程序并添加简单路由（SpringbootdemoApplication.java）
```
package com.springbootdemo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class SpringbootdemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootdemoApplication.class, args);
    }

    @GetMapping(value = "/")
    public String hello() {
        return "hello world";
    }

}
```
Spring Boot 项目通常有一个名为 *Application 的入口类，入口类里有一个 main 方法， 这个 main 方法其实就是一个标准的 Javay 应用的入口方法。
@SpringBootApplication 是 Spring Boot 的核心注解，它是一个组合注解，该注解组合了：@Configuration、@EnableAutoConfiguration、@ComponentScan； 若不是用 @SpringBootApplication 注解也可以使用这三个注解代替。

其中，@EnableAutoConfiguration 让 Spring Boot 根据类路径中的 jar 包依赖为当前项目进行自动配置，例如，添加了 spring-boot-starter-web 依赖，会自动添加 Tomcat 和 Spring MVC 的依赖，那么 Spring Boot 会对 Tomcat 和 Spring MVC 进行自动配置。

Spring Boot 还会自动扫描 @SpringBootApplication 所在类的同级包以及下级包里的 Bean 

3、application.properties 配置文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190225183914245.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3BhbjE5OTQ2Mg==,size_16,color_FFFFFF,t_70)
Spring Boot 使用一个全局的配置文件 application.properties 或 application.yml，放置在【src/main/resources】目录。
在这里的配置：server.port表示程序的端口号，server.servlet.context-path表示程序路径的前缀
4、运行
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019022518115286.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3BhbjE5OTQ2Mg==,size_16,color_FFFFFF,t_70)
在浏览器中输入http://localhost:8080/hello，运行
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190225184008683.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3BhbjE5OTQ2Mg==,size_16,color_FFFFFF,t_70)
这样，一个简单的Springboot程序就完成了
