# 1.JAVA基础知识

## Java基础概念

### main函数介绍

函数入口，程序执行的起点



### JAVA关键字特点

1.完全小写字母

2.增强版的记事本里有特殊颜色标记



### 修饰符

公有的，以public修饰符指定，对所有类可见。

受保护的，以protected修饰符指定，对同一包内的类和所有子类可见。

默认的，也称为default，在同一包内可见，不使用任何修饰符。

私有的，以private修饰符指定，在同一类内可见。



### 标识符

1.自己定义的内容，类名字，方法的名字和变量名字等等

2.包含26个字母，0-9数字，$和_

3.命名规范，类：首字母大写，后面每个单词首字母大写（驼峰式），变量：首字母小写，后面每个单词首字母大写（小驼峰式），方法名：同变量名



### 常量

1.程序运行期间固定不变的量

2.分类：字符串常量（双引号，随便几个字符），整数常量，浮点数常量，字符常量（单引号，单个字符），布尔常量，空常量（不能直接打印输出）



### 数据类型

八个基本类型：byte,short,int,long,float,double,char,boolean

引用类型：String，数组

引用类型：变量由类的构造函数创建，可以使用它们访问所引用的对象，可以被赋值成null



- ### **数据转换**

隐式转换，需要符合从右到左数据范围从小到大（精度范围）

强制转换，手动转换，范围小变量 = （范围小类型）范围大变量，有可能发生精度损失或者数据溢出

编译器的常量优化：

1. 针对byte/short/char三种类型，如果右侧赋值的数值(常量)没有超过范围，那么javac编译器会自动隐含地补上一个强转代码(byte)(short)(char)
2. Java中的byte，short，char进行计算时都会提升为int类型



### 加号的用法

1.数值相加

2.char和数值根据assci表值进行相加,返回int类型

3.字符串和其他类型数据进行连接



### 运算符

取模的两种方式

- 取模运算符%

- 位与运算符&

  当n=2*n时，x%n=(n-1)&x

  ==并且，但由于&运算效率会更高，因此hashmap的底层取模用的是后者==





### 三元运算符?:

variable = expression ？value1(if true) : value2( if false)

ex:

a = b == c ? 1 : 2(当b=c为true时，a=1，b=c为false时，a=2)



### 自增自减

++n，前++，先加后用

n++，后++，先用后加

前++和后++在单独使用时(语句带了分号)，作用相同,"n++;++n;"，一般使用后++



### switch语句注意事项

多个case后的数值不可以相同

switch后小括号里支持的数据类型只包含基本数据类型：byte/short/char/int, 引用数据类型：String字符串，enum枚举

如果没有break，将会向下穿透下一个case（无论case中的条件是否满足）执行，因此case中的break不能省略，而且defaul的break建议不省略（万一顺序颠倒，则会引起穿透）



### Intellij IDEA常用快捷键

修复错误（如自动导包）alt(option)+回车

删除某一行 control+Y或者command+删除

复制某一行 control+D或者command+D

格式化代码 control+alt+L或者option+command+L

移动上下行 alt+shift+up/down 或者option+shift+up/down



### 方法调用格式

1.单独调用

2.打印调用，需要返回值

3.赋值调用，需要返回值

void方法只能单独调用，因为没有返回值



## JAVA四种权限修饰符



注意事项：(default)不是关键字default，而是根本不写，以下都是“直接访问”权限演示



​				public    >    protected    >    (default)    >    private

同一个类    YES           	 YES           	 YES        	   YES

同一个包    YES           	  YES     	       YES         	   NO

不同包的子类 YES            YES            	NO       	     NO

不同包的不同类 YES         NO       	     NO           	 NO

