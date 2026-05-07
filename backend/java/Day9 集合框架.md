# Day9 集合框架

## 一、Java 集合框架概述

早在 Java 2 之前，Java 就提供了特设类（如 Dictionary、Vector、Stack 和 Properties）来存储和操作对象组。但这些类缺少一个核心统一的主题，使用方式各不相同。

集合框架被设计成要满足以下几个目标：
- 高性能：基本集合的实现必须是高效的
- 互操作性：允许不同类型的集合以类似的方式工作
- 易扩展：对集合的扩展和适应必须是简单的

整个集合框架围绕一组标准接口而设计，你可以直接使用这些接口的标准实现，也可以通过这些接口实现自己的集合。

### 1.1 集合框架体系

Java 集合框架主要包括两种类型的容器：
- **Collection（集合）**：存储一个元素集合
- **Map（图）**：存储键/值对映射

Collection 接口有 3 种子类型：List、Set 和 Queue，下面是一些抽象类，最后是具体实现类，常用的有 ArrayList、LinkedList、HashSet、HashMap 等。

### 1.2 集合接口

| 接口 | 描述 |
| --- | --- |
| Collection | 最基本的集合接口，存储一组不唯一、无序的对象 |
| List | 有序的 Collection，允许有相同元素，可通过索引访问 |
| Set | 不保存重复的元素，存储一组唯一、无序的对象 |
| Map | 存储一组键值对象，提供 key 到 value 的映射 |

### 1.3 Set 和 List 的区别

- Set 接口实例存储的是无序的、不重复的数据；List 接口实例存储的是有序的、可以重复的元素
- Set 检索效率低下，删除和插入效率高；List 查找元素效率高，插入删除效率低

---

## 二、ArrayList

ArrayList 类是一个可以动态修改的数组，与普通数组的区别是没有固定大小的限制，可以添加或删除元素。

### 2.1 创建 ArrayList

```java
import java.util.ArrayList;

ArrayList<String> sites = new ArrayList<String>();
```

### 2.2 添加元素

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites);
    }
}
```

输出结果：

```
[Google, Runoob, Taobao, Weibo]
```

### 2.3 访问元素

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites.get(1)); // 访问第二个元素
    }
}
```

输出结果：

```
Runoob
```

### 2.4 修改元素

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        sites.set(2, "Wiki"); // 修改第三个元素
        System.out.println(sites);
    }
}
```

输出结果：

```
[Google, Runoob, Wiki, Weibo]
```

### 2.5 删除元素

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        sites.remove(3); // 删除第四个元素
        System.out.println(sites);
    }
}
```

输出结果：

```
[Google, Runoob, Taobao]
```

### 2.6 计算大小

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        System.out.println(sites.size());
    }
}
```

输出结果：

```
4
```

### 2.7 迭代数组列表

```java
import java.util.ArrayList;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        
        // 使用 for 循环
        for (int i = 0; i < sites.size(); i++) {
            System.out.println(sites.get(i));
        }
        
        // 使用 for-each
        for (String i : sites) {
            System.out.println(i);
        }
    }
}
```

输出结果：

```
Google
Runoob
Taobao
Weibo
```

### 2.8 ArrayList 排序

```java
import java.util.ArrayList;
import java.util.Collections;

public class RunoobTest {
    public static void main(String[] args) {
        ArrayList<String> sites = new ArrayList<String>();
        sites.add("Taobao");
        sites.add("Wiki");
        sites.add("Runoob");
        sites.add("Weibo");
        sites.add("Google");
        
        Collections.sort(sites); // 字母排序
        
        for (String i : sites) {
            System.out.println(i);
        }
    }
}
```

输出结果：

```
Google
Runoob
Taobao
Weibo
Wiki
```

---

## 三、LinkedList

LinkedList（链表）类似于 ArrayList，是一种常用的数据容器。与 ArrayList 相比，LinkedList 的增加和删除操作效率更高，而查找和修改的操作效率较低。

### 3.1 创建 LinkedList

```java
import java.util.LinkedList;

LinkedList<String> sites = new LinkedList<String>();
```

### 3.2 在列表开头添加元素

```java
import java.util.LinkedList;

