# java异常概念和体系

*根类：java.lang.Throwable

​		**子类：java.lang.Exception：编译期异常，进行编译（写代码）时出现的问题

​			***子类：RuntimeException:运行期异常，java程序运行过程中出现的问题

​		备注：异常相当于程序可以解决的小毛病，处理之后程序可以继续执行

​		**子类：java.lang.Error

​		备注：相当于程序中无法治愈的问题，必须修改代码，程序才能继续执行



## 1.异常（exception）分类和处理方式

### 异常分类：

编译期异常，是指编译器在编译时可以预计出现的异常情况，因此编译器会提前检查这些程序是否有异常处理，如果没有则需要在程序编译前强制加上，不然编译检查会报错

运行期异常，是指编译器不会检查的异常类型，在运行时才会出现。

### 处理异常的两种方式：

1.throws抛出异常，将异常向上抛出（调用者），若上层所有调用者都没有该异常的处理方式，则最终抛给JVM处理，JVM会将异常（==内容，原因，位置==）打印并终止程序

2.try_catch异常，将异常在catch代码块中处理（向上抛出或者其他处理逻辑）之后，程序后序代码可以正常执行



```java
    public static void main(String[] args) /*throws ArrayIndexOutOfBoundsException*/ {//编译期异常处理方式：抛出异常
        //编译期异常
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        Date date = null;
        //编译期异常处理方式：try catch异常
        try {
            date = sdf.parse("1999-1111");
        } catch (ParseException e) {
            e.printStackTrace();
        }

        //运行期异常
        int[] int1 = new int[]{1, 2, 3};
        try {

            System.out.println(int1[3]);//ArrayIndexOutOfBoundsException
        }catch (Exception e){
            System.out.println("出现了越界："+e);
        }
        
        //ERROR
//        int[] in = new int[1024*1024*1024];
        System.out.println("后序代码执行");

    }
```



## 2.throw关键字

作用：可以使用throw关键字在指定的方法中抛出指定的异常

格式：`throw new xxException("异常产生的原因")`

注意事项:

​			1.throw关键字必须写在方法的内部

​			2.throw关键字后面new的对象必须是Exception或者Exception的子类

​			3.throw关键字抛出指定的异常对象，我们就必须处理这个异常对象

​						throw关键字后面创建RuntimeException或者其子类，我们可以不处理，默认会交给JVM处理（打印，中断）						throw关键字后面创建的是编译异常，我们就必须处理这个异常，要么throws，要么try...catch

```java
public static void main(String[] args) {

    int[] a = null;
    int result = method(a, 0);
    System.out.println(result);
}

private static int method(int[] array, int index) {

    if (array==null){
        throw new NullPointerException("数组为null");
    }

    return array[index];
}
```



## 3.throws关键字

### 概述

异常处理的第一种方式，交给别人处理

### 作用

​		当方法内部抛出异常对象的时候，那么我们就必须处理这个异常对象

​		可以使用throws关键字处理异常对象，会把异常对象声明抛出给方法的调用处者处理（给别人处理，自己不处理），若调用者没有处理，最终交给JVM处理-->中断处理

### 格式

​	修饰符 返回值类型 方法名（参数列表） throws AAAException,BBBException...{

​			throw new AAAException("产生原因");

​			throw new BBBException("产生原因");

​	}

备注：所有的exception都是Exception类的子类，因此可以在声明多个exception的方法时，只抛出Exception一个异常也可以



## 4.try...catch关键字

### 格式

​	try{

​		可能产生的异常代码	

​	}catch(异常类型  变量名){

​		异常的处理逻辑，一般在工作中，会将异常记录到日志中

​	}

注意事项：如果try中可能出现多个异常，那么可以使用多个catch分别处理这些异常



### Throwable类中获取异常信息方法

getMessage()只返回异常的message内容

toString()返回message+异常类别(异常类路径)

printStackTrace()，打印异常对象，包括所有内容



### finally关键字

格式：

```java
try {
}catch (Exception e){
}finally {
    System.out.println("资源施放");
}
```

作用：

无论异常是否发生，都会执行finally代码块中代码，一般用于资源释放操作

finally可以返回值，但是如果存在finally代码块，一定会执行，因此一定会返回finally的return结果。==容易出现问题，避免出现这种情况==



### 多异常捕获处理

1.多次捕获多次处理：多个try和对应多个catch

2.一次捕获多次处理：1个try和对应多个catch

3.一次捕获一次处理：1个try和1个catch



## 5.子父类异常注意事项

1.父类抛出什么异常，子类可以用相同异常

2.父类抛出什么异常，子类可以用该异常的子类异常

3.父类不抛出异常，子类也不可以抛出异常

4.父类不抛出异常，子类只能try...catch异常



## 6.自定义异常类

### 格式

public class XXXException extends Exception | RuntimeException{

​	空参构造

​	带异常信息的构造

}

### 注意

1.自定义异常类一般默认命名规则是XXXException

2.必须继承Exception(表示编译期异常)或者RuntimeException(运行期异常)



```java
public class Demo01DefineException extends Exception{

    public Demo01DefineException() {
    }

    public Demo01DefineException(String message) {
        super(message);
    }
}
```





