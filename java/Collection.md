# Collection接口

| 方法名称                         | 内容           |
| ---------------------------- | ------------ |
| boolean add（E e）             | 添加到集合中       |
| void clear()                 | 清空当前所有元素     |
| boolean remove(E e)          | 给定对象在当前集合中删去 |
| boolean contains（Object obj） | 判断是否包含给定对象   |
| boolean isEmpty()            | 判断集合是否为空     |
| int size（）                   | 返回集合长度       |

因为list可以用for循环，Set不可以，所以都可以用

方法，迭代器遍历集合不依赖索引

```java
Iterator<String> it = list.iterator
//当前元素是否存在
boolean flag = it.hasnext();
//指向当前元素，返回值，
String str = it.next();
System.out.println(str);
```

1.迭代器遍历完毕，指针不复位

2.循环中只能用一次next方法，因为每次都会移动指针，挪到最后时再移动会指空

3.迭代器遍历时，不能用集合方法删除或增加，可以用迭代器的方法来删除



## 1.list接口

有序，可重复，有索引

| 方法                          | 内容                  |
| --------------------------- | ------------------- |
| void add(int index,element) | 指定位置插入指定元素          |
| E remove(int index)         | 删除指定索引处对象，返回被删除的元素  |
| E set(int index,E element)  | 修改指定索引处的元素，返回被修改的元素 |
| E get(int index)            | 返回指定索引处的元素          |

### 1.1.ArrayList实现类

底层是数组

### 1.2.LinkedList实现类

底层是双链表，查询慢，首尾操作快

| 方法                 | 内容             |
| ------------------ | -------------- |
| void addFirst(E e) | 开头插入指定元素       |
| void addLast(E e)  | 指定元素追加到此列表的末尾  |
| E getFirst()       | 返回列表中第一个元素     |
| E getLast()        | 返回列表中最后一个元素    |
| E removeFirst()    | 此列表中删除并返回第一个元素 |
| E removeLast()     | 列表删除并返回最后一个元素  |





### 1.3.Vector



## 2.Set接口

无序，不重复，无索引

### 2.1.hashSet



### 2.2.TreeSet


