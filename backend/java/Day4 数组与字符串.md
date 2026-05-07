# Day4 数组与字符串

## 一、Java 数组

数组是用来存储固定大小的同类型元素的数据结构。

### 1.1 声明数组变量

```java
dataType[] arrayRefVar;  // 推荐方式
dataType arrayRefVar[];  // 兼容 C/C++ 风格
```

### 1.2 创建数组

**方式一：使用 new 操作符**

```java
arrayRefVar = new dataType[arraySize];
```

**方式二：声明和创建合并**

```java
dataType[] arrayRefVar = new dataType[arraySize];
```

**方式三：直接初始化**

```java
dataType[] arrayRefVar = {value0, value1, ..., valuek};
```

### 1.3 数组示例

**TestArray.java 文件代码：**

```java
public class TestArray {
    public static void main(String[] args) {
        int size = 10;
        double[] myList = new double[size];
        
        myList[0] = 5.6;
        myList[1] = 4.5;
        myList[2] = 3.3;
        myList[3] = 13.2;
        myList[4] = 4.0;
        myList[5] = 34.33;
        myList[6] = 34.0;
        myList[7] = 45.45;
        myList[8] = 99.993;
        myList[9] = 11123;
        
        double total = 0;
        for (int i = 0; i < size; i++) {
            total += myList[i];
        }
        
        System.out.println("总和为： " + total);
    }
}
```

输出结果：

```
总和为： 11367.373
```

### 1.4 处理数组

**TestArray.java 文件代码：**

```java
public class TestArray {
    public static void main(String[] args) {
        double[] myList = {1.9, 2.9, 3.4, 3.5};
        
        // 打印所有元素
        for (int i = 0; i < myList.length; i++) {
            System.out.println(myList[i] + " ");
        }
        
        // 计算总和
        double total = 0;
        for (int i = 0; i < myList.length; i++) {
            total += myList[i];
        }
        System.out.println("Total is " + total);
        
        // 查找最大值
        double max = myList[0];
        for (int i = 1; i < myList.length; i++) {
            if (myList[i] > max) max = myList[i];
        }
        System.out.println("Max is " + max);
    }
}
```

输出结果：

```
1.9 
2.9 
3.4 
3.5 
Total is 11.7
Max is 3.5
```

### 1.5 For-Each 循环

```java
public class TestArray {
    public static void main(String[] args) {
        double[] myList = {1.9, 2.9, 3.4, 3.5};
        
        for (double element : myList) {
            System.out.println(element);
        }
    }
}
```

输出结果：

```
1.9
2.9
3.4
3.5
```

### 1.6 数组作为函数参数

```java
public static void printArray(int[] array) {
    for (int i = 0; i < array.length; i++) {
        System.out.print(array[i] + " ");
    }
}

// 调用
printArray(new int[]{3, 1, 2, 6, 4, 2});
```

### 1.7 数组作为函数返回值

```java
public static int[] reverse(int[] list) {
    int[] result = new int[list.length];
    
    for (int i = 0, j = result.length - 1; i < list.length; i++, j--) {
        result[j] = list[i];
    }
    
    return result;
}
```

### 1.8 多维数组

```java
// 二维数组声明
int[][] a = new int[2][3];

// 二维数组初始化
String[][] s = new String[2][];
s[0] = new String[2];
s[1] = new String[3];
s[0][0] = "Good";
s[0][1] = "Luck";
s[1][0] = "to";
s[1][1] = "you";
s[1][2] = "!";

// 访问二维数组元素
int[][] matrix = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
System.out.println(matrix[1][2]); // 6
```

### 1.9 Arrays 工具类

```java
import java.util.Arrays;

int[] numbers = {3, 1, 4, 1, 5, 9};

// 排序
Arrays.sort(numbers);

// 二分查找
int index = Arrays.binarySearch(numbers, 4);

// 填充
int[] filled = new int[5];
Arrays.fill(filled, 10);

// 比较
int[] arr1 = {1, 2, 3};
int[] arr2 = {1, 2, 3};
boolean equal = Arrays.equals(arr1, arr2);

// 数组转字符串
System.out.println(Arrays.toString(numbers));
```

---

## 二、Java String 类

字符串广泛应用在 Java 编程中，Java 提供了 String 类来创建和操作字符串。

### 2.1 创建字符串

