学习流之1  springBoot 教学

来点以前的总结放上来让大家过目一下，以往实在太忙，现在抽出一些空来整理一些东西放git，让IT代码生涯结束前留点东西给大家；

#项目创建方式
Maven 创建工程方式

配置Maven环境
下载地址：http://maven.apache.org/download.cgi
下载文件含义：

~~~
Binary tar.gz archive：是装在Linux、MacOsX上的；
Binary zip archive：是装在windows上的；
binary表示编译后的二进制文件，一般比较小，适合直接在项目中使用；
source表示可以查看源代码的，比binary大一些，如果你想看一下maven的源码可以下载这一类的
~~~
vim ~/.bash_profile
:wq (保存修改)
source .bash_profile

DgroupId 包名
DartifactId 项目名称/模块名称
DarcgetypeArtufactId 项目骨架//不是很清楚啥意思

~~~
mvn archetype:generate -DgroupId=com.java.xing -DartifactId=chapter01 -DarchetypeArtifactId=maven-archetype-quickstart -Dversion=1.0-SNAPSHOT -DinteractiveMode=false 
~~~

下载intellJ IDEA ，打开项目运行程序，即可；

###构建第一个项目

添加
spring-boot-starter-parent 依赖，其是一个特殊的starter，提供Maven的默认配置，同事提供 deoendency-management,作用在引入其他依赖时不必输入版本号，方便依赖管理。我们引入一个Web的starter代码如下：

~~~
....
  <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.0.0.RELEASE</version>
  </parent>
...

<dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
    <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
  </dependencies>
~~~

#####编写启动类
在目录结构下的APP.java类，编写如下代码：

~~~
@EnableAutoConfiguration
@ComponentScan
public class App
{
    public static void main( String[] args )
    {
        SpringApplication.run(App.class,args);
    }
}
~~~
这里主要发现能使用Spring的一些注解了；
1）@EnableAutoConfiguration 开启自动化配置（这里会自动进行Spring和SpringMVC配置）；
2）SpringApplication 第一个参数是确定主要组建，第二个参数是运行时的其他参数；
3）ComponentScan 进行包扫描，扫描注解，这里可以使用  @SpringBootApplication  替代 @EnableAutoConfiguration
@ComponentScan；

创建类HelloController，代码如下：

~~~
@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello(){
        return "hello spring boot";
    }
}
~~~

运行APP

输入：
http://localhost:8080/hello 访问成功。
