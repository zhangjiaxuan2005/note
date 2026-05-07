# Day4 数组与字符串

## 一、数组

### 1.1 数组的定义与初始化

```java
// 方式1：声明并初始化
int[] numbers = {1, 2, 3, 4, 5};

// 方式2：先声明，后初始化
int[] scores = new int[5];
scores[0] = 90;
scores[1] = 85;
scores[2] = 95;
scores[3] = 88;
scores[4] = 92;

// 方式3：声明时指定长度
String[] names = new String[3];
names[0] = "张三";
names[1] = "李四";
names[2] = "王五";
```

### 1.2 数组的访问

```java
int[] numbers = {10, 20, 30, 40, 50};

// 访问数组元素
System.out.println(numbers[0]); // 输出第一个元素
System.out.println(numbers[2]); // 输出第三个元素

// 修改数组元素
numbers[1] = 25;

// 获取数组长度
int length = numbers.length;
System.out.println("数组长度: " + length);
```

### 1.3 数组遍历

```java
int[] numbers = {1, 2, 3, 4, 5};

// 方式1：for 循环
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}

// 方式2：增强 for 循环
for (int num : numbers) {
    System.out.println(num);
}

// 方式3：Java 8+ forEach
Arrays.stream(numbers).forEach(System.out::println);
```

### 1.4 多维数组

```java
// 二维数组
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// 访问二维数组元素
System.out.println(matrix[0][0]); // 1
System.out.println(matrix[1][2]); // 6

// 遍历二维数组
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

### 1.5 Arrays 工具类

```java
import java.util.Arrays;

int[] numbers = {3, 1, 4, 1, 5, 9};

// 排序
Arrays.sort(numbers);
System.out.println(Arrays.toString(numbers)); // [1, 1, 3, 4, 5, 9]

// 二分查找（需先排序）
int index = Arrays.binarySearch(numbers, 4);
System.out.println("4 的索引: " + index); // 3

// 数组拷贝
int[] copy = Arrays.copyOf(numbers, 3);
System.out.println(Arrays.toString(copy)); // [1, 1, 3]

// 填充
int[] filled = new int[5];
Arrays.fill(filled, 10);
System.out.println(Arrays.toString(filled)); // [10, 10, 10, 10, 10]

// 比较两个数组是否相等
int[] arr1 = {1, 2, 3};
int[] arr2 = {1, 2, 3};
boolean equal = Arrays.equals(arr1, arr2);
System.out.println(equal); // true
```

## 二、字符串

### 2.1 String 类的特点
- String 是不可变的（immutable）
- 字符串常量池（String Pool）优化

### 2.2 String 的创建

```java
// 方式1：直接赋值（会放入字符串常量池）
String str1 = "Hello";

// 方式2：使用 new 关键字（创建新对象）
String str2 = new String("Hello");

// 方式3：字符串拼接
String str3 = "Hello" + " World";
```

### 2.3 字符串比较

```java
String str1 = "Hello";
String str2 = "Hello";
String str3 = new String("Hello");

// == 比较引用（地址）
System.out.println(str1 == str2);   // true（同一对象）
System.out.println(str1 == str3);   // false（不同对象）

// equals 比较内容
System.out.println(str1.equals(str2)); // true
System.out.println(str1.equals(str3)); // true

// equalsIgnoreCase 忽略大小写比较
String str4 = "hello";
System.out.println(str1.equalsIgnoreCase(str4)); // true
```

### 2.4 常用字符串方法

```java
String str = "Hello, World!";

// 获取长度
int length = str.length(); // 13

// 获取字符
char ch = str.charAt(0); // 'H'

// 查找子串位置
int index = str.indexOf("World"); // 7
int lastIndex = str.lastIndexOf("o"); // 8

// 截取子串
String sub = str.substring(7);      // "World!"
String sub2 = str.substring(0, 5);  // "Hello"

// 替换
String replaced = str.replace("World", "Java"); // "Hello, Java!"

// 分割
String[] parts = str.split(","); // ["Hello", " World!"]

// 转换大小写
String upper = str.toUpperCase();   // "HELLO, WORLD!"
String lower = str.toLowerCase();   // "hello, world!"

// 去除首尾空白
String trimmed = "  Hello  ".trim(); // "Hello"

// 判断是否包含子串
boolean contains = str.contains("World"); // true

// 判断是否以指定字符串开头/结尾
boolean startsWith = str.startsWith("Hello"); // true
boolean endsWith = str.endsWith("!");         // true

// 判断是否为空
boolean empty = str.isEmpty(); // false

// 字符串拼接
String combined = String.join("-", "a", "b", "c"); // "a-b-c"
```

### 2.5 字符串与基本类型转换

```java
// 基本类型转字符串
int num = 123;
String strNum = String.valueOf(num); // "123"
String strNum2 = Integer.toString(num); // "123"

// 字符串转基本类型
String str = "456";
int num2 = Integer.parseInt(str); // 456
double d = Double.parseDouble("3.14"); // 3.14

// 避免 NumberFormatException
try {
    int invalid = Integer.parseInt("abc");
} catch (NumberFormatException e) {
    System.out.println("格式错误");
}
```

### 2.6 StringBuilder 与 StringBuffer

```java
// StringBuilder（非线程安全，效率高）
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" ");
sb.append("World");
sb.insert(5, ",");      // 在索引5处插入
sb.delete(5, 6);        // 删除索引5-6之间的字符
sb.reverse();           // 反转
String result = sb.toString();

// StringBuffer（线程安全，效率较低）
StringBuffer sbf = new StringBuffer();
sbf.append("Hello").append(" World");
```

### 2.7 StringBuilder vs StringBuffer vs String

| 类 | 可变性 | 线程安全 | 效率 |
|----|--------|----------|------|
| String | 不可变 | 是 | 低（每次修改创建新对象） |
| StringBuilder | 可变 | 否 | 高 |
| StringBuffer | 可变 | 是 | 中（有同步开销） |

## 三、练习

1. 编写程序找出数组中的最大值和最小值
2. 使用 Arrays.sort() 对数组进行排序
3. 编写程序反转字符串
4. 统计字符串中每个字符出现的次数
5. 判断一个字符串是否为回文字符串