```java
// 方式1：直接赋值（存储在字符串常量池）
String str = "Runoob";

// 方式2：使用构造函数（存储在堆上）
String str2 = new String("Runoob");

// 方式3：从字符数组创建
char[] helloArray = {'r', 'u', 'n', 'o', 'o', 'b'};
String helloString = new String(helloArray);
```

**StringDemo.java 文件代码：**

```java
public class StringDemo {
    public static void main(String args[]) {
        char[] helloArray = {'r', 'u', 'n', 'o', 'o', 'b'};
        String helloString = new String(helloArray);
        System.out.println(helloString);
    }
}
```

输出结果：

```
runoob
```

### 2.2 字符串长度

```java
public class StringDemo {
    public static void main(String args[]) {
        String site = "www.runoob.com";
        int len = site.length();
        System.out.println("菜鸟教程网址长度 : " + len);
    }
}
```

输出结果：

```
菜鸟教程网址长度 : 14
```

### 2.3 连接字符串

```java
// 使用 concat() 方法
string1.concat(string2);

// 使用 + 操作符（更常用）
"Hello," + " runoob" + "!";
```

**StringDemo.java 文件代码：**

```java
public class StringDemo {
    public static void main(String args[]) {
        String string1 = "菜鸟教程网址：";
        System.out.println("1、" + string1 + "www.runoob.com");
    }
}
```

输出结果：

```
1、菜鸟教程网址：www.runoob.com
```

### 2.4 创建格式化字符串

```java
// 使用 printf()
System.out.printf("浮点型变量的值为 %f, 整型变量的值为 %d", floatVar, intVar);

// 使用 String.format()
String fs = String.format("浮点型变量的值为 %f, 整型变量的值为 %d", floatVar, intVar);
```

### 2.5 字符串比较

```java
String str1 = "Hello";
String str2 = "Hello";
String str3 = new String("Hello");

// == 比较引用（地址）
System.out.println(str1 == str2);   // true（同一对象）
System.out.println(str1 == str3);   // false（不同对象）

// equals 比较内容
System.out.println(str1.equals(str3)); // true

// equalsIgnoreCase 忽略大小写
System.out.println(str1.equalsIgnoreCase("hello")); // true
```

### 2.6 常用字符串方法

```java
String str = "Hello, World!";

// 获取长度
int length = str.length(); // 13

// 获取指定索引字符
char ch = str.charAt(0); // 'H'

// 查找子串位置
int index = str.indexOf("World"); // 7
int lastIndex = str.lastIndexOf("o"); // 8

// 截取子串
String sub = str.substring(7);      // "World!"
String sub2 = str.substring(0, 5);  // "Hello"

// 替换
String replaced = str.replace("World", "Java");

// 分割
String[] parts = str.split(",");

// 转换大小写
String upper = str.toUpperCase();
String lower = str.toLowerCase();

// 去除首尾空白
String trimmed = "  Hello  ".trim();

// 判断是否包含
boolean contains = str.contains("World");

// 判断开头/结尾
boolean startsWith = str.startsWith("Hello");
boolean endsWith = str.endsWith("!");
```

### 2.7 字符串与基本类型转换

```java
// 基本类型转字符串
int num = 123;
String strNum = String.valueOf(num);
String strNum2 = Integer.toString(num);

// 字符串转基本类型
String str = "456";
int num2 = Integer.parseInt(str);
double d = Double.parseDouble("3.14");
```

### 2.8 StringBuilder 与 StringBuffer

**StringBuilder（非线程安全，效率高）：**

```java
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" ");
sb.append("World");
sb.insert(5, ",");
sb.delete(5, 6);
sb.reverse();
String result = sb.toString();
```

**StringBuffer（线程安全，效率较低）：**

```java
StringBuffer sbf = new StringBuffer();
sbf.append("Hello").append(" World");
```

### 2.9 String、StringBuilder、StringBuffer 对比

| 类 | 可变性 | 线程安全 | 效率 |
|----|--------|----------|------|
| String | 不可变 | 是 | 低（每次修改创建新对象） |
| StringBuilder | 可变 | 否 | 高 |
| StringBuffer | 可变 | 是 | 中（有同步开销） |

---

## 三、练习

1. 编写程序找出数组中的最大值和最小值
2. 使用 Arrays.sort() 对数组进行排序
3. 编写程序反转字符串
4. 统计字符串中每个字符出现的次数
5. 判断一个字符串是否为回文字符串