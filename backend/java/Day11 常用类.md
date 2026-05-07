# Day11 常用类

## 一、Java Number 类

一般情况下，当需要使用数字的时候，我们通常使用内置数据类型，如：byte、int、long、double 等。

然而，在实际开发过程中，我们经常会遇到需要使用对象，而不是内置数据类型的情形。为了解决这个问题，Java 语言为每一个内置数据类型提供了对应的包装类。

所有的包装类（Integer、Long、Byte、Double、Float、Short）都是抽象类 Number 的子类。

| 包装类 | 基本数据类型 |
|--------|--------------|
| Boolean | boolean |
| Byte | byte |
| Short | short |
| Integer | int |
| Long | long |
| Character | char |
| Float | float |
| Double | double |

### 1.1 装箱与拆箱

**装箱：** 将基本数据类型转换为包装类对象
**拆箱：** 将包装类对象转换为基本数据类型

```java
public class Test {
    public static void main(String[] args) {
        // 装箱：基本数据类型 -> 包装类
        Integer x = 5;  // 自动装箱
        Integer y = Integer.valueOf(5);  // 手动装箱
        
        // 拆箱：包装类 -> 基本数据类型
        int a = x;  // 自动拆箱
        int b = x.intValue();  // 手动拆箱
        
        System.out.println(x);  // 5
        System.out.println(a);  // 5
    }
}
```

### 1.2 Number 方法

| 方法 | 描述 |
|------|------|
| `xxxValue()` | 将 Number 对象转换为 xxx 数据类型的值并返回 |
| `compareTo()` | 将 Number 对象与参数比较 |
| `equals()` | 判断 Number 对象是否与参数相等 |
| `valueOf()` | 返回一个 Number 对象指定的内置数据类型 |
| `toString()` | 以字符串形式返回值 |
| `parseInt()` | 将字符串解析为 int 类型 |
| `abs()` | 返回参数的绝对值 |
| `ceil()` | 返回大于等于参数的最小整数 |
| `floor()` | 返回小于等于参数的最大整数 |
| `round()` | 返回最接近参数的 long 或 int 类型 |
| `max()` | 返回两个参数中的最大值 |
| `min()` | 返回两个参数中的最小值 |
| `random()` | 返回一个随机数 |

### 1.3 Math 类

Math 类包含了用于执行基本数学运算的属性和方法，如初等指数、对数、平方根和三角函数。

```java
public class Test {
    public static void main(String[] args) {
        System.out.println("90度的正弦值：" + Math.sin(Math.PI/2));
        System.out.println("0度的余弦值：" + Math.cos(0));
        System.out.println("60度的正切值：" + Math.tan(Math.PI/3));
        System.out.println("1的反正切值：" + Math.atan(1));
        System.out.println("π/2的角度值：" + Math.toDegrees(Math.PI/2));
        System.out.println("随机数：" + Math.random());
    }
}
```

---

## 二、Java 日期时间

java.util 包提供了 Date 类来封装当前的日期和时间。Date 类提供两个构造函数来实例化 Date 对象。

### 2.1 Date 类

```java
import java.util.Date;

public class DateDemo {
    public static void main(String[] args) {
        // 初始化 Date 对象
        Date date = new Date();
        
        // 使用 toString() 函数显示日期时间
        System.out.println(date.toString());
    }
}
```

输出结果：

```
Mon May 04 09:51:52 CDT 2025
```

### 2.2 日期比较

- 使用 `getTime()` 方法获取两个日期（自1970年1月1日经历的毫秒数值），然后比较这两个值
- 使用方法 `before()`、`after()` 和 `equals()` 进行比较
- 使用 `compareTo()` 方法进行比较

### 2.3 SimpleDateFormat 格式化日期

SimpleDateFormat 是一个以语言环境敏感的方式来格式化和分析日期的类。

```java
import java.util.Date;
import java.text.SimpleDateFormat;

public class DateDemo {
    public static void main(String[] args) {
        Date dNow = new Date();
        SimpleDateFormat ft = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
        
        System.out.println("当前时间为: " + ft.format(dNow));
    }
}
```

输出结果：

```
当前时间为: 2025-05-04 10:12:34
```

**日期和时间模式：**

| 字母 | 描述 | 示例 |
|------|------|------|
| G | 纪元标记 | AD |
| y | 四位年份 | 2025 |
| M | 月份 | July or 07 |
| d | 一个月的日期 | 10 |
| h | A.M./P.M. (1~12)格式小时 | 12 |
| H | 一天中的小时 (0~23) | 22 |
| m | 分钟数 | 30 |
| s | 秒数 | 55 |
| S | 毫秒数 | 234 |
| E | 星期几 | Tuesday |
| D | 一年中的日子 | 360 |
| F | 一个月中第几周的周几 | 2 (second Wed. in July) |
| w | 一年中第几周 | 40 |
| W | 一个月中第几周 | 1 |
| a | A.M./P.M. 标记 | PM |
| k | 一天中的小时(1~24) | 24 |
| K | A.M./P.M. (0~11)格式小时 | 10 |
| z | 时区 | Eastern Standard Time |

