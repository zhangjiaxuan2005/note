# Day12 Java方法、枚举与包

## 一、Java 方法

### 1.1 方法概述

**方法**是语句的集合，它们在一起执行一个功能。

**方法的优点：**
- 使程序变得更简短而清晰
- 有利于程序维护
- 可以提高程序开发的效率
- 提高了代码的重用性

**方法命名规则：**
- 第一个单词小写，后面单词首字母大写（驼峰命名法）
- 例如：`addPerson`, `getUserName`

### 1.2 方法的定义

```
修饰符 返回值类型 方法名(参数类型 参数名) {
    ... 方法体 ...
    return 返回值;
}
```

**组成部分：**
- **修饰符**：可选，定义方法的访问类型
- **返回值类型**：方法可能返回的值的数据类型，`void` 表示无返回值
- **方法名**：方法的实际名称
- **参数类型**：参数像是一个占位符
- **方法体**：包含具体的语句

```java
public static int max(int num1, int num2) {
    int result;
    if (num1 > num2) {
        result = num1;
    } else {
        result = num2;
    }
    return result;
}

// 简写形式
public static int max(int num1, int num2) {
    return num1 > num2 ? num1 : num2;
}
```

### 1.3 方法调用

```java
public class TestMax {
    public static void main(String[] args) {
        int i = 5;
        int j = 2;
        int k = max(i, j);  // 调用方法
        System.out.println(i + " 和 " + j + " 比较，最大值是：" + k);
    }
    
    public static int max(int num1, int num2) {
        return num1 > num2 ? num1 : num2;
    }
}
```

### 1.4 void 方法

void 方法不返回值，调用时必须作为一条语句。

```java
public class TestVoidMethod {
    public static void main(String[] args) {
        printGrade(78.5);  // 作为语句调用
    }
    
    public static void printGrade(double score) {
        if (score >= 90.0) {
            System.out.println('A');
        } else if (score >= 80.0) {
            System.out.println('B');
        } else if (score >= 70.0) {
            System.out.println('C');
        } else if (score >= 60.0) {
            System.out.println('D');
        } else {
            System.out.println('F');
        }
    }
}
```

### 1.5 值传递

Java 中只有**值传递**，方法参数是原始值的副本。

```java
public class TestPassByValue {
    public static void main(String[] args) {
        int num1 = 1;
        int num2 = 2;
        System.out.println("交换前 num1=" + num1 + ", num2=" + num2);
        swap(num1, num2);
        System.out.println("交换后 num1=" + num1 + ", num2=" + num2);
    }
    
    public static void swap(int n1, int n2) {
        int temp = n1;
        n1 = n2;
        n2 = temp;
        System.out.println("swap方法内 n1=" + n1 + ", n2=" + n2);
    }
}
// 输出：交换后 num1和num2的值不会改变
```

### 1.6 方法重载

**方法重载**：同一个类中，方法名相同但参数列表不同。

```java
public class OverloadExample {
    // 重载方法1：两个int参数
    public static int max(int num1, int num2) {
        return num1 > num2 ? num1 : num2;
    }
    
    // 重载方法2：两个double参数
    public static double max(double num1, double num2) {
        return num1 > num2 ? num1 : num2;
    }
    
    // 重载方法3：三个int参数
    public static int max(int num1, int num2, int num3) {
        return max(max(num1, num2), num3);
    }
    
    public static void main(String[] args) {
        System.out.println(max(3, 4));        // 调用方法1
        System.out.println(max(3.5, 4.5));    // 调用方法2
        System.out.println(max(1, 2, 3));     // 调用方法3
    }
}
```

**重载规则：**
- 参数数量不同
- 参数类型不同
- 参数顺序不同
- **不能**仅通过返回类型不同来重载

### 1.7 可变参数

JDK 1.5 开始，Java 支持传递同类型的可变参数。

```java
public class VarargsDemo {
    public static void main(String[] args) {
        printMax(34, 3, 3, 2, 56.5);
        printMax(new double[]{1, 2, 3});
    }
    
    public static void printMax(double... numbers) {
        if (numbers.length == 0) {
            System.out.println("No argument passed");
            return;
        }
        double result = numbers[0];
        for (int i = 1; i < numbers.length; i++) {
            if (numbers[i] > result) {
                result = numbers[i];
            }
        }
        System.out.println("The max value is " + result);
    }
}
```

**注意：**
- 一个方法只能有一个可变参数
- 可变参数必须是方法的最后一个参数

### 1.8 变量作用域

