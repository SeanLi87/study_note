# HTTP学习

## HTTP概述

概念：超文本传输协议

​		*传输协议：定义了客户端和服务器端通信时发送数据的格式

​		*特点：

​				1.基于TCP/IP高级协议

​				2.默认端口号：80

​				3.基于请求/响应模型的：一次请求对应一次响应

​				4.无状态的：每次请求之间相互独立，不能交互数据



## HTTP请求体

### 请求数据格式：

#### 		1.请求行

​				格式：请求方式	请求url	请求协议/版本

​				例如：	GET		/login.html	http/1.1

​					*请求方式：

​							*GET:

​									1.请求参数在请求行中，在url后

​									2.请求的url长度有限制

​									3.不太安全

​							*POST:

​									1.请求参数在请求体中

​									2.请求的url长度没有限制

​									3.相对安全					

#### 		2.请求头

​			格式：请求头名称：请求头值

​					*常见的请求头：

​								1.Host：主机地址

​								2.User-Agent：浏览器告诉服务器，我访问你使用的浏览器版本信息

​									*解决不同浏览器兼容性问题

​								3.Referer：http://xxx.xxx.com

​									*告诉服务器，当前请求从哪来

​											*作用：

​													1.防盗链，2.统计用户来源



#### 		3.请求空行

​			*用于分割post请求头和请求体

#### 		4.请求体：

​			*封装post消息的请求参数的

### 响应数据格式：

1.响应行

协议/版本  响应状态码 状态码描述

​		状态码分类：

​				1.1xx：服务器接收客户端消息，但没有接收完成，等待一段时间后，发送1xx多状态码

​				2.2xx：成功。

​				3.3xx：重定向。

​				4.4xx

​				5.5xx 

2.响应头

​	常见响应头：content-type, content-length,date...

3.响应空行

4.响应体



### request

1.request对象和response对象的原理

​	1.request和response对象都是由服务器创建的。我们来使用它们

​	2.request对象是来获取请求消息，response对象是来设置响应消息

2.request对象继承体系结构：

​	ServletRequest	--接口

​			|	继承

​	HttpServletRequest	--接口

​			|	实现

​	org.apache.catalina.connector.RequestFacade类(tomcat)

3.request：获取请求消息

### response



### servletContext对象

1.概念：代表整个web应用，可以和程序的容器(服务器)来通信

2.功能：

​	1.获取MIME类型

​	2.域对象：共享数据

​	3.获取文件的真实（服务器）路径



### 会话技术

1.会话：一次会话中包含多次请求和响应

​	*一次会话：浏览器第一次给服务器发送请求，会话建立，直到有一方断开为止

2.功能：在一次会话的范围内的多次请求间，共享数据

3.方式：

​	1.客户端会话技术：cookie

​	2.服务器端会话技术：session

### cookie

1.概念：客户端会话技术，绑定数据

2.cookie使用流程及原理

​	*客户端第一次请求servlet资源后，服务器在servlet的请求方法中创建cookie对象，设置cookie数据（==键值对==）

​	*将cookie对象添加到response中，response会自动创建一个cookie的响应头，发送给客户端

​	*客户端接收到响应后，获取到对应cookie，并根据http协议，会将cookie自动保存到客户端浏览器

​	*在相同会话中第二次请求其他servlet资源时，浏览器自动将本地cookie带入请求头里发送给服务器端

​	*服务器端在请求方法中可以从request里获取cookie

### JSP

1.概念：java server pages：java服务器端页面。可以理解为一个特殊的页面，其中既可以指定定义html标签，又可以定义java代码

2.作用：用于简化通过servlet生成html(特指带动态内容的页面，因为静态页面可以直接书写html标签页面）的书写方式。

3.原理：JSP本质上是一个servlet

### session

1.概念：服务器端会话技术，在一次会话的多次请求间共享数据，将数据保存在服务器端的对象中。HttpSession

2.session的使用流程及原理：

==session是基于cookie的。==

​	*客户端第一次请求servlet资源后，服务器在请求方法中创建session对象，设置session数据

​	*在response中添加响应头，内容为set-cookie：JSESSIONID=XXX

​	*客户端拿到响应后，会存储cookie，下次请求时，会将该cookie自动加到请求头中

​	*服务器端第二次受到请求后，会根据sessionID找到对应session，从而操作session(获取数据，设置数据等等)



## web的三层架构

表示层，应用层，数据层