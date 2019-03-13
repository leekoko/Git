## Java概述

### Java是怎么做到跨平台的？

字节码：Java源文件编译成的字节码与平台无关，为不同系统开发虚拟机来执行字节码

## 名词

### Java EE，Java SE，Java ME

企业版，标准版，移动版

### JRE，JDK

- JRE：运行环境，面向用户
- JDK：开发工具包，包含JRE，面向程序员

### JavaHome和Path

- Path：运行java时不用使用全路径
- JavaHome：方便设置Path

### classpath

Java虚拟机的类装载机制会通过classpath寻找类进行加载，不设定classpath，会出现类找不到

## 语法

### 类型所占字节多少？

byte 1

short 2

int 4

long 8

float 4

double 8

### short

short s1 = 1;

s1 = s1 + 1;编译错误，会认为（s1 + 1）是int类型，不能将int 转化为short

### int，Integer

- int是原生类型，不能和面向对象的类进行交互。例如添加到ArrayList中

### float

2.00-1.10得数0.89999999999

因为二进制无法很好表示浮点数，得用BigDecimal   

## 面向对象

###  private

private不能用于局部变量

### final

当final指向的是对象，对象的属性

还是可以改变的。

### 多态

Fruit fruit = apple ;是超类

多态仅对方法有效：fruit.print();调用的方法是apple类的方法，而fruit.name的成员变量则是Fruit类的成员变量

fruit.setDate(new Date());如果有参数且参数不一样，则不构成多态，调用的还是父类fruit方法

### abstract

abstract的用法：模板方法，在abstract类中定义方法名的估计，子类extends父类，实现该方法。







热身2	23:00



