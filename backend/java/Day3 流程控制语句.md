# Java 流程控制语句

## 一、条件判断语句

### 1.1 if 语句

一个 `if` 语句包含一个布尔表达式和一条或多条语句。

**语法：**

```java
if(布尔表达式) {
    // 如果布尔表达式为 true 将执行的语句
}
```

**实例：**

```java
public class Test {
    public static void main(String args[]) {
        int x = 10;
        
        if (x < 20) {
            System.out.print("这是 if 语句");
        }
    }
}
```

运行结果：

```
这是 if 语句
```

### 1.2 if...else 语句

`if` 语句后面可以跟 `else` 语句，当 `if` 语句的布尔表达式值为 `false` 时，`else` 语句块会被执行。

**语法：**

```java
if(布尔表达式) {
    // 如果布尔表达式的值为 true 执行代码
} else {
    // 如果布尔表达式的值为 false 执行代码
}
```

**实例：**

```java
public class Test {
    public static void main(String args[]) {
        int x = 30;
        
        if (x < 20) {
            System.out.print("这是 if 语句");
        } else {
            System.out.print("这是 else 语句");
        }
    }
}
```

运行结果：

```
这是 else 语句
```

### 1.3 if...else if...else 语句

`if` 语句后面可以跟 `else if...else` 语句，这种语句可以检测到多种可能的情况。

**使用规则：**
- `if` 语句至多有 1 个 `else` 语句，`else` 语句在所有的 `else if` 语句之后
- `if` 语句可以有若干个 `else if` 语句，它们必须在 `else` 语句之前
- 一旦其中一个 `else if` 语句检测为 `true`，其他的 `else if` 以及 `else` 语句都将跳过执行

**语法：**

```java
if(布尔表达式 1) {
    // 如果布尔表达式 1 的值为 true 执行代码
} else if(布尔表达式 2) {
    // 如果布尔表达式 2 的值为 true 执行代码
} else if(布尔表达式 3) {
    // 如果布尔表达式 3 的值为 true 执行代码
} else {
    // 如果以上布尔表达式都不为 true 执行代码
}
```

**实例：**

```java
public class Test {
    public static void main(String args[]) {
        int x = 30;
        
        if (x == 10) {
            System.out.print("Value of X is 10");
        } else if (x == 20) {
            System.out.print("Value of X is 20");
        } else if (x == 30) {
            System.out.print("Value of X is 30");
        } else {
            System.out.print("这是 else 语句");
        }
    }
}
```

运行结果：

```
Value of X is 30
```

### 1.4 嵌套的 if...else 语句

使用嵌套的 `if...else` 语句是合法的。也就是说你可以在另一个 `if` 或者 `else if` 语句中使用 `if` 或者 `else if` 语句。

**语法：**

```java
if(布尔表达式 1) {
    // 如果布尔表达式 1 的值为 true 执行代码
    if(布尔表达式 2) {
        // 如果布尔表达式 2 的值为 true 执行代码
    }
}
```

**实例：**

```java
public class Test {
    public static void main(String args[]) {
        int x = 30;
        int y = 10;
        
        if (x == 30) {
            if (y == 10) {
                System.out.print("X = 30 and Y = 10");
            }
        }
    }
}
```

运行结果：

```
X = 30 and Y = 10
```

---

## 二、switch case 语句

`switch case` 语句判断一个变量与一系列值中某个值是否相等，每个值称为一个分支。

### 2.1 语法

```java
switch(expression) {
    case value :
        // 语句
        break;  // 可选
    case value :
        // 语句
        break;  // 可选
    // 可以有任意数量的 case 语句
    default :   // 可选
        // 语句
}
```

### 2.2 switch case 语句规则

- `switch` 语句中的变量类型可以是：`byte`、`short`、`int` 或者 `char`
- 从 Java SE 7 开始，`switch` 支持字符串 `String` 类型，同时 `case` 标签必须为字符串常量或字面量
- `switch` 语句可以拥有多个 `case` 语句。每个 `case` 后面跟一个要比较的值和冒号
- `case` 语句中的值的数据类型必须与变量的数据类型相同，而且只能是常量或者字面常量
- 当变量的值与 `case` 语句的值相等时，那么 `case` 语句之后的语句开始执行，直到 `break` 语句出现才会跳出 `switch` 语句
- 当遇到 `break` 语句时，`switch` 语句终止。程序跳转到 `switch` 语句后面的语句执行
- `case` 语句不必须要包含 `break` 语句。如果没有 `break` 语句出现，程序会继续执行下一条 `case` 语句，直到出现 `break` 语句
- `switch` 语句可以包含一个 `default` 分支，该分支一般是 `switch` 语句的最后一个分支（可以在任何位置，但建议在最后一个）
- `default` 在没有 `case` 语句的值和变量值相等的时候执行。`default` 分支不需要 `break` 语句

### 2.3 实例

**实例 1：基本用法**

