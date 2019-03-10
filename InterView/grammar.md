# 集合

## 集合1

M：**ArrayList&Vector&LinkedList的区别 ？**

Z：相同点，三者都是有序集合

Z：不同点

### List1.Vector

Vector的特性是 线程安全，动态数组。

线程安全：是有额外开销的。

动态数组：数组满的时候，创建新的数组，拷贝原有数组。动态数组结构适合访问，因为是顺序存储的。但不适合插入，删除数据，因为需要挪动所有后序元素。

### List2.ArrayList

ArrayList的特性是 动态数组

ArrayList动态数组：数组的扩容同Vector动态数组，但Vector每次提高1倍，而ArrayList每次提高50%

线程安全：本身非线程安全，可以利用``Collections.synchronizedList(new ArrayList());``实现线程安全，原理就是往基本方法的编辑操作（add，get，set）添加synchronizd同步支持

### List3.LinkList

ArrayList的特性是 双向链表  

双向链表：插入和删除比较高效，随机访问则比较慢

### Collection

Z:Collection接口是所有集合的根，展开三类集合：

- List	有序集合
- Set 不允许重复元素
  - TreeSet的特性 顺序访问，但添加删除操作低效。基于TreeMap实现。
  - HashSet的特性 无序，添加删除操作如常数时间，遍历性能与底层HashMap容量有关。
  - LinkedHashSet 有序，添加删除操作如常数时间，因维护链表性能略低HashSet，遍历性能以元素多少有关
- Queue 先入先出，后入后出，常用于并发编程场景

### 排序

Z：java的默认排序，分为以下两种情况：

- 原始数据类型
  - 快速排序的改进版，双轴快速排序
- 对象数据
  - 归并和二分插入排序结合版，TimSort

Java8提供并行排序算法，利用多核处理器的计算能力，主要针对百万级别数据

## 集合2

M：**对比 Hashtable、HashMap、TreeMap 有什么不同？**  

Z：相同点，三者都是Map实现，键值对形式存储和操作数据

Z：不同点

### Map1.Hashtable

Hashtable同步的，性能开销，不支持null的键值

结构：扩展了Dictionary 类，与扩展AbstractMap的HashMap，TreeMap结构大有不同。

### Map2.HashMap

HashMap非同步的，支持null的键值

结构：数组+链表，哈希值决定数组的寻址，哈希值相同的键对，以链表存储。

线程安全：本身非线程安全，可以利用``Collections.synchronizedMap(new HashMap());``实现线程安全

LinkedHashMap遍历顺序符合插入顺序，通过维护双向链表实现。特定场景：可以定义删除策略，将不常用对象释放掉。

### Map3.TreeMap

TreeMap有序的，顺序基于红黑树算法，操作数据是O(log(n))的时间复杂度，可以通过Comparator定制顺序，也可以Comparable自然顺序

### 哈希冲突

M：怎么解决哈希冲突呢？

Z：解决方式其中两种：

- 开放地址法：当关键字key的哈希地址冲突时，产生新的哈希地址，一直到不冲突为止
- 建立溢出表：当基础表冲突的元素，填入溢出表中