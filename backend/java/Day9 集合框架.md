# Day9 集合框架

## 一、集合框架概述

### 1.1 集合框架层次结构

```
Collection
├── List（有序、可重复）
│   ├── ArrayList
│   ├── LinkedList
│   └── Vector
├── Set（无序、不可重复）
│   ├── HashSet
│   ├── LinkedHashSet
│   └── TreeSet
└── Queue（队列）
    ├── LinkedList
    └── PriorityQueue

Map（键值对）
├── HashMap
├── LinkedHashMap
├── TreeMap
└── Hashtable
```

### 1.2 集合与数组的区别

| 特性 | 数组 | 集合 |
|------|------|------|
| 大小 | 固定 | 动态 |
| 类型 | 单一 | 多样 |
| 方法 | 基本 | 丰富 |
| 存储 | 基本类型/对象 | 对象 |

## 二、List 接口

### 2.1 ArrayList

```java
import java.util.ArrayList;
import java.util.List;

public class ArrayListExample {
    public static void main(String[] args) {
        // 创建 ArrayList
        List<String> names = new ArrayList<>();
        
        // 添加元素
        names.add("张三");
        names.add("李四");
        names.add("王五");
        
        // 获取元素
        String first = names.get(0);
        System.out.println("第一个元素: " + first);
        
        // 修改元素
        names.set(1, "赵六");
        
        // 删除元素
        names.remove(2);
        
        // 遍历
        for (String name : names) {
            System.out.println(name);
        }
        
        // 其他常用方法
        System.out.println("大小: " + names.size());
        System.out.println("是否为空: " + names.isEmpty());
        System.out.println("是否包含: " + names.contains("张三"));
    }
}
```

### 2.2 LinkedList

```java
import java.util.LinkedList;

public class LinkedListExample {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();
        
        // 添加元素
        list.addFirst("第一个");
        list.addLast("最后一个");
        list.add(1, "中间");
        
        // 获取元素
        System.out.println("第一个: " + list.getFirst());
        System.out.println("最后一个: " + list.getLast());
        
        // 删除元素
        list.removeFirst();
        list.removeLast();
        
        // 队列操作
        list.offer("A");
        list.offer("B");
        System.out.println("出队: " + list.poll());
        
        // 栈操作
        list.push("X");
        list.push("Y");
        System.out.println("出栈: " + list.pop());
    }
}
```

### 2.3 ArrayList vs LinkedList

| 特性 | ArrayList | LinkedList |
|------|-----------|------------|
| 底层实现 | 数组 | 双向链表 |
| 随机访问 | 快 | 慢 |
| 插入删除 | 慢（需移动元素） | 快 |
| 内存占用 | 连续空间 | 每个节点有额外开销 |

## 三、Set 接口

### 3.1 HashSet

```java
import java.util.HashSet;
import java.util.Set;

public class HashSetExample {
    public static void main(String[] args) {
        Set<String> fruits = new HashSet<>();
        
        // 添加元素（自动去重）
        fruits.add("苹果");
        fruits.add("香蕉");
        fruits.add("苹果"); // 重复，不会添加
        
        // 遍历
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
        
        // 常用方法
        System.out.println("大小: " + fruits.size());
        System.out.println("是否包含香蕉: " + fruits.contains("香蕉"));
        fruits.remove("香蕉");
    }
}
```

### 3.2 LinkedHashSet

```java
import java.util.LinkedHashSet;

public class LinkedHashSetExample {
    public static void main(String[] args) {
        // 保持插入顺序
        LinkedHashSet<String> set = new LinkedHashSet<>();
        set.add("D");
        set.add("A");
        set.add("B");
        set.add("C");
        
        // 输出顺序与插入顺序一致
        for (String item : set) {
            System.out.println(item); // D, A, B, C
        }
    }
}
```

### 3.3 TreeSet