```java
public class ScopeExample {
    // 实例变量（成员变量）
    int instanceVar = 10;
    
    // 静态变量
    static int staticVar = 20;
    
    public void method() {
        // 局部变量
        int localVar = 30;
        
        for (int i = 0; i < 10; i++) {
            // i 只在循环内有效
            int loopVar = i;
        }
        // loopVar 在这里不可用
    }
}
```

| 变量类型 | 声明位置 | 作用范围 | 生命周期 |
|----------|----------|----------|----------|
| 局部变量 | 方法内 | 方法内部 | 方法执行期间 |
| 实例变量 | 类中，方法外 | 整个类 | 对象存在期间 |
| 静态变量 | 类中，带static | 整个类 | 程序运行期间 |

---

## 二、Java 枚举(enum)

### 2.1 枚举概述

枚举是一个特殊的类，一般表示一组**常量**。

```java
// 定义枚举
enum Color {
    RED, GREEN, BLUE;
}

// 使用枚举
public class Test {
    public static void main(String[] args) {
        Color c1 = Color.RED;
        System.out.println(c1);  // RED
    }
}
```

### 2.2 枚举迭代

```java
enum Color {
    RED, GREEN, BLUE;
}

public class EnumIteration {
    public static void main(String[] args) {
        // 遍历枚举值
        for (Color color : Color.values()) {
            System.out.println(color);
        }
        
        // 获取枚举名称和序号
        Color c = Color.BLUE;
        System.out.println("名称: " + c.name());       // BLUE
        System.out.println("序号: " + c.ordinal());    // 2
    }
}
```

### 2.3 在 switch 中使用枚举

```java
enum Color {
    RED, GREEN, BLUE;
}

public class EnumSwitch {
    public static void main(String[] args) {
        Color myColor = Color.BLUE;
        
        switch(myColor) {
            case RED:
                System.out.println("红色");
                break;
            case GREEN:
                System.out.println("绿色");
                break;
            case BLUE:
                System.out.println("蓝色");
                break;
        }
    }
}
```

### 2.4 枚举的常用方法

```java
enum Color {
    RED, GREEN, BLUE;
}

public class EnumMethods {
    public static void main(String[] args) {
        // values() - 返回所有枚举值
        Color[] colors = Color.values();
        
        // ordinal() - 返回枚举常量的索引
        int index = Color.GREEN.ordinal();  // 1
        
        // valueOf() - 根据字符串获取枚举常量
        Color red = Color.valueOf("RED");
        
        // name() - 返回枚举常量名称
        String name = Color.BLUE.name();  // "BLUE"
        
        // compareTo() - 比较枚举常量的顺序
        int result = Color.RED.compareTo(Color.BLUE);  // 负数
    }
}
```

### 2.5 带构造方法和字段的枚举

```java
enum Status {
    SUCCESS(200, "成功"),
    NOT_FOUND(404, "未找到"),
    ERROR(500, "服务器错误");
    
    private int code;
    private String message;
    
    // 构造方法必须是 private
    private Status(int code, String message) {
        this.code = code;
        this.message = message;
    }
    
    public int getCode() {
        return code;
    }
    
    public String getMessage() {
        return message;
    }
}

public class EnumWithFields {
    public static void main(String[] args) {
        Status status = Status.NOT_FOUND;
        System.out.println(status.getCode());     // 404
        System.out.println(status.getMessage());  // 未找到
    }
}
```

---

## 三、Java 包(package)

### 3.1 包的作用

- 把功能相似或相关的类组织在一起
- 避免类名冲突
- 提供访问控制

### 3.2 包的声明

```java
// 包声明必须在文件的第一行
package com.example.myapp;

public class MyClass {
    // 类内容
}
```

**目录结构对应：**
```
com/
└── example/
    └── myapp/
        └── MyClass.java
```

### 3.3 导入包

```java
// 导入单个类
import java.util.ArrayList;

// 导入包中所有类
import java.util.*;

// 导入静态成员
import static java.lang.Math.*;

// 使用完全限定名（不需要import）
java.util.ArrayList<String> list = new java.util.ArrayList<>();
```

**import 语句顺序：**
```java
package com.example;           // 1. 包声明

import java.util.*;            // 2. 标准库导入
import com.otherpackage.*;     // 3. 第三方导入

public class MyClass { }       // 4. 类声明
```

### 3.4 Java 常用包

| 包名 | 说明 |
|------|------|
| java.lang | 基础类（自动导入） |
| java.util | 工具类、集合框架 |
| java.io | 输入输出流 |
| java.net | 网络编程 |
| java.sql | 数据库操作 |
| java.time | 日期时间（Java 8+） |

### 3.5 访问修饰符与包

