# Spring学习

地址：https://www.bilibili.com/video/BV1WZ4y1H7du/?p=2

# 1.1 Spring简介：

Spring是分层的JavaSE/EE应用full-stack轻量级开源框架，以==loC==（Inverse of Control：反转控制）和==AOP==（Aspect Oriented Programming：面向切面编程）为内核。

提供了==展现层SpringMVC==和==持久层Spring JDBCTemplate==以及==业务层事务管理==等众多的企业级应用技术，还能整合开源世界众多著名的第三方框架和库类，逐渐成为使用最多的JavaEE企业应用开源框架

# 1.2 Spring的优势：

1)方便解耦，简化开发：

通过spring提供的loC容器，可以将对象间的依赖关系交由Spring进行控制，避免硬编码所造成的过度耦合。用户也不必再为单例模式类、属性文件解析等底层的需求编写代码，可以更关注上层的应用。

2）AOP编程的支持

通过Spring的AOP功能，方便进行面向切面编程，许多不容易用传统OOP实现的功能可以通过AOP轻松实现。

3）声明式事务的支持

可以将我们从单调烦闷的事务管理代码中解脱出来，通过声明方式灵活的进行事务管理，提高开发效率和质量。

4）方便程序的测试

可以用非容器依赖的编程方式进行几乎所有的测试工作，测试不再是昂贵的操作，而是随手可做的事情。

5）方便集成各种优秀的框架

6）降低javaEE API的使用难度

Spring对javaEE API(如JDBC,JavaMail，远程调用等)进行了薄薄的封装，使这些API的使用难度大大降低

7）Java源码是经典学习范例

Spring的源码设计精妙，结构清晰，匠心独用，是学习的典范。

## 1.3 Spring的体系结构

<img src="/Users/xin.li/Documents/学习笔记/Spring/Spring学习.assets/截屏2020-09-23 下午6.39.14.png" alt="截屏2020-09-23 下午6.39.14" style="zoom: 50%;" />

## 1.4 Spring快速入门

<img src="/Users/xin.li/Documents/学习笔记/Spring/Spring学习.assets/截屏2020-09-23 下午6.45.50.png" alt="截屏2020-09-23 下午6.45.50" style="zoom:50%;" />

开发步骤文字描述：

1.导入spring开发的基本包坐标

2.编写Dao接口和实现类

3.创建spring核心配置文件

4.在spring配置文件中配置UserDaoImpl

5.使用spring的API获得Bean实例