```java
public class Test {
    public static void main(String args[]) {
        char grade = 'C';
        
        switch(grade) {
            case 'A' :
                System.out.println("优秀");
                break;
            case 'B' :
            case 'C' :
                System.out.println("良好");
                break;
            case 'D' :
                System.out.println("及格");
                break;
            case 'F' :
                System.out.println("你需要再努力努力");
                break;
            default :
                System.out.println("未知等级");
        }
        System.out.println("你的等级是 " + grade);
    }
}
```

运行结果：

```
良好
你的等级是 C
```

**实例 2：没有 break 语句的情况**

```java
public class Test {
    public static void main(String args[]) {
        int i = 1;
        
        switch(i) {
            case 0:
                System.out.println("0");
            case 1:
                System.out.println("1");
            case 2:
                System.out.println("2");
            default:
                System.out.println("default");
        }
    }
}
```

运行结果：

```
1
2
default
```

**实例 3：匹配不成功返回 default**

```java
public class Test {
    public static void main(String args[]) {
        int i = 5;
        
        switch(i) {
            case 0:
                System.out.println("0");
            case 1:
                System.out.println("1");
            case 2:
                System.out.println("2");
            default:
                System.out.println("default");
        }
    }
}
```

运行结果：

```
default
```

**实例 4：后续 case 有 break 语句**

```java
public class Test {
    public static void main(String args[]) {
        int i = 1;
        
        switch(i) {
            case 0:
                System.out.println("0");
            case 1:
                System.out.println("1");
            case 2:
                System.out.println("2");
            case 3:
                System.out.println("3");
                break;
            default:
                System.out.println("default");
        }
    }
}
```

运行结果：

```
1
2
3
```

**实例 5：Java 7+ 支持 String 类型**

```java
public class Test {
    public static void main(String args[]) {
        String day = "Monday";
        
        switch(day) {
            case "Monday":
                System.out.println("星期一");
                break;
            case "Tuesday":
                System.out.println("星期二");
                break;
            case "Wednesday":
                System.out.println("星期三");
                break;
            default:
                System.out.println("未知日期");
        }
    }
}
```

运行结果：

```
星期一
```

---

## 三、循环结构

顺序结构的程序语句只能被执行一次。如果想要同样的操作执行多次，就需要使用循环结构。

Java 中有三种主要的循环结构：

- `while` 循环
- `do...while` 循环
- `for` 循环

在 Java 5 中引入了一种主要用于数组的增强型 for 循环。

### 3.1 while 循环

`while` 是最基本的循环，只要布尔表达式为 `true`，循环就会一直执行下去。

**语法：**

```java
while(布尔表达式) {
    // 循环内容
}
```

**实例：**

```java
public class Test {
    public static void main(String[] args) {
        int x = 10;
        
        while (x < 20) {
            System.out.print("value of x : " + x);
            x++;
            System.out.print("\n");
        }
    }
}
```

运行结果：

```
value of x : 10
value of x : 11
value of x : 12
value of x : 13
value of x : 14
value of x : 15
value of x : 16
value of x : 17
value of x : 18
value of x : 19
```

### 3.2 do...while 循环

对于 `while` 语句而言，如果不满足条件，则不能进入循环。但有时候我们需要即使不满足条件，也至少执行一次。

`do...while` 循环和 `while` 循环相似，不同的是，`do...while` 循环至少会执行一次。

**语法：**

```java
do {
    // 代码语句
} while(布尔表达式);
```

**注意：** 布尔表达式在循环体的后面，所以语句块在检测布尔表达式之前已经执行了。如果布尔表达式的值为 `true`，则语句块一直执行，直到布尔表达式的值为 `false`。

**实例：**

```java
public class Test {
    public static void main(String[] args) {
        int x = 10;
        
        do {
            System.out.print("value of x : " + x);
            x++;
            System.out.print("\n");
        } while (x < 20);
    }
}
```

运行结果：

```
value of x : 10
value of x : 11
value of x : 12
value of x : 13
value of x : 14
value of x : 15
value of x : 16
value of x : 17
value of x : 18
value of x : 19
```

**对比：while 和 do...while 的区别**

```java
public class Test {
    public static void main(String[] args) {
        int a = 100;
        
        System.out.println("=== while 循环 ===");
        while (a < 10) {
            System.out.println("value of a : " + a);
            a++;
        }
        
        int b = 100;
        System.out.println("\n=== do...while 循环 ===");
        do {
            System.out.println("value of b : " + b);
            b++;
        } while (b < 10);
    }
}
```

运行结果：

```
=== while 循环 ===

=== do...while 循环 ===
value of b : 100
```

### 3.3 for 循环

虽然所有循环结构都可以用 `while` 或者 `do...while` 表示，但 Java 提供了另一种语句 —— `for` 循环，使一些循环结构变得更加简单。

`for` 循环执行的次数是在执行前就确定的。

**语法：**

```java
for(初始化; 布尔表达式; 更新) {
    // 代码语句
}
```