| 修饰符 | 同类 | 同包 | 子类 | 任何地方 |
|--------|------|------|------|----------|
| public | ✓ | ✓ | ✓ | ✓ |
| protected | ✓ | ✓ | ✓ | ✗ |
| default | ✓ | ✓ | ✗ | ✗ |
| private | ✓ | ✗ | ✗ | ✗ |

```java
package com.example;

public class AccessDemo {
    public int publicVar;        // 任何地方可访问
    protected int protectedVar;  // 同包或子类
    int defaultVar;              // 同包
    private int privateVar;      // 仅同类
}
```

### 3.6 创建和使用自定义包

**步骤1：创建包结构**
```
myproject/
├── com/
│   └── mycompany/
│       ├── utils/
│       │   └── StringUtil.java
│       └── model/
│           └── User.java
└── Main.java
```

**步骤2：编写包内类**
```java
// com/mycompany/utils/StringUtil.java
package com.mycompany.utils;

public class StringUtil {
    public static boolean isEmpty(String str) {
        return str == null || str.trim().isEmpty();
    }
}
```

```java
// com/mycompany/model/User.java
package com.mycompany.model;

public class User {
    private String name;
    
    public User(String name) {
        this.name = name;
    }
    
    public String getName() {
        return name;
    }
}
```

**步骤3：编译和运行**
```bash
# 编译
javac -d . com/mycompany/utils/StringUtil.java
javac -d . com/mycompany/model/User.java

# 运行
java -cp . Main
```

---

## 四、练习题目

### 题目1：方法重载
编写一个计算器类，支持整数和浮点数的加法运算。

<details>
<summary>点击查看答案</summary>

```java
public class Calculator {
    // 整数加法
    public int add(int a, int b) {
        return a + b;
    }
    
    // 浮点数加法
    public double add(double a, double b) {
        return a + b;
    }
    
    // 三个数相加
    public int add(int a, int b, int c) {
        return a + b + c;
    }
    
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(1, 2));        // 3
        System.out.println(calc.add(1.5, 2.5));    // 4.0
        System.out.println(calc.add(1, 2, 3));     // 6
    }
}
```
</details>

### 题目2：枚举应用
定义一个表示星期的枚举，包含中文名称，并编写程序判断某天是否为工作日。

<details>
<summary>点击查看答案</summary>

```java
enum Weekday {
    MONDAY("星期一", true),
    TUESDAY("星期二", true),
    WEDNESDAY("星期三", true),
    THURSDAY("星期四", true),
    FRIDAY("星期五", true),
    SATURDAY("星期六", false),
    SUNDAY("星期日", false);
    
    private String chineseName;
    private boolean isWorkday;
    
    private Weekday(String chineseName, boolean isWorkday) {
        this.chineseName = chineseName;
        this.isWorkday = isWorkday;
    }
    
    public String getChineseName() {
        return chineseName;
    }
    
    public boolean isWorkday() {
        return isWorkday;
    }
}

public class WeekdayDemo {
    public static void main(String[] args) {
        Weekday today = Weekday.SATURDAY;
        System.out.println(today.getChineseName());
        System.out.println(today.isWorkday() ? "工作日" : "休息日");
    }
}
```
</details>

### 题目3：包的使用
创建一个工具包，包含字符串处理和数学工具类，并在主程序中使用。

<details>
<summary>点击查看答案</summary>

```java
// utils/StringUtils.java
package utils;

public class StringUtils {
    public static String reverse(String str) {
        return new StringBuilder(str).reverse().toString();
    }
    
    public static boolean isPalindrome(String str) {
        return str.equals(reverse(str));
    }
}

// utils/MathUtils.java
package utils;

public class MathUtils {
    public static int factorial(int n) {
        if (n <= 1) return 1;
        return n * factorial(n - 1);
    }
    
    public static boolean isPrime(int n) {
        if (n <= 1) return false;
        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0) return false;
        }
        return true;
    }
}

// Main.java
import utils.StringUtils;
import utils.MathUtils;

public class Main {
    public static void main(String[] args) {
        System.out.println(StringUtils.reverse("hello"));  // olleh
        System.out.println(MathUtils.factorial(5));        // 120
        System.out.println(MathUtils.isPrime(17));         // true
    }
}
```
</details>

---

## 五、总结

| 知识点 | 核心内容 |
|--------|----------|
| 方法 | 定义、调用、重载、可变参数、作用域 |
| 枚举 | 定义、迭代、switch使用、构造方法 |
| 包 | 声明、导入、访问控制、常用包 |

**重点掌握：**
1. 方法重载的规则和实际应用
2. 可变参数的定义和使用限制
3. 枚举的定义方式，特别是带字段和构造方法的枚举
4. 包的声明、导入机制以及访问修饰符的作用范围
