# Day2 数据类型与运算符

## 一、Java数据类型分类

### 1.1 基本数据类型（8种）

| 类型 | 关键字 | 占用字节 | 取值范围 | 默认值 |
|------|--------|----------|----------|--------|
| 字节型 | byte | 1 | -128 ~ 127 | 0 |
| 短整型 | short | 2 | -32768 ~ 32767 | 0 |
| 整型 | int | 4 | -2^31 ~ 2^31-1 | 0 |
| 长整型 | long | 8 | -2^63 ~ 2^63-1 | 0L |
| 单精度浮点 | float | 4 | 约 ±3.4×10^38 | 0.0f |
| 双精度浮点 | double | 8 | 约 ±1.7×10^308 | 0.0d |
| 字符型 | char | 2 | '\u0000' ~ '\uffff' | '\u0000' |
| 布尔型 | boolean | 1 | true / false | false |

### 1.2 引用数据类型
- 类（class）
- 接口（interface）
- 数组（array）
- 字符串（String）

### 1.3 常量声明
```java
final int MAX_AGE = 100;
final double PI = 3.1415926;
```

## 二、变量声明与初始化

### 2.1 变量声明语法
```java
// 声明变量
int age;
String name;

// 声明并初始化
int score = 90;
double height = 1.75;
boolean isStudent = true;
char gender = '男';
long population = 1400000000L;
float price = 9.9f;
```

### 2.2 变量命名规范
- 遵循小驼峰命名法：`studentName`, `totalScore`
- 见名知意，避免使用单个字母（循环变量除外）

## 三、数据类型转换

### 3.1 自动类型转换（隐式转换）
- 容量小的类型自动转换为容量大的类型
- 转换顺序：byte → short → int → long → float → double

```java
int num = 10;
double result = num; // int → double，自动转换
```

### 3.2 强制类型转换（显式转换）
- 需要使用强制转换符 `(类型)`
- 可能会导致精度损失或溢出

```java
double pi = 3.14159;
int approx = (int) pi; // approx = 3，小数部分被舍弃

long bigNum = 10000000000L;
int smallNum = (int) bigNum; // 可能溢出
```

## 四、运算符

### 4.1 算术运算符
```java
int a = 10, b = 3;
int add = a + b;      // 13
int sub = a - b;      // 7
int mul = a * b;      // 30
int div = a / b;      // 3（整数除法取整）
int mod = a % b;      // 1（取模）
```

### 4.2 赋值运算符
```java
int x = 5;
x += 3;  // x = x + 3，结果为 8
x -= 2;  // x = x - 2，结果为 6
x *= 2;  // x = x * 2，结果为 12
x /= 3;  // x = x / 3，结果为 4
x %= 2;  // x = x % 2，结果为 0
```

### 4.3 比较运算符
```java
int a = 5, b = 3;
boolean eq = (a == b);  // false
boolean neq = (a != b); // true
boolean gt = (a > b);   // true
boolean lt = (a < b);   // false
boolean ge = (a >= b);  // true
boolean le = (a <= b);  // false
```

### 4.4 逻辑运算符
```java
boolean condition1 = true;
boolean condition2 = false;

boolean and = condition1 && condition2;  // false（短路与）
boolean or = condition1 || condition2;   // true（短路或）
boolean not = !condition1;               // false（非）
```

### 4.5 位运算符
```java
int a = 60;  // 0011 1100
int b = 13;  // 0000 1101

int and = a & b;   // 0000 1100 = 12
int or = a | b;    // 0011 1101 = 61
int xor = a ^ b;   // 0011 0001 = 49
int not = ~a;      // 1100 0011（补码表示）
int left = a << 2; // 1111 0000 = 240
int right = a >> 2;// 0000 1111 = 15
```

### 4.6 自增自减运算符
```java
int i = 5;
int j = i++;  // j = 5, i = 6（后增）
int k = ++i;  // k = 7, i = 7（前增）

int m = 5;
int n = m--;  // n = 5, m = 4（后减）
int p = --m;  // p = 3, m = 3（前减）
```

### 4.7 运算符优先级（从高到低）
1. 括号 `()`
2. 一元运算符 `++`、`--`、`!`、`~`
3. 算术运算符 `*`、`/`、`%`
4. 算术运算符 `+`、`-`
5. 位运算符 `<<`、`>>`、`>>>`
6. 比较运算符 `<`、`>`、`<=`、`>=`、`instanceof`
7. 比较运算符 `==`、`!=`
8. 位运算符 `&`
9. 位运算符 `^`
10. 位运算符 `|`
11. 逻辑运算符 `&&`
12. 逻辑运算符 `||`
13. 三元运算符 `? :`
14. 赋值运算符 `=`、`+=`、`-=` 等

## 五、练习

1. 声明各种类型的变量并赋值
2. 练习类型转换（自动和强制）
3. 编写程序计算两个数的加、减、乘、除、取模
4. 使用逻辑运算符组合多个条件