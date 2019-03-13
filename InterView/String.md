# 字符串

M：理解 Java 的字符串，String、StringBuffer、StringBuilder 有什么区别？

### String

Z：String：由final修饰

操作：所以对字符串的操作都会产生新的String，对性能影响比较大。

### StringBuffer

StringBuffer：线程安全，需要更多的性能。可修改的字符序列

底层：可修改的数组，加了synchronized。默认长度16，扩容时进行arraycopy，抛弃原先数组

### StringBuilder

StringBuilder：线程不安全，可修改的字符序列  

底层：可修改的数组

### 缓存

Z：因为字符串的大量重复，所以JDK将字符串常量储存起来

- intern：JDK6提供，存在OOM风险。需用手动调用。
- MetaSpace（元数据区）：替代 永久带，避免了占满