### 2.4 Calendar 类

Calendar 类是一个抽象类，在实际使用时实现特定的子类的对象。

```java
import java.util.Calendar;

public class CalendarDemo {
    public static void main(String[] args) {
        Calendar c = Calendar.getInstance();
        
        System.out.println("年: " + c.get(Calendar.YEAR));
        System.out.println("月: " + (c.get(Calendar.MONTH) + 1));
        System.out.println("日: " + c.get(Calendar.DATE));
        System.out.println("时: " + c.get(Calendar.HOUR_OF_DAY));
        System.out.println("分: " + c.get(Calendar.MINUTE));
        System.out.println("秒: " + c.get(Calendar.SECOND));
    }
}
```

### 2.5 Java 8 日期时间 API

Java 8 引入了新的日期时间 API，位于 java.time 包中。

```java
import java.time.LocalDate;
import java.time.LocalTime;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class Java8DateTime {
    public static void main(String[] args) {
        // 获取当前日期
        LocalDate date = LocalDate.now();
        System.out.println("当前日期: " + date);
        
        // 获取当前时间
        LocalTime time = LocalTime.now();
        System.out.println("当前时间: " + time);
        
        // 获取当前日期时间
        LocalDateTime dateTime = LocalDateTime.now();
        System.out.println("当前日期时间: " + dateTime);
        
        // 格式化
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        String formatted = dateTime.format(formatter);
        System.out.println("格式化后: " + formatted);
    }
}
```

---

## 三、Java 正则表达式

正则表达式定义了字符串的模式，可以用来搜索、编辑或处理文本。

### 3.1 正则表达式语法

| 子表达式 | 匹配内容 |
|----------|----------|
| ^ | 匹配行的开头 |
| $ | 匹配行的结尾 |
| . | 匹配除换行符外的任何单个字符 |
| [...] | 匹配括号中的任何一个字符 |
| [^...] | 匹配不在括号中的任何一个字符 |
| \\A | 匹配字符串的开头 |
| \\z | 匹配字符串的结尾 |
| \\Z | 匹配字符串的结尾，仅允许最后的换行符 |
| re* | 匹配 0 个或多个的表达式 |
| re+ | 匹配 1 个或多个的表达式 |
| re? | 匹配 0 个或 1 个由前面的正则表达式定义的片段 |
| re{ n} | 精确匹配 n 个前面表达式 |
| re{ n,} | 匹配 n 个或多个前面表达式 |
| re{ n, m} | 匹配至少 n 个、至多 m 个前面表达式 |
| a\|b | 匹配 a 或 b |
| (re) | 对正则表达式分组并记住匹配的文本 |
| \\w | 匹配字母数字及下划线 |
| \\W | 匹配非字母数字及下划线 |
| \\s | 匹配任意空白字符 |
| \\S | 匹配任意非空白字符 |
| \\d | 匹配任意数字 |
| \\D | 匹配任意非数字 |

### 3.2 Pattern 和 Matcher 类

java.util.regex 包主要包括以下两个类：

- **Pattern 类：** 正则表达式的编译表示
- **Matcher 类：** 对输入字符串进行解释和匹配操作

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class RegexMatches {
    public static void main(String[] args) {
        // 要验证的字符串
        String str = "runoob";
        // 正则表达式规则
        String pattern = "^run.*";
        
        // 创建 Pattern 对象
        Pattern r = Pattern.compile(pattern);
        
        // 创建 matcher 对象
        Matcher m = r.matcher(str);
        
        if (m.find()) {
            System.out.println("匹配成功");
        } else {
            System.out.println("匹配失败");
        }
    }
}
```

### 3.3 常用正则表达式示例

```java
import java.util.regex.Pattern;

public class RegexExamples {
    public static void main(String[] args) {
        // 验证邮箱
        String email = "test@runoob.com";
        String emailPattern = "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$";
        System.out.println("邮箱验证: " + Pattern.matches(emailPattern, email));
        
        // 验证手机号（中国大陆）
        String phone = "13800138000";
        String phonePattern = "^1[3-9]\\d{9}$";
        System.out.println("手机号验证: " + Pattern.matches(phonePattern, phone));
        
        // 验证身份证号码
        String idCard = "110101199001011234";
        String idPattern = "^\\d{17}[\\dXx]$";
        System.out.println("身份证验证: " + Pattern.matches(idPattern, idCard));
    }
}
```

---

## 四、练习

1. 使用 Math 类计算圆的面积和周长
2. 使用 SimpleDateFormat 格式化当前日期时间为 "yyyy年MM月dd日 HH时mm分ss秒" 格式
3. 使用 Calendar 类计算两个日期之间相差的天数
4. 使用正则表达式验证用户名（只能包含字母、数字、下划线，长度6-20位）
5. 使用 Java 8 日期时间 API 计算某日期加上 100 天后的日期