public class RunoobTest {
    public static void main(String[] args) {
        LinkedList<String> sites = new LinkedList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.addFirst("Wiki"); // 在头部添加元素
        System.out.println(sites);
    }
}
```

输出结果：

```
[Wiki, Google, Runoob, Taobao]
```

### 3.3 在列表结尾添加元素

```java
import java.util.LinkedList;

public class RunoobTest {
    public static void main(String[] args) {
        LinkedList<String> sites = new LinkedList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.addLast("Wiki"); // 在尾部添加元素
        System.out.println(sites);
    }
}
```

输出结果：

```
[Google, Runoob, Taobao, Wiki]
```

### 3.4 在列表开头移除元素

```java
import java.util.LinkedList;

public class RunoobTest {
    public static void main(String[] args) {
        LinkedList<String> sites = new LinkedList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        sites.removeFirst(); // 移除头部元素
        System.out.println(sites);
    }
}
```

输出结果：

```
[Runoob, Taobao, Weibo]
```

### 3.5 在列表结尾移除元素

```java
import java.util.LinkedList;

public class RunoobTest {
    public static void main(String[] args) {
        LinkedList<String> sites = new LinkedList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        sites.removeLast(); // 移除尾部元素
        System.out.println(sites);
    }
}
```

输出结果：

```
[Google, Runoob, Taobao]
```

### 3.6 获取列表开头和结尾的元素

```java
import java.util.LinkedList;

public class RunoobTest {
    public static void main(String[] args) {
        LinkedList<String> sites = new LinkedList<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Weibo");
        
        System.out.println(sites.getFirst()); // 获取头部元素
        System.out.println(sites.getLast());  // 获取尾部元素
    }
}
```

输出结果：

```
Google
Weibo
```

---

## 四、HashSet

HashSet 基于 HashMap 来实现的，是一个不允许有重复元素的集合。

HashSet 允许有 null 值，是无序的，即不会记录插入的顺序。HashSet 不是线程安全的。

### 4.1 创建 HashSet

```java
import java.util.HashSet;

HashSet<String> sites = new HashSet<String>();
```

### 4.2 添加元素

```java
import java.util.HashSet;

public class RunoobTest {
    public static void main(String[] args) {
        HashSet<String> sites = new HashSet<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Zhihu");
        sites.add("Runoob"); // 重复的元素不会被添加
        System.out.println(sites);
    }
}
```

输出结果：

```
[Google, Runoob, Zhihu, Taobao]
```

### 4.3 判断元素是否存在

```java
import java.util.HashSet;

public class RunoobTest {
    public static void main(String[] args) {
        HashSet<String> sites = new HashSet<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Zhihu");
        System.out.println(sites.contains("Taobao"));
    }
}
```

输出结果：

```
true
```

### 4.4 删除元素

```java
import java.util.HashSet;

public class RunoobTest {
    public static void main(String[] args) {
        HashSet<String> sites = new HashSet<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Zhihu");
        sites.remove("Taobao"); // 删除元素
        System.out.println(sites);
    }
}
```

输出结果：

```
[Google, Runoob, Zhihu]
```

### 4.5 计算大小

```java
import java.util.HashSet;

public class RunoobTest {
    public static void main(String[] args) {
        HashSet<String> sites = new HashSet<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Zhihu");
        System.out.println(sites.size());
    }
}
```

输出结果：

```
4
```

### 4.6 迭代 HashSet

```java
import java.util.HashSet;

public class RunoobTest {
    public static void main(String[] args) {
        HashSet<String> sites = new HashSet<String>();
        sites.add("Google");
        sites.add("Runoob");
        sites.add("Taobao");
        sites.add("Zhihu");
        
        for (String i : sites) {
            System.out.println(i);
        }
    }
}
```

输出结果：

```
Google
Runoob
Zhihu
Taobao
```

---

## 五、HashMap

HashMap 是一个散列表，它存储的内容是键值对(key-value)映射。

HashMap 实现了 Map 接口，根据键的 HashCode 值存储数据，具有很快的访问速度，最多允许一条记录的键为 null，不支持线程同步。

### 5.1 创建 HashMap

```java
import java.util.HashMap;