**执行过程：**
1. 最先执行初始化步骤。可以声明一种类型，但可初始化一个或多个循环控制变量，也可以是空语句
2. 然后，检测布尔表达式的值。如果为 `true`，循环体被执行。如果为 `false`，循环终止，开始执行循环体后面的语句
3. 执行一次循环后，更新循环控制变量
4. 再次检测布尔表达式。循环执行上面的过程

**实例：**

```java
public class Test {
    public static void main(String[] args) {
        for(int x = 10; x < 20; x = x + 1) {
            System.out.print("value of x : " + x);
            System.out.print("\n");
        }
    }
}
```

运行结果：

```
value of x : 10
value of x : 11
value of x : 12
value of x : 13
value of x : 14
value of x : 15
value of x : 16
value of x : 17
value of x : 18
value of x : 19
```

### 3.4 Java 增强 for 循环

Java 5 引入了一种主要用于数组的增强型 for 循环。

**语法：**

```java
for(声明语句 : 表达式) {
    // 代码语句
}
```

**声明语句：** 声明新的局部变量，该变量的类型必须和数组元素的类型匹配。其作用域限定在循环语句块，其值与此时数组元素的值相等。

**表达式：** 表达式是要访问的数组名，或者是返回值为数组的方法。

**实例：**

```java
public class Test {
    public static void main(String[] args) {
        int [] numbers = {10, 20, 30, 40, 50};
        
        for(int x : numbers ) {
            System.out.print(x);
            System.out.print(",");
        }
        
        System.out.print("\n");
        
        String [] names = {"James", "Larry", "Tom", "Lacy"};
        for( String name : names ) {
            System.out.print(name);
            System.out.print(",");
        }
    }
}
```

运行结果：

```
10,20,30,40,50,
James,Larry,Tom,Lacy,
```

### 3.5 循环对比

| 循环类型 | 特点 | 使用场景 |
|----------|------|----------|
| `for` | 适合已知循环次数 | 遍历数组、固定次数迭代 |
| `while` | 先判断后执行 | 不确定循环次数 |
| `do...while` | 先执行后判断 | 至少执行一次的场景 |

---

## 四、跳转语句

### 4.1 break 关键字

`break` 主要用在循环语句或者 `switch` 语句中，用来跳出整个语句块。

`break` 跳出最里层的循环，并且继续执行该循环下面的语句。

**语法：**

```java
break;
```

**实例 1：跳出循环**

```java
public class Test {
    public static void main(String[] args) {
        int [] numbers = {10, 20, 30, 40, 50};
        
        for(int x : numbers ) {
            if( x == 30 ) {
                break;
            }
            System.out.print(x);
            System.out.print("\n");
        }
    }
}
```

运行结果：

```
10
20
```

**实例 2：跳出多层循环（带标签）**

```java
public class Test {
    public static void main(String[] args) {
        outer: for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (i + j == 3) {
                    break outer; // 跳出外层循环
                }
                System.out.println("i = " + i + ", j = " + j);
            }
        }
    }
}
```

运行结果：

```
i = 0, j = 0
i = 0, j = 1
i = 0, j = 2
i = 1, j = 0
i = 1, j = 1
```

### 4.2 continue 关键字

`continue` 适用于任何循环控制结构中。作用是让程序立刻跳转到下一次循环的迭代。

在 `for` 循环中，`continue` 语句使程序立即跳转到更新语句。

在 `while` 或者 `do...while` 循环中，程序立即跳转到布尔表达式的判断语句。

**语法：**

```java
continue;
```

**实例：**

```java
public class Test {
    public static void main(String[] args) {
        int [] numbers = {10, 20, 30, 40, 50};
        
        for(int x : numbers ) {
            if( x == 30 ) {
                continue;
            }
            System.out.print(x);
            System.out.print("\n");
        }
    }
}
```

运行结果：

```
10
20
40
50
```

**实例：跳过偶数**

```java
public class Test {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            if (i % 2 == 0) {
                continue; // 跳过偶数
            }
            System.out.println(i); // 只输出奇数
        }
    }
}
```

运行结果：

```
1
3
5
7
9
```

### 4.3 return 关键字

`return` 语句用于退出方法，返回一个值给调用者。

**语法：**

```java
return value;  // 返回值
return;        // 无返回值（用于 void 方法）
```

**实例：**

```java
public class Test {
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
    
    public static void main(String[] args) {
        int sum = add(3, 5);
        System.out.println("3 + 5 = " + sum);
        
        checkAge(20);
        checkAge(15);
    }
}
```

运行结果：

```
3 + 5 = 8
成年
未成年
```

---

## 五、练习

1. 编写程序判断一个年份是否为闰年
2. 使用 `switch` 语句实现简单的计算器（加减乘除）
3. 使用 `for` 循环输出 1 到 100 的所有偶数
4. 使用 `while` 循环计算 1 到 100 的累加和
5. 使用嵌套循环打印九九乘法表
6. 输出 200 以内能被 7 整除但是不能被 4 整除的数字，并且每行输出 6 个
7. 使用 `for` 和 `if` 绘制一个空心的菱形
