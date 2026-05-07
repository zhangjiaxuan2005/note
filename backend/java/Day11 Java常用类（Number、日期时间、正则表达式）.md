# Day11 Java常用类（Number、日期时间、正则表达式）

## 一、Java Number & Math 类

### 1.1 包装类概述

Java 为每一个内置数据类型提供了对应的**包装类**，所有的包装类（Integer、Long、Byte、Double、Float、Short）都是抽象类 **Number** 的子类。

| 类名 | 对应基本类型 | 描述 |
|------|-------------|------|
| Byte | byte | 字节型包装类 |
| Short | short | 短整型包装类 |
| Integer | int | 整型包装类 |
| Long | long | 长整型包装类 |
| Float | float | 单精度浮点型包装类 |
| Double | double | 双精度浮点型包装类 |
| BigInteger | - | 不可变任意精度整数 |
| BigDecimal | - | 不可变任意精度有符号十进制数 |

### 1.2 装箱与拆箱

**装箱**：将基本数据类型转换为包装类对象  
**拆箱**：将包装类对象转换为基本数据类型

```java
// 自动装箱
Integer x = 5;  // 编译器转换为 Integer.valueOf(5)

// 自动拆箱
int y = x;      // 编译器转换为 x.intValue()

// 手动装箱
Integer num = new Integer(100);

// 手动拆箱
int value = num.intValue();
```

### 1.3 Number 类常用方法

```java
Number num = 1234.56;  // 实际是Double类型

// 基本类型转换
System.out.println(num.intValue());     // 1234 (截断小数)
System.out.println(num.longValue());    // 1234
System.out.println(num.floatValue());   // 1234.56
System.out.println(num.doubleValue());  // 1234.56
```

### 1.4 Math 类

Math 类包含用于执行基本数学运算的静态方法，位于 `java.lang` 包中。

#### 常用方法

```java
// 绝对值
Math.abs(-10);        // 10

// 四舍五入
Math.round(11.5);     // 12
Math.round(-11.5);    // -11

// 向上取整
Math.ceil(1.4);       // 2.0

// 向下取整
Math.floor(1.6);      // 1.0

// 最大值和最小值
Math.max(10, 20);     // 20
Math.min(10, 20);     // 10

// 幂运算
Math.pow(2, 3);       // 8.0

// 平方根
Math.sqrt(16);        // 4.0

// 随机数 [0.0, 1.0)
Math.random();

// 生成 [1, 100] 的随机整数
int randomInt = (int)(Math.random() * 100) + 1;
```

#### 三角函数

```java
Math.sin(Math.PI / 2);    // 1.0 (90度的正弦值)
Math.cos(0);              // 1.0 (0度的余弦值)
Math.tan(Math.PI / 4);    // 1.0 (45度的正切值)
Math.toDegrees(Math.PI);  // 180.0 (弧度转角度)
Math.toRadians(180);      // π (角度转弧度)
```

#### 常量

```java
Math.PI;   // π ≈ 3.141592653589793
Math.E;    // 自然对数底数e ≈ 2.718281828459045
```

### 1.5 大数处理

```java
import java.math.BigInteger;
import java.math.BigDecimal;

// BigInteger - 任意精度整数
BigInteger bigInt = new BigInteger("12345678901234567890");
BigInteger sum = bigInt.add(new BigInteger("1"));
BigInteger product = bigInt.multiply(new BigInteger("2"));

// BigDecimal - 任意精度浮点数
BigDecimal bigDec = new BigDecimal("1234567890.1234567890");
BigDecimal result = bigDec.divide(new BigDecimal("2"), 10, RoundingMode.HALF_UP);
```

---

## 二、Java 日期时间

### 2.1 Date 类

`java.util.Date` 类表示特定的瞬间，精确到毫秒。

```java
import java.util.Date;

// 创建当前日期对象
Date now = new Date();
System.out.println(now);  // Thu Sep 17 10:20:30 CST 2025

// 获取时间戳（毫秒）
long timestamp = now.getTime();

// 根据时间戳创建日期
Date date = new Date(1609459200000L);
```

### 2.2 SimpleDateFormat 类

用于格式化和解析日期。

```java
import java.text.SimpleDateFormat;
import java.util.Date;

// 创建格式化对象
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

// 格式化日期为字符串
String strDate = sdf.format(new Date());
System.out.println("当前时间: " + strDate);  // 2025-09-17 10:20:30

// 解析字符串为日期
Date parseDate = sdf.parse("2025-01-01 00:00:00");
```

#### 日期格式化编码

