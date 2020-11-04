# Collection集合

## 1.collection集合概述

集合的概念：集合是java提供的一种容器，可以用来存储多个数据

### 1.1 集合和数组的区别和关系

- 数组是长度固定的，集合是长度可变的数组
- 数组存储同一种类型的数据，包括==基本型==或者==引用类型==，集合只能存储==引用类型==
- 数组不属于collection
- collection中的list（arraylist，vector）底层使用数组进行实现
- 数组是java内置的数据类型



### 1.2 学习集合的方式

先从最上层的collection接口常用方法开始学，这些方法在实现类中都会存在，再学习实现类中不同的常用方法

![截屏2020-08-13 下午2.38.04](/Users/xin.li/Documents/学习笔记/java学习笔记/Collection集合.assets/截屏2020-08-13 下午2.38.04.png)

List集合：有索引，可以存储重复元素，可以保证存取数据

ArrayList：底层是数组实现的，查询快，增删慢

LinkedList： 底层是链表实现的，查询慢，增删块

Vector：...



set集合：无索引，不可以存储重复元素，存取无序

HashSet：底层是哈希表+(红黑树)实现的，无索引，不可以存储重复元素，存取无序

LinkedHashSet：底层是哈希表+链表实现的，无索引，不可以存储重复元素、可以保证存取顺序

TreeSet：底层是二叉树实现。一般用于排序

### 1.3遍历collection集合的方式有三种

1.转换成数组，根据索引for循环遍历----不推荐

2.使用迭代器遍历，使用while(hasNext())---较推荐

3.使用增强for循环遍历---推荐



## 2.泛型

### 2.1泛型的概念

![截屏2020-08-13 下午2.45.10](/Users/xin.li/Documents/学习笔记/java学习笔记/Collection集合.assets/截屏2020-08-13 下午2.45.10.png)

不建议使用泛型情况：因为默认是object类型，因此参数/返回值可以是任何类型，但是当使用泛型对象时，容易引起数据类型异常， 比如存储的数据包含数字和string，向下将object转型成string后，数字类型的数据只会在程序运行时才报错。==因此不要对泛型接口/类创建对象时，不指定数据类型==

建议使用泛型情况：提前指定泛型，这样在使用泛型对象时，可以在编译时时就能提前将数据格式使用错误暴露出来（idea可以在写代码的时候就报错）

### 2.2声明泛型类/接口

```java
public class GenericClass<E>{

    public E getName() {//泛型类型返回值的成员方法
        return name;
    }

    public void setName(E name) {//泛型类型参数的成员方法
        this.name = name;
    }

    //泛型类型的成员变量
    private E name;
}
```



### 使用泛型类/接口

使用泛型的第一种方式

在实现类中指定泛型

```java
public class GenericInterfaceImpl1 implements GenericInterface<String> {
    @Override
    public void method1(String s) {

        System.out.println(s);
    }
}
```

使用泛型第二种方式

在实现类中不指定泛型

```java
public class GenericInterfaceImpl2<I> implements GenericInterface<I> {
    @Override
    public void method1(I i) {
        System.out.println(i);
    }
}
```



### 2.4声明泛型方法

```java
public <S> S method3(S a){//返回值为泛型，参数也是泛型
    return a;
}
```

### 2.5泛型的通配符

泛型没有继承关系，因此不能使用object类进行自动向上转型操作或者向下转型。只能通过<? extend 类名>使用当前类或者子类类型， <? super 类名>使用当前类或者父类



## 3.和集合相关的数据结构

### 栈结构

![截屏2020-08-13 下午2.56.49](/Users/xin.li/Documents/学习笔记/java学习笔记/Collection集合.assets/截屏2020-08-13 下午2.56.49.png)



### 队列结构

![截屏2020-08-13 下午2.56.58](/Users/xin.li/Documents/学习笔记/java学习笔记/Collection集合.assets/截屏2020-08-13 下午2.56.58.png)

### 数组结构

![截屏2020-08-13 下午2.57.16](/Users/xin.li/Documents/学习笔记/java学习笔记/Collection集合.assets/截屏2020-08-13 下午2.57.16.png)

### 链表结构

![截屏2020-08-13 下午2.58.24](/Users/xin.li/Documents/学习笔记/java学习笔记/Collection集合.assets/截屏2020-08-13 下午2.58.24.png)

### 红黑树结构

待学

## 4.List集合

### 接口特点

1.有序集合，存储和取出元素的顺序是一致的

2.有索引，包含了一些带索引的方法：add,get,remove,set

3.允许存储重复元素

### ArrayList集合（常用）

特点：查询快（因为数组内存是一个整体，元素的地址是连续的，可以通过索引进行查找），增删慢（因为每次增删都需要重新拷贝一份集合），多线程。

备注：不要将任何需求都使用ArrayList进行实现，提升性能

### LinkedList集合

特点：

1.查询慢（因为元素中地址不连续，需要通过前一个元素进行查找下一个元素，因此每次都需要遍历整个数组）

2.增删快（因为增删操操作不需要重新拷贝集合）。多线程。大量操作集合首尾的方法

