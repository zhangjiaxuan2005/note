# Day3 流程控制语句

## 一、条件判断语句

### 1.1 if 语句
```java
int score = 85;

if (score >= 60) {
    System.out.println("及格");
}
```

### 1.2 if-else 语句
```java
int score = 85;

if (score >= 60) {
    System.out.println("及格");
} else {
    System.out.println("不及格");
}
```

### 1.3 if-else if-else 语句
```java
int score = 85;

if (score >= 90) {
    System.out.println("优秀");
} else if (score >= 80) {
    System.out.println("良好");
} else if (score >= 60) {
    System.out.println("及格");
} else {
    System.out.println("不及格");
}
```

### 1.4 嵌套 if 语句
```java
int age = 25;
boolean isStudent = true;

if (age >= 18) {
    if (isStudent) {
        System.out.println("成年学生");
    } else {
        System.out.println("成年非学生");
    }
} else {
    System.out.println("未成年");
}
```

## 二、switch 语句

### 2.1 基本用法
```java
int dayOfWeek = 3;

switch (dayOfWeek) {
    case 1:
        System.out.println("星期一");
        break;
    case 2:
        System.out.println("星期二");
        break;
    case 3:
        System.out.println("星期三");
        break;
    case 4:
        System.out.println("星期四");
        break;
    case 5:
        System.out.println("星期五");
        break;
    case 6:
        System.out.println("星期六");
        break;
    case 7:
        System.out.println("星期日");
        break;
    default:
        System.out.println("无效的日期");
}
```

### 2.2 switch 支持的类型
- byte, short, int, char（Java 7+ 支持 String）
- 枚举类型

### 2.3 switch 表达式（Java 12+）
```java
int dayOfWeek = 3;
String dayName = switch (dayOfWeek) {
    case 1 -> "星期一";
    case 2 -> "星期二";
    case 3 -> "星期三";
    default -> "未知";
};
System.out.println(dayName);
```

## 三、循环语句

### 3.1 for 循环
```java
// 基本 for 循环
for (int i = 0; i < 5; i++) {
    System.out.println("循环次数: " + i);
}

// 增强 for 循环（foreach）
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}
```

### 3.2 while 循环
```java
int i = 0;
while (i < 5) {
    System.out.println("循环次数: " + i);
    i++;
}
```

### 3.3 do-while 循环
```java
int i = 0;
do {
    System.out.println("循环次数: " + i);
    i++;
} while (i < 5);
```

### 3.4 循环对比
| 循环类型 | 特点 | 使用场景 |
|----------|------|----------|
| for | 适合已知循环次数 | 遍历数组、固定次数迭代 |
| while | 先判断后执行 | 不确定循环次数 |
| do-while | 先执行后判断 | 至少执行一次的场景 |

## 四、跳转语句

### 4.1 break 语句
```java
// 跳出单层循环
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break; // 跳出循环
    }
    System.out.println(i);
}

// 跳出多层循环（带标签）
outer: for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 3; j++) {
        if (i + j == 3) {
            break outer; // 跳出外层循环
        }
        System.out.println("i=" + i + ", j=" + j);
    }
}
```

### 4.2 continue 语句
```java
// 跳过当前迭代，继续下一次
for (int i = 0; i < 10; i++) {
    if (i % 2 == 0) {
        continue; // 跳过偶数
    }
    System.out.println(i); // 只输出奇数
}
```

### 4.3 return 语句
```java
public static int add(int a, int b) {
    return a + b; // 返回结果，结束方法
}

public static void checkAge(int age) {
    if (age < 18) {
        System.out.println("未成年");
        return; // 结束方法
    }
    System.out.println("成年");
}
```

## 五、练习

1. 编写程序判断一个年份是否为闰年
2. 使用 switch 语句实现简单的计算器（加减乘除）
3. 使用 for 循环输出 1 到 100 的所有偶数
4. 使用 while 循环计算 1 到 100 的累加和
5. 使用嵌套循环打印九九乘法表