| 字母 | 描述 | 示例 |
|------|------|------|
| y | 年份 | 2025 |
| M | 月份 | 09 或 September |
| d | 日期 | 17 |
| H | 小时 (0-23) | 14 |
| h | 小时 (1-12) | 02 |
| m | 分钟 | 30 |
| s | 秒 | 55 |
| S | 毫秒 | 234 |
| E | 星期几 | Thursday |
| a | AM/PM | PM |

### 2.3 Calendar 类

`Calendar` 类是一个抽象类，提供了更强大的日期操作功能。

```java
import java.util.Calendar;

// 获取当前日历对象
Calendar calendar = Calendar.getInstance();

// 获取各个字段
int year = calendar.get(Calendar.YEAR);
int month = calendar.get(Calendar.MONTH) + 1;  // 月份从0开始
int day = calendar.get(Calendar.DAY_OF_MONTH);
int hour = calendar.get(Calendar.HOUR_OF_DAY);
int minute = calendar.get(Calendar.MINUTE);
int second = calendar.get(Calendar.SECOND);

// 设置特定日期
calendar.set(2025, Calendar.JANUARY, 1);

// 日期加减
calendar.add(Calendar.DATE, 10);    // 加10天
calendar.add(Calendar.MONTH, -1);   // 减1个月

// 获取星期几
int dayOfWeek = calendar.get(Calendar.DAY_OF_WEEK);
```

### 2.4 Java 8 新日期时间 API

Java 8 引入了新的日期时间 API（`java.time` 包），设计更合理、使用更方便。

```java
import java.time.*;
import java.time.format.DateTimeFormatter;

// 当前日期
LocalDate today = LocalDate.now();
System.out.println(today);  // 2025-09-17

// 当前时间
LocalTime now = LocalTime.now();
System.out.println(now);    // 10:20:30.123

// 当前日期时间
LocalDateTime dateTime = LocalDateTime.now();

// 创建特定日期时间
LocalDate birthDate = LocalDate.of(2000, 1, 1);
LocalTime birthTime = LocalTime.of(12, 0, 0);

// 日期计算
LocalDate tomorrow = today.plusDays(1);
LocalDate lastMonth = today.minusMonths(1);

// 格式化
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
String formatted = dateTime.format(formatter);

// 解析
LocalDateTime parsed = LocalDateTime.parse("2025-01-01 12:00:00", formatter);

// 时间戳
Instant instant = Instant.now();
long epochMilli = instant.toEpochMilli();
```

### 2.5 日期比较

```java
import java.util.Date;

Date date1 = new Date();
Date date2 = new Date();

// 方法1：使用 getTime()
if (date1.getTime() > date2.getTime()) {
    System.out.println("date1 在 date2 之后");
}

// 方法2：使用 before() / after() / equals()
boolean isBefore = date1.before(date2);
boolean isAfter = date1.after(date2);
boolean isEqual = date1.equals(date2);

// 方法3：使用 compareTo()
int result = date1.compareTo(date2);  // 负数表示date1在前
```

---

## 三、Java 正则表达式

### 3.1 正则表达式概述

正则表达式定义了字符串的模式，用于搜索、编辑或处理文本。Java 通过 `java.util.regex` 包提供正则表达式支持。

### 3.2 Pattern 和 Matcher 类

```java
import java.util.regex.*;

// 编译正则表达式
Pattern pattern = Pattern.compile(".*runoob.*");

// 创建匹配器
Matcher matcher = pattern.matcher("I am noob from runoob.com.");

// 判断是否匹配
boolean isMatch = matcher.matches();
System.out.println("是否包含 'runoob': " + isMatch);

// 简写方式
boolean match = Pattern.matches(".*runoob.*", "I am noob from runoob.com.");
```

### 3.3 常用正则表达式语法

| 字符 | 说明 | 示例 |
|------|------|------|
| `.` | 匹配任意单个字符 | `a.c` 匹配 "abc", "aec" |
| `\d` | 匹配数字 [0-9] | `\d{3}` 匹配 "123" |
| `\D` | 匹配非数字 | `\D+` 匹配 "abc" |
| `\w` | 匹配单词字符 [a-zA-Z0-9_] | `\w+` 匹配 "hello" |
| `\W` | 匹配非单词字符 | `\W` 匹配 "@" |
| `\s` | 匹配空白字符 | `\s+` 匹配空格、制表符 |
| `\S` | 匹配非空白字符 | `\S+` 匹配 "hello" |
| `^` | 匹配字符串开头 | `^Hello` 匹配以Hello开头 |
| `$` | 匹配字符串结尾 | `world$` 匹配以world结尾 |
| `*` | 零次或多次 | `ab*c` 匹配 "ac", "abc", "abbc" |
| `+` | 一次或多次 | `ab+c` 匹配 "abc", "abbc" |
| `?` | 零次或一次 | `ab?c` 匹配 "ac", "abc" |
| `{n}` | 恰好 n 次 | `a{3}` 匹配 "aaa" |
| `{n,}` | 至少 n 次 | `a{2,}` 匹配 "aa", "aaa" |
| `{n,m}` | n 到 m 次 | `a{1,3}` 匹配 "a", "aa", "aaa" |
| `[]` | 字符类 | `[abc]` 匹配 "a", "b", 或 "c" |
| `[^]` | 否定字符类 | `[^abc]` 匹配非 "a", "b", "c" |
| `\|` | 或 | `cat\|dog` 匹配 "cat" 或 "dog" |
| `()` | 分组 | `(ab)+` 匹配 "ab", "abab" |

