# Mysql学习笔记

简介：mysql是一种关系型(关联)数据库，关联数据库将数据存储倒不同的表中，而不是将所有数据放入一个大仓库内，提升了灵活性。所谓关系型数据库，是建立在关系模型基础上的数据库，借助于集合代数等数学概念和方法来处理数据库中的数据

## 数据类型

| **类型**     | **大小**                                 | **范围（有符号）**                                           | **范围（无符号）**                                           | **用途**        |
| :----------- | :--------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------------- |
| TINYINT      | 1 字节                                   | (-128，127)                                                  | (0，255)                                                     | 小整数值        |
| SMALLINT     | 2 字节                                   | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值        |
| MEDIUMINT    | 3 字节                                   | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值        |
| INT或INTEGER | 4 字节                                   | (-2 147 483 648，2 147 483 647)                              | (0，4 294 967 295)                                           | 大整数值        |
| BIGINT       | 8 字节                                   | (-9 233 372 036 854 775 808，9 223 372 036 854 775 807)      | (0，18 446 744 073 709 551 615)                              | 极大整数值      |
| FLOAT        | 4 字节                                   | (-3.402 823 466 E+38，-1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度 浮点数值 |
| DOUBLE       | 8 字节                                   | (-1.797 693 134 862 315 7 E+308，-2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度 浮点数值 |
| DECIMAL      | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值                                               | 依赖于M和D的值                                               | 小数值          |



## 常用sql

排序：==order by== {column} ==asc/desc==,按照column升序/降序排序，默认为升序排序

分组：==group by== {column}，按照column进行分组，需要配合分组操作进行使用，如count,sum,avg等等

连接：

​		内连接 ==from== {lefttable} ==inner join== {righttable} ==on== (condition)，获取左右表有关联的数据，等同于from {lefttable}, {right table} where condition

​		左连接/右连接，==from== {lefttable} ==left/right join== {righttable} ==on== (condition) ,获取左表/右表全部数据及(右表/左表)关联上的数据

NULL值判断：==where== {column} ==IS NULL/IS NOT NULL==

正则：==REGEXP== '(condition)'



## 事务：

事务主要用于处理复杂度高，操作量大的数据，比如说，在人员管理系统中，你删除一个人员，你即需要删除人员的基本资料，也要删除和该人员相关的信息，如信箱，文章等等，这样，这些数据库操作语句就构成一个事务。



## 索引：

索引是一张表，用于对某单列（单列索引）或者多列（组合索引）进行快速查找，索引==大大提高了查询速度==，同时却==会降低更新表的速度==，如对表进行INSERT、UPDATE和DELETE。因为更新表时，MySQL不仅要保存数据，还要重新保存一下索引文件。建立索引会占用磁盘空间的索引文件。

### 索引类型：

------

PRIMARY KEY 主键索引：主键索引

INDEX 普通索引

UNIQUE 唯一索引，索引列的值必须唯一，但允许有空值。如果是组合索引，则列值的组合必须唯一

FULLTEXT 全文索引

组合索引（较特殊）



### 创建索引

```sql
CREATE TABLE table_name[col_name data type]
[unique|fulltext][index|key][index_name](col_name[length])[asc|desc]
```

1.unique|fulltext为可选参数，分别表示唯一索引、全文索引
		2.index和key为同义词，两者作用相同，用来指定创建索引
		3.col_name为需要创建索引的字段列，该列必须从数据表中该定义的多个列中选择
		4.index_name指定索引的名称，为可选参数，如果不指定，默认col_name为索引值
		5.length为可选参数，表示索引的长度，只有字符串类型的字段才能指定索引长度，长字符串的时候，建议只创建前面n个字符的索引(使用前缀索引)，避免索引长度过长
		6.asc或desc指定升序或降序的索引值存储





