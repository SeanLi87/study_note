# Tomcat和servlet

## web相关概念

### 服务器资源分类：

1.静态资源：所有用户访问后，得到的结果都是一样的，称为静态资源，静态资源直接被浏览器解析

​	如：html，css，Javascript

2.动态资源：每个用户访问相同资源后，得到的结果可能不一样。称为动态资源，动态资源被访问后，需要先转化成动态资源，再返回给浏览器

​	如:servlet/jsp, php,asp...



### web服务器软件：

- 服务器：安装了安装了服务器软件的计算机

- 服务器软件：接收用户请求，处理请求，做出响应

- web服务器软件：接收用户请求，处理请求，做出响应

  ​	在web服务器软件中，可以部署web项目，让用户通过浏览器来访问这些项目

  ​	由于web资源只能在容器中运行，因此也称为web容器

### 常见的java相关web服务器软件

Weblogic: : oracle公司，大型的javaEE服务器，支持所有的JavaEE规范，收费的。

websphere：IBM公司，大型的javaEE服务器，支持所有的JavaEE规范，收费的。

JBOSS: JBOSS公司，大型的javaEE服务器，支持所有的JavaEE规范，直接使用不收费，间接收费的。

Tomcat：Apache基金组织，中小型的JavaEE服务器，仅仅支持少量的JavaEE规范如servlet/jsp。开源的，免费的。

备注：JavaEE是Java语言在企业级开发中使用的技术规范的综合，一共规定了13项大的规范。



### Tomcat：web服务器软件

1.下载

2.安装

3.卸载

4.启动

​	备注：80端口是http默认端口号，因此如果tomcat的端口号为80，客户端在请求的时候可以不输入端口号直接通过地址请求即可

5.关闭

6.配置

​	部署项目的方式：

​			1.直接将项目放到webapps目录下即可。

​					* 将访问项目拷贝到webapps下面，访问方式为 ==地址:端口/项目目录/资源文件==

​					* 简化部署：将项目打包成一个war包，再将war包放到webapps目录下。

​										war包自动解压缩，删除war包会自动删除目录

​			2.配置conf/server.xml文件（缺点：不安全）

​					在<Host>标签体中配置

​					<Context docBase="项目存放路径" path="/hehe" />

​					docBase:项目存放路径

​					path:虚拟目录

​			3.在conf/Catalina/localhost目录下创建任意名称的xml文件，在文件中编写

​				<Context docBase="项目存放路径" />

​				虚拟目录：xml文件的名称

​				xml可以进行热更新，随时生效



### 静态项目和动态项目：

目录结构：

​	java动态项目的目录结构：

​		-- 项目的根目录

​			--WEB-INF目录：

​				--web.xml :web项目的核心配置

​				--classes目录：放置字节码文件的目录

​				--lib目录：防止依赖的jar包

## Servlet: server applet

### 概念：运行在服务器端的小程序

​		servlet就是一个接口，定义了java被浏览器访问到(意思是被tomcat识别和执行)的规则

​		将来我们定义一个类，实现servlet接口，覆写方法

### 快速入门：

​		1.创建JaveEE项目

​		2.定义一个类，实现Servlet接口

​		3.实现接口中的抽象方法

​		4.配置Servlet

​			在web.xml中配置：		

```xml
<!--配置servlet -->
<servlet>
  <servlet-name>demo1</servlet-name>
  <servlet-class>cn.itcast.web.servlet.....</servlet-class>
</servlet>

<servlet-mapping>
  <servlet-name>demo1</servlet-name>
  <url-patter>/demo1</url-patter>
</servlet-mapping>
```

### 	执行原理

1.当服务器接收到浏览器客户端请求后，会解析请求URL路径，获取访问的Servlet的资源路径

2.查找web.xml文件，是否有对应的<url-patter>标签体内容

3.如果有，则在找到对应的<servlet-class>全类名

4.tomcat会将字节码文件加载进内存，并且创建其对象(有些对象是配置成在容器启动时创建)

5.调用其方法

### servlet生命周期

1.被创建：执行init方法，只执行一次，加载资源

​		* servlet什么时候被创建？

​				* 默认情况下，第一次被访问时，Servlet被创建

​				* 可以配置执行Servlet的创建时机

​						1.第一次被访问时，创建

​						<load-on-startup>的值为负数

​						2.在容器启动时，创建

​						<load-on-startup>的值为>=0整数

​			*Servlet的init方法，只执行一次，说明一个Servlet在内存中只存在一个对象，Servlet是单实例的。

​					*多个用户同时访问时，可能存在线程安全问题。（比如同时获取和修改成员变量）

​					*解决：尽量不要在Servlet中定义成员变量。即使定义了成员变量，也不要修改值。

2.提供服务：执行service方法，执行多次

​		*每次访问Servlet时，Service方法都会被调用一次

3.被销毁：执行destroy方法，当服务器正常关闭时执行一次

​		*Servlet被销毁时执行，服务器关闭时，Servlet被销毁

​		*只有服务器正常关闭时，才会执行destroy方法

​		*destroy方法在Servlet被销毁之前执行，一般用于释放资源



### Servlet3.0:

*好处：

​	支持注解配置，不需要配置web.xml了

*步骤：

1.创建javaEE项目，选择Servlet3.0的版本以上，可以不创建web.xml了

2.定义一个类，实现servlet接口

3.覆写方法

4.在类上使用@WebServlet注解，进行配置

​		@WebServlet("资源路径")



### 容器

docker run --name tomcat2 -v /tmp/webapps/:/usr/local/tomcat/webapps -it -d --rm -p 8082:8080 tomcat:9.0