3.有序，有索引（双向链表？）

备注：不能使用多态来创建linkedlist，因为需要使用大量LinkedList实现类中的方法，而List中是缺少这些方法的



### Vector集合（仅作了解）

1.底层也是基于数组实现

2.是线程安全

3.是一个1.0版本的早期集合



## 5.Set集合

接口特点：

1.不允许存储重复元素

2.不带索引，不能使用普通的for循环遍历

3.存入元素和取出元素的顺序不同



### HashSet集合

概述：底层是hashmap。jdk1.8之前，hashmap=数组+链表；jdk1.8之后：哈希表=数组+链表/红黑树(当链表元素超过8时，转化成红黑树结构）

![截屏2020-08-13 下午3.06.34](/Users/xin.li/Documents/学习笔记/java学习笔记/Collection集合.assets/截屏2020-08-13 下午3.06.34.png)

特点：

1.不允许存储重复元素

2.不带索引，不能使用普通的for循环遍历

3.是一个无序集合

4.底层是哈希表

5.查询速度快

```java
    Set<Integer> set = new HashSet<>();
    set.add(3);
    set.add(2);
    set.add(1);
    set.add(3);
    //使用迭代器循环
    Iterator<Integer> iterator = set.iterator();
    while (iterator.hasNext()){
        System.out.println(iterator.next());
    }
    //使用增强for循环
    for (Integer integer : set) {
        System.out.println(integer);
    }
```
### 哈希值

概述：哈希值是一个十进制整数，由系统随机给出（==可以表示对象的地址值，是一个逻辑地址，是模拟出来的得到的地址，不是数据实际存储的地址==。直接sout打印对象时为16进制地址(没有重写hashcode方法时)，然后将其转换成10进制后就成为了hash值的结果)

```java
public native int hashCode()
```



```java
        Person p1 = new Person();
        System.out.println(p1.hashCode());//1625635731
        System.out.println(p1);//com.sean.demo03.HashCode.Person@60e53b93   “60e53b93”的十进制是1625635731
```



备注：native关键字表示调用本地操作系统的方法，调用的是和其他语言，如C/C++一起编写的底层API，不在JDK源代码中。不同系统略有差异。



String类重写hashCode方法：根据字符串中每个字符的byte编码计算得出。

注意：不同字符串可能出现相同的哈希值(==哈希冲突==）

```java
      int h = hash;
        if (h == 0 && value.length > 0) {
            char val[] = value;

            for (int i = 0; i < value.length; i++) {
                h = 31 * h + val[i];
            }
            hash = h;
        }
        return h;
```

### HashSet中add元素不重复的原理

1.先判断分类数组中是否存在相同的哈希值

2.若不存在，则直接将元素存到集合中

3.若存在（哈希冲突），判断元素值是否和已有元素相同

4.若不相同，则说明不是同一个元素，可以存入集合，返回true

5.若相同，则说明是同一个元素，则不存入集合，返回false



### HashSet存储自定义类型

由于存储时，会判断先判断元素哈希值，然后再判断元素的数值，因此需要==重写hashCode和equals方法==



### LinkedHashSet，需要继续学习

描述：底层是哈希表（数组+链表/红黑树）+链表，多了一条链表记录元素的顺序，保证元素有序



### 可变参数

概述：

当方法的参数类型确定，但是个数不确定时，可以使用可变参数。可变参数底层是一个数组，根据传递参数个数不同，创建不同长度的    数组，来存储这些参数，0~多个参数.

方法内部使用入参为数组格式

格式：

修饰符 返回值类型 方法名(参数类型...变量名) {}



注意事项：

1.一个方法的参数列表，只能有一个可变参数

2.如果方法的参数有多个，那么可变参数必须写在参数列表的末尾

```
    private static int sum(int... array) {

        int sum = 0;
        for (int i : array) {
            sum += i;
        }

        return sum;
    }
```



4.collection集合工具类常用方法

addAll(集合名字，集合可变元素参数)，批量添加集合元素

suffle(list集合名字)，将list集合的顺序随机打乱

sort(list集合)，讲list集合进行排序(默认升序）

注意事项：若需要比较自定义类型，需要继承Comparable<T>接口，然后重写compareTo方法

排序规则参考如下代码：

```
    @Override
    public int compareTo(Person o) {
        return this.age - o.age;//升序排序,结果为0代表不需要排序，为<0时不需要调换this和o的额顺序，为>0时需要调换this和o的顺序
    }
```

sort(list集合，comparator)，使用自定义的comparator直接定义排序方式

```
        Collections.sort(students, new Comparator<Student>() {//第一种，只是用一种方式排序
            @Override
            public int compare(Student o1, Student o2) {
                return o1.getAge()-o2.getAge();
            }
        });

        System.out.println(students);

        Collections.sort(students, new Comparator<Student>() {//第二种，当第一个参数相等时，使用第二个参数进行排序
            @Override
            public int compare(Student o1, Student o2) {
                int result = o1.getAge()-o2.getAge();
                if (result == 0){
                    result = o1.getName().charAt(0) - o2.getName().charAt(0);
                }

                return result;
            }
        });
```