### 3.4 常用匹配示例

```java
// 验证邮箱
String emailRegex = "^[\\w.-]+@[\\w.-]+\\.[a-zA-Z]{2,}$";
boolean isEmail = Pattern.matches(emailRegex, "test@example.com");

// 验证手机号（中国大陆）
String phoneRegex = "^1[3-9]\\d{9}$";
boolean isPhone = Pattern.matches(phoneRegex, "13800138000");

// 验证身份证号
String idCardRegex = "^\\d{15}$|^\\d{18}$|^\\d{17}[Xx]$";

// 匹配IP地址
String ipRegex = "^((25[0-5]|2[0-4]\\d|[01]?\\d\\d?)\\.){3}(25[0-5]|2[0-4]\\d|[01]?\\d\\d?)$";
```

### 3.5 Matcher 类方法

```java
import java.util.regex.*;

String text = "The cat sat on the mat with the cats.";
Pattern pattern = Pattern.compile("cat");
Matcher matcher = pattern.matcher(text);

// find() - 查找下一个匹配
while (matcher.find()) {
    System.out.println("找到匹配: " + matcher.group());
    System.out.println("起始位置: " + matcher.start());
    System.out.println("结束位置: " + matcher.end());
}

// 替换
String result1 = matcher.replaceAll("dog");     // 替换所有
String result2 = matcher.replaceFirst("dog");   // 替换第一个

// 分组捕获
Pattern p = Pattern.compile("(\\d{4})-(\\d{2})-(\\d{2})");
Matcher m = p.matcher("2025-09-17");
if (m.find()) {
    System.out.println("年: " + m.group(1));  // 2025
    System.out.println("月: " + m.group(2));  // 09
    System.out.println("日: " + m.group(3));  // 17
}
```

### 3.6 正则表达式分割字符串

```java
String str = "apple,banana,orange";
String[] fruits = str.split(",");

String text = "a  b   c";
String[] parts = text.split("\\s+");  // 按一个或多个空白字符分割
```

---

## 四、练习题目

### 题目1：Math 类练习
编写程序计算圆的面积和周长，半径为 5.5。

<details>
<summary>点击查看答案</summary>

```java
public class CircleMath {
    public static void main(String[] args) {
        double radius = 5.5;
        double area = Math.PI * Math.pow(radius, 2);
        double circumference = 2 * Math.PI * radius;
        
        System.out.printf("半径: %.2f%n", radius);
        System.out.printf("面积: %.2f%n", area);
        System.out.printf("周长: %.2f%n", circumference);
    }
}
```
</details>

### 题目2：日期格式化
将当前日期格式化为 "2025年09月17日 星期四" 的形式。

<details>
<summary>点击查看答案</summary>

```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Locale;

public class DateFormatExercise {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter
            .ofPattern("yyyy年MM月dd日 EEEE", Locale.CHINESE);
        String formatted = now.format(formatter);
        System.out.println(formatted);
    }
}
```
</details>

### 题目3：正则表达式验证
编写程序验证用户输入的密码是否满足：至少8位，包含大小写字母和数字。

<details>
<summary>点击查看答案</summary>

```java
import java.util.regex.*;

public class PasswordValidator {
    public static void main(String[] args) {
        String password = "Hello123";
        // 至少8位，包含大写、小写和数字
        String regex = "^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d).{8,}$";
        
        boolean isValid = Pattern.matches(regex, password);
        System.out.println("密码是否有效: " + isValid);
    }
}
```
</details>

---

## 五、总结

| 知识点 | 核心内容 |
|--------|----------|
| Number & Math | 包装类、装箱拆箱、Math工具方法 |
| 日期时间 | Date、SimpleDateFormat、Calendar、Java 8新API |
| 正则表达式 | Pattern、Matcher、常用语法规则 |

**重点掌握：**
1. 自动装箱拆箱的原理
2. Math 类的常用数学计算方法
3. SimpleDateFormat 的格式化模式
4. 正则表达式的基本语法和 Pattern/Matcher 的使用