HashMap<Integer, String> sites = new HashMap<Integer, String>();
```

### 5.2 添加元素

```java
import java.util.HashMap;

public class RunoobTest {
    public static void main(String[] args) {
        HashMap<Integer, String> sites = new HashMap<Integer, String>();
        sites.put(1, "Google");
        sites.put(2, "Runoob");
        sites.put(3, "Taobao");
        sites.put(4, "Zhihu");
        System.out.println(sites);
    }
}
```

输出结果：

```
{1=Google, 2=Runoob, 3=Taobao, 4=Zhihu}
```

### 5.3 访问元素

```java
import java.util.HashMap;

public class RunoobTest {
    public static void main(String[] args) {
        HashMap<Integer, String> sites = new HashMap<Integer, String>();
        sites.put(1, "Google");
        sites.put(2, "Runoob");
        sites.put(3, "Taobao");
        sites.put(4, "Zhihu");
        System.out.println(sites.get(3));
    }
}
```

输出结果：

```
Taobao
```

### 5.4 删除元素

```java
import java.util.HashMap;

public class RunoobTest {
    public static void main(String[] args) {
        HashMap<Integer, String> sites = new HashMap<Integer, String>();
        sites.put(1, "Google");
        sites.put(2, "Runoob");
        sites.put(3, "Taobao");
        sites.put(4, "Zhihu");
        sites.remove(4);
        System.out.println(sites);
    }
}
```

输出结果：

```
{1=Google, 2=Runoob, 3=Taobao}
```

### 5.5 计算大小

```java
import java.util.HashMap;

public class RunoobTest {
    public static void main(String[] args) {
        HashMap<Integer, String> sites = new HashMap<Integer, String>();
        sites.put(1, "Google");
        sites.put(2, "Runoob");
        sites.put(3, "Taobao");
        sites.put(4, "Zhihu");
        System.out.println(sites.size());
    }
}
```

输出结果：

```
4
```

### 5.6 迭代 HashMap

```java
import java.util.HashMap;

public class RunoobTest {
    public static void main(String[] args) {
        HashMap<Integer, String> sites = new HashMap<Integer, String>();
        sites.put(1, "Google");
        sites.put(2, "Runoob");
        sites.put(3, "Taobao");
        sites.put(4, "Zhihu");
        
        // 输出 key 和 value
        for (Integer i : sites.keySet()) {
            System.out.println("key: " + i + " value: " + sites.get(i));
        }
        
        // 返回所有 value 值
        for (String value : sites.values()) {
            System.out.print(value + ", ");
        }
    }
}
```

输出结果：

```
key: 1 value: Google
key: 2 value: Runoob
key: 3 value: Taobao
key: 4 value: Zhihu
Google, Runoob, Taobao, Zhihu,
```

---

## 六、Collections 工具类

Collections 类提供了很多有用的方法，如排序、反转、打乱顺序等。

```java
import java.util.ArrayList;
import java.util.Collections;

public class CollectionsExample {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(3);
        list.add(1);
        list.add(4);
        list.add(2);
        
        // 排序
        Collections.sort(list);
        System.out.println("排序后: " + list);
        
        // 反转
        Collections.reverse(list);
        System.out.println("反转后: " + list);
        
        // 打乱顺序
        Collections.shuffle(list);
        System.out.println("打乱后: " + list);
        
        // 查找（需先排序）
        Collections.sort(list);
        int index = Collections.binarySearch(list, 3);
        System.out.println("3 的索引: " + index);
        
        // 最大值/最小值
        int max = Collections.max(list);
        int min = Collections.min(list);
        System.out.println("最大值: " + max + ", 最小值: " + min);
    }
}
```

---

## 七、练习

1. 使用 ArrayList 存储学生信息，实现增删改查
2. 使用 HashSet 去除重复元素
3. 使用 HashMap 统计字符串中每个字符出现的次数
4. 使用 TreeSet 对自定义对象进行排序
5. 使用 Collections 工具类进行排序、反转等操作