## String，StringBuilder, StringBuffer和静态关键字



## String

### String的概述

java程序中所有字符串字面值（如“abc”）都作为此类的实例实现。

*<u>意思是说程序里所有双引号的字符串，都是string类的对象（就算没有new，也是string类对象）</u>*

特点：

1.字符串的内容用不可变

2.正因为不可变，因此字符串是可以共享使用的

3.字符串效果上相当于是final char[]字符数组，但是底层原理是byte[]数组（==JDK1.8及以前是char[]数组，由于发现String类型是拉丁字符居多，拉丁字符对应的assic码只需要1个byte长度即可表示，因此为了节省内存空间，将string底层由char数组变成了byte数组==）



### String的比较

String str1 = "abc";

String str2 = "abc";

String str3 = "a"+"bc";

String str4 = "a";

String str5 = str4+"bc";

str1 == str2; ==都引用相同的字符串常量池对象，因此地址相同==

str1 == str3; ==jvm在拼接常量池对象时会优化处理，直接从常量池中查找拼接后的字符串，因此地址相同==

str1 != str5; ==只要有String引用类型加入运算，最后都会重新new一个常量池以外堆内存的String对象出来==



注意事项：**禁止在循环中进行+=字符串变量操作，因为会new出很多StringBuilder对象和String对象，消耗大量资源**

参考文档：https://blog.csdn.net/qq_44507430/article/details/106733368

备注：UTF-8的中文字符占2-4个字节，字节的取值范围是[-128,127]



### String的内存图

![截屏2020-08-13 上午10.22.38](/Users/xin.li/Documents/学习笔记/java学习笔记/String字符串和静态关键字.assets/截屏2020-08-13 上午10.22.38.png)



## StringBuilder类

背景：在使用字符串直接相加进行拼接时，总是会在内存中创建一个新的String对象，因此会造成大量的内存消耗。（因为底层时final修饰的数组）

概述：StringBuilder是一个字符串缓冲区，底层是没有被final修饰的数组，可以改变长度（初始16个字符），当超出了当前容量时，会自动扩容

StringBuilder和String可以相互转换：

​	StringBuilder.ToString====>String

​	StringBuilder("String")===>StringBuilder

备注：StringBuilder是线程不安全的（多线程）

```java
StringBuilder bu1 = new StringBuilder();//空参构造
System.out.println("bu1:" + bu1);//空字符串

StringBuilder bu2 = new StringBuilder("abc");//有参构造
System.out.println("bu2:" +bu2);//bu2:abc

StringBuilder bu3 = new StringBuilder();
StringBuilder bu4 = bu3.append("abc");//append方法
System.out.println("bu3:"+bu3);//bu4:abc
System.out.println("bu4:"+bu4);//bu4:abc

StringBuilder bu5 = new StringBuilder();
bu5.append(1).append('a').append(1.1).append("ABC");
System.out.println("bu5:"+bu5);

String a = "abc";
StringBuilder bu = new StringBuilder(a);
String b = bu.toString();
System.out.println(a.equals(b));
```



## StringBuffer

StringBuffer用法和StringBuilder类似，但是append方法是线程安全的（单线程，使用关键字synchronized修饰）



## static关键字概述

![截屏2020-08-13 上午10.23.45](/Users/xin.li/Documents/学习笔记/java学习笔记/String字符串和静态关键字.assets/截屏2020-08-13 上午10.23.45.png)

**Static变量内存示意**

- ![截屏2020-08-13 上午10.23.52](/Users/xin.li/Documents/学习笔记/java学习笔记/String字符串和静态关键字.assets/截屏2020-08-13 上午10.23.52.png)