```java
import java.util.TreeSet;

public class TreeSetExample {
    public static void main(String[] args) {
        // 自动排序
        TreeSet<Integer> numbers = new TreeSet<>();
        numbers.add(5);
        numbers.add(1);
        numbers.add(3);
        numbers.add(7);
        
        // 自然排序输出
        for (Integer num : numbers) {
            System.out.println(num); // 1, 3, 5, 7
        }
        
        // 特殊方法
        System.out.println("最小: " + numbers.first());
        System.out.println("最大: " + numbers.last());
        System.out.println("小于5的最大: " + numbers.lower(5));
        System.out.println("大于5的最小: " + numbers.higher(5));
    }
}
```

## 四、Map 接口

### 4.1 HashMap

```java
import java.util.HashMap;
import java.util.Map;

public class HashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> scores = new HashMap<>();
        
        // 添加键值对
        scores.put("张三", 90);
        scores.put("李四", 85);
        scores.put("王五", 95);
        
        // 获取值
        int zhangScore = scores.get("张三");
        System.out.println("张三的分数: " + zhangScore);
        
        // 修改值
        scores.put("李四", 88);
        
        // 遍历方式1：遍历键
        for (String name : scores.keySet()) {
            System.out.println(name + ": " + scores.get(name));
        }
        
        // 遍历方式2：遍历键值对
        for (Map.Entry<String, Integer> entry : scores.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
        
        // 常用方法
        System.out.println("大小: " + scores.size());
        System.out.println("是否包含张三: " + scores.containsKey("张三"));
        System.out.println("是否包含90分: " + scores.containsValue(90));
        scores.remove("王五");
    }
}
```

### 4.2 LinkedHashMap

```java
import java.util.LinkedHashMap;

public class LinkedHashMapExample {
    public static void main(String[] args) {
        // 保持插入顺序
        LinkedHashMap<String, String> map = new LinkedHashMap<>();
        map.put("B", "Banana");
        map.put("A", "Apple");
        map.put("C", "Cherry");
        
        // 按插入顺序输出
        for (Map.Entry<String, String> entry : map.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

### 4.3 TreeMap

```java
import java.util.TreeMap;

public class TreeMapExample {
    public static void main(String[] args) {
        // 按键排序
        TreeMap<String, Integer> map = new TreeMap<>();
        map.put("B", 2);
        map.put("A", 1);
        map.put("C", 3);
        
        // 按键的自然顺序输出
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

## 五、Collections 工具类

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CollectionsExample {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        list.add(3);
        list.add(1);
        list.add(4);
        list.add(2);
        
        // 排序
        Collections.sort(list);
        
        // 反转
        Collections.reverse(list);
        
        // 打乱顺序
        Collections.shuffle(list);
        
        // 查找（需先排序）
        Collections.sort(list);
        int index = Collections.binarySearch(list, 3);
        
        // 填充
        Collections.fill(list, 0);
        
        // 最大值/最小值
        int max = Collections.max(list);
        int min = Collections.min(list);
    }
}
```

## 六、泛型

### 6.1 泛型的使用

```java
// 定义泛型类
public class Box<T> {
    private T item;
    
    public void setItem(T item) {
        this.item = item;
    }
    
    public T getItem() {
        return item;
    }
}

// 使用泛型类
public class BoxExample {
    public static void main(String[] args) {
        Box<String> stringBox = new Box<>();
        stringBox.setItem("Hello");
        String str = stringBox.getItem();
        
        Box<Integer> intBox = new Box<>();
        intBox.setItem(123);
        Integer num = intBox.getItem();
    }
}
```

### 6.2 泛型方法

```java
public class GenericMethodExample {
    public static <T> void printArray(T[] array) {
        for (T item : array) {
            System.out.println(item);
        }
    }
    
    public static void main(String[] args) {
        Integer[] intArray = {1, 2, 3, 4, 5};
        String[] strArray = {"A", "B", "C"};
        
        printArray(intArray);
        printArray(strArray);
    }
}
```

## 七、练习

1. 使用 ArrayList 存储学生信息，实现增删改查
2. 使用 HashSet 去除重复元素
3. 使用 HashMap 统计字符串中每个字符出现的次数
4. 使用 TreeSet 对自定义对象进行排序
5. 使用 Collections 工具类进行排序、反转等操作