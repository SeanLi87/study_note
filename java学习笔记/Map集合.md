## Map集合

章节地址：https://www.bilibili.com/video/BV1uJ411k7wy?p=274

map是一个接口

### map集合特点

1.map集合是一个双列集合,一个元素包含两个值：key和value

2.map集合中的元素，key value的数据类型可以相同也可以不同

3.key不允许重复，value可以重复

4.key和value是一一对应的

### map的常用实现类

#### 1.HashMap

java.util.HashMap<k,v>实现类 implements Map<k,v>接口

特点：

1.HashMap集合底层是哈希表，查询速度特别快

JDK1.8之前：数组+链表

JDK1.8之后：数组(以key的hashcode为数组下标，数组元素是entry（包含了key的hashcode，key，value），数组初始长度为16位，自动扩容时乘以2）+链表/红黑树（链表长度超过8时，以红黑树替代链表加快查询速度）

==hashmap时如何通过key的hash值来快速计算索引？==

使用**hash%length**进行取模运算可以直接得到对应的索引，但是取模运算符效率较低，因此利用的是位与运算符==&==来取模

&取模必须是2n-1才能实现，刚好hashmap的自动扩容是2n，因此公式为**(length - 1) & hash**



2.HashMap是一个无序集合，存储和取出元素的顺序可能不一致



缺点：

1.如果key是自定义类型，需要重写hashcode方法，并且要求hashcode所依赖的成员变量不能发生变化，不然hashmap的行为将不正常

2.当触发数组扩容时，需要重新计算hashcode，效率较低，因此尽量提前确定数组长度

#### 2.LinkedHashMap

java.util.LinkedHashMap<k,v>类 extends HashMap<k,v>类

特点：

1.底层是哈希表+链表（保证迭代顺序）

2.是一个有序的集合，存储元素和取出元素顺序是一致的



#### 3.HashTable集合概述

和HashMap类似，但区别在于：

1.单线程，速度慢

2.键和值都不允许存储null值

备注：大部分场景都被HashMap取代了，但是其子类Properties依然活跃在历史舞台，因为Properties是唯一一个和IO流结合的集合



#### 4.Debug追踪

方式：在程序左侧，行号右侧空白处，鼠标左键单击，添加断点

操作：

F8：逐行执行程序

F7：进入到方法中

shift+F8：跳出方法

F9：跳到下一个断点，如果没有下一个断点，那么就结束程序

ctrl+F2：退出debug模式，停止程序

console：切换到控制台