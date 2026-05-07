# Java 数据类型与运算符

## 一、Java 数据类型

Java 中的数据类型分为两大类：**内置数据类型**和**引用数据类型**。

变量就是申请内存来存储值。也就是说，当创建变量的时候，需要在内存中申请空间。

内存管理系统根据变量的类型为变量分配存储空间，分配的空间只能用来储存该类型数据。

因此，通过定义不同类型的变量，可以在内存中储存整数、小数或者字符。

### 1.1 内置数据类型

Java 语言提供了八种基本类型。六种数字类型（四个整数型，两个浮点型），一种字符类型，还有一种布尔型。

#### byte

- byte 数据类型是8位、有符号的，以二进制补码表示的整数
- 最小值是 -128（-2^7）
- 最大值是 127（2^7-1）
- 默认值是 0
- byte 类型用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一

```java
byte a = 100;
byte b = -50;
```

#### short

- short 数据类型是 16 位、有符号的以二进制补码表示的整数
- 最小值是 -32768（-2^15）
- 最大值是 32767（2^15 - 1）
- 默认值是 0
- 一个 short 变量是 int 型变量所占空间的二分之一

```java
short s = 1000;
short r = -20000;
```

#### int

- int 数据类型是32位、有符号的以二进制补码表示的整数
- 最小值是 -2,147,483,648（-2^31）
- 最大值是 2,147,483,647（2^31 - 1）
- 一般地整型变量默认为 int 类型
- 默认值是 0

```java
int a = 100000;
int b = -200000;
```

#### long

- long 数据类型是 64 位、有符号的以二进制补码表示的整数
- 最小值是 -9,223,372,036,854,775,808（-2^63）
- 最大值是 9,223,372,036,854,775,807（2^63 -1）
- 默认值是 0L
- 这种类型主要使用在需要比较大整数的系统上

```java
long a = 100000L;
long b = -200000L;
```

> 注意：理论上 "L" 不分大小写，但是若写成 "l" 容易与数字 "1" 混淆，不容易分辩。所以最好大写。

#### float

- float 数据类型是单精度、32位、符合IEEE 754标准的浮点数
- 默认值是 0.0f
- 浮点数不能用来表示精确的值，如货币

```java
float f1 = 234.5f;
```

#### double

- double 数据类型是双精度、64 位、符合 IEEE 754 标准的浮点数
- 浮点数的默认类型为 double 类型
- 默认值是 0.0d
- double 类型同样不能表示精确的值，如货币

```java
double d1 = 7D;
double d2 = 7.;
double d3 = 8.0;
double d4 = 8.D;
double d5 = 12.9867;
```

> 说明：7 是一个 int 字面量，而 7D、7. 和 8.0 是 double 字面量。

#### boolean

- boolean 数据类型表示一位的信息
- 只有两个取值：true 和 false
- 默认值是 false

```java
boolean one = true;
```

#### char

- char 类型是一个单一的 16 位 Unicode 字符
- 最小值是 \u0000（十进制等效值为 0）
- 最大值是 \uffff（即为 65535）
- char 数据类型可以储存任何字符

```java
char letter = 'A';
```

### 1.2 数据类型默认值

下表列出了 Java 各个类型的默认值：

| 数据类型 | 默认值 |
|----------|--------|
| byte | 0 |
| short | 0 |
| int | 0 |
| long | 0L |
| float | 0.0f |
| double | 0.0d |
| char | '\u0000' |
| boolean | false |

### 1.3 引用数据类型

- 引用类型指向一个对象，指向对象的变量是引用变量
- 对象、数组都是引用数据类型
- 所有引用类型的默认值都是 null
- 一个引用变量可以用来引用任何与之兼容的类型

```java
String name = "James";
Site site = new Site("Runoob");
```

---

## 二、Java 变量

在 Java 语言中，所有的变量在使用前必须声明。

声明变量的基本格式如下：

```java
type identifier [ = value][, identifier [= value] ...] ;
```

- type -- 数据类型
- identifier -- 是变量名，可以使用逗号 , 隔开来声明多个同类型变量

```java
int a, b, c;
int d = 3, e = 4, f = 5;
byte z = 22;
String s = "runoob";
double pi = 3.14159;
char x = 'x';
```

### 2.1 局部变量

局部变量是在方法、构造函数或语句块内部声明的变量。

- 局部变量在声明的方法、构造函数或块执行结束后被销毁
- 局部变量在声明时需要初始化，否则会导致编译错误
- 局部变量存储在 Java 虚拟机（JVM）的栈上

```java
public void exampleMethod() {
    int localVar = 10; // 局部变量
}
```

```java
public class LocalVariablesExample {
    public static void main(String[] args) {
        int a = 10;
        int b;
        b = 20;

        System.out.println("a = " + a);
        System.out.println("b = " + b);
    }
}
```

### 2.2 实例变量（成员变量）

实例变量是在类中声明，但在方法、构造函数或块之外。

- 当一个对象被实例化之后，每个实例变量的值就跟着确定
- 实例变量在对象创建的时候创建，在对象被销毁的时候销毁
- 实例变量具有默认值（数值型为 0，布尔型为 false，引用类型为 null）

```java
public class Employee {
    public String name;        // 实例变量
    private double salary;     // 私有实例变量

    public Employee(String empName) {
        name = empName;
    }

    public void setSalary(double empSal) {
        salary = empSal;
    }

    public void printEmp() {
        System.out.println("名字 : " + name);
        System.out.println("薪水 : " + salary);
    }
}
```

### 2.3 静态变量（类变量）

静态变量是在类中用 static 关键字声明的变量，属于类而不是实例。

- 所有该类的实例共享同一个静态变量的值
- 静态变量在类加载时被初始化，而且只初始化一次
- 静态变量的生命周期与程序的生命周期一样长

```java
public class Counter {
    private static int count = 0;

    public Counter() {
        count++;
    }

    public static int getCount() {
        return count;
    }

    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        Counter c3 = new Counter();
        System.out.println("目前为止创建的对象数: " + Counter.getCount());
    }
}
```

输出结果：

```
目前为止创建的对象数: 3
```

---

## 三、Java 常量

常量在程序运行时是不能被修改的。

在 Java 中使用 final 关键字来修饰常量：

```java
final double PI = 3.1415927;
```

虽然常量名也可以用小写，但为了便于识别，通常使用大写字母表示常量。

### 3.1 字面量

字面量可以赋给任何内置类型的变量。例如：

```java
byte a = 68;
char a = 'A';
```

byte、int、long 和 short 都可以用十进制、16进制以及8进制的方式来表示。

当使用字面量的时候，前缀 0 表示 8 进制，而前缀 0x 代表 16 进制：

```java
int decimal = 100;
int octal = 0144;      // 八进制，对应十进制 100
int hexa = 0x64;        // 十六进制，对应十进制 100
```

### 3.2 转义字符

Java 语言支持一些特殊的转义字符序列：

| 符号 | 字符含义 |
|------|----------|
| \n | 换行 (0x0a) |
| \r | 回车 (0x0d) |
| \f | 换页符 (0x0c) |
| \b | 退格 (0x08) |
| \0 | 空字符 (0x0) |
| \s | 空格 (0x20) |
| \t | 制表符 |
| \" | 双引号 |
| \' | 单引号 |
| \\ | 反斜杠 |

```java
char c1 = '\u0001';
String s1 = "\u0001";
```

---

## 四、变量命名规则

在 Java 中，变量名有一些命名规则和约定：

- **使用有意义的名字**：变量名应该具有清晰的含义，能够准确地反映变量的用途
- **驼峰命名法（Camel Case）**：将每个单词的首字母大写，除了第一个单词外，例如 `myVariableName`
- **避免关键字**：不要使用 Java 关键字（例如 class、int、boolean 等）作为变量名
- **区分大小写**：Java 是大小写敏感的
- **不以数字开头**：变量名不能以数字开头，但可以包含数字

### 4.1 各种变量的命名规范

**局部变量和实例变量**：使用驼峰命名法，以小写字母开头

```java
int myLocalVariable;
private int myInstanceVariable;
```

**静态变量**：可以使用驼峰命名法，也可以使用大写蛇形命名法

```java
public static int myStaticVariable;
public static final int MAX_SIZE = 100;
```

**常量**：使用全大写字母，单词之间用下划线分隔

```java
public static final double PI = 3.14;
public static final int MAX_CONNECTIONS = 1000;
```

**参数**：使用驼峰命名法

```java
public void myMethod(int myParameter) {
}
```

---

## 五、数据类型转换

整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型，然后进行运算。

转换从低级到高级：

```
byte, short, char → int → long → float → double
```

### 5.1 自动类型转换

必须满足转换前的数据类型的位数要低于转换后的数据类型。

```java
public class ZiDongLeiZhuan {
    public static void main(String[] args) {
        char c1 = 'a';
        int i1 = c1;
        System.out.println("char自动类型转换为int后的值等于" + i1);

        char c2 = 'A';
        int i2 = c2 + 1;
        System.out.println("char类型和int计算后的值等于" + i2);
    }
}
```

输出结果：

```
char自动类型转换为int后的值等于97
char类型和int计算后的值等于66
```

> 解析：c1 的值为字符 'a'，查 ASCII 码表可知对应的 int 类型值为 97，'A' 对应值为 65，所以 i2 = 65 + 1 = 66。

### 5.2 强制类型转换

在把容量大的类型转换为容量小的类型时必须使用强制类型转换。

格式：`(type)value`

```java
public class ForceTransform {
    public static void main(String[] args) {
        int i1 = 123;
        byte b = (byte) i1;
        System.out.println("int强制类型转换为byte后的值等于" + b);
    }
}
```

输出结果：

```
int强制类型转换为byte后的值等于123
```

### 5.3 类型转换注意事项

- 不能对 boolean 类型进行类型转换
- 在把容量大的类型转换为容量小的类型时可能会导致溢出或损失精度

```java
int i = 128;
byte b = (byte) i;  // byte 类型最大值是 127，所以会导致溢出
```

- 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入

```java
(int) 23.7 == 23;
(int) -45.89f == -45;
```

---

## 六、Java 运算符

计算机的最基本用途之一就是执行数学运算。Java 提供了一套丰富的运算符来操纵变量。

### 6.1 算术运算符

| 操作符 | 描述 | 例子 |
|--------|------|------|
| + | 加法 - 相加运算符两侧的值 | A + B 等于 30 |
| - | 减法 - 左操作数减去右操作数 | A - B 等于 -10 |
| * | 乘法 - 相乘操作符两侧的值 | A * B 等于 200 |
| / | 除法 - 左操作数除以右操作数 | B / A 等于 2 |
| % | 取余 - 左操作数除以右操作数的余数 | B % A 等于 0 |
| ++ | 自增: 操作数的值增加1 | B++ 或 ++B 等于 21 |
| -- | 自减: 操作数的值减少1 | B-- 或 --B 等于 19 |

```java
public class Test {
    public static void main(String[] args) {
        int a = 10;
        int b = 20;
        int c = 25;
        int d = 25;

        System.out.println("a + b = " + (a + b));
        System.out.println("a - b = " + (a - b));
        System.out.println("a * b = " + (a * b));
        System.out.println("b / a = " + (b / a));
        System.out.println("b % a = " + (b % a));
        System.out.println("c % a = " + (c % a));
        System.out.println("a++   = " + (a++));
        System.out.println("a--   = " + (a--));
        System.out.println("d++   = " + (d++));
        System.out.println("++d   = " + (++d));
    }
}
```

输出结果：

```
a + b = 30
a - b = -10
a * b = 200
b / a = 2
b % a = 0
c % a = 5
a++   = 10
a--   = 11
d++   = 25
++d   = 27
```

### 6.2 自增自减运算符详解

- **前缀自增自减法 (++a, --a)**：先进行自增或自减运算，再进行表达式运算
- **后缀自增自减法 (a++, a--)**：先进行表达式运算，再进行自增或自减运算

```java
public class selfAddMinus {
    public static void main(String[] args) {
        int a = 5;
        int b = 5;
        int x = 2 * ++a;
        int y = 2 * b++;

        System.out.println("自增运算符前缀运算后 a = " + a + ", x = " + x);
        System.out.println("自增运算符后缀运算后 b = " + b + ", y = " + y);
    }
}
```

输出结果：

```
自增运算符前缀运算后 a = 6, x = 12
自增运算符后缀运算后 b = 6, y = 10
```

### 6.3 关系运算符

| 运算符 | 描述 | 例子 |
|--------|------|------|
| == | 检查两个操作数的值是否相等 | (A == B) 为假 |
| != | 检查两个操作数的值是否不相等 | (A != B) 为真 |
| > | 检查左操作数的值是否大于右操作数 | (A > B) 为假 |
| < | 检查左操作数的值是否小于右操作数 | (A < B) 为真 |
| >= | 检查左操作数的值是否大于或等于右操作数 | (A >= B) 为假 |
| <= | 检查左操作数的值是否小于或等于右操作数 | (A <= B) 为真 |

```java
public class Test {
    public static void main(String[] args) {
        int a = 10;
        int b = 20;

        System.out.println("a == b = " + (a == b));
        System.out.println("a != b = " + (a != b));
        System.out.println("a > b = " + (a > b));
        System.out.println("a < b = " + (a < b));
        System.out.println("b >= a = " + (b >= a));
        System.out.println("b <= a = " + (b <= a));
    }
}
```

### 6.4 位运算符

位运算符作用在所有的位上，并且按位运算。

假设 a = 60，b = 13，它们的二进制格式表示如下：

```
A = 0011 1100
B = 0000 1101
-----------------
A & B = 0000 1100
A | B = 0011 1101
A ^ B = 0011 0001
~A    = 1100 0011
```

| 操作符 | 描述 | 例子 |
|--------|------|------|
| & | 如果相对应位都是1，则结果为1，否则为0 | (A & B) 得到 12 |
| \| | 如果相对应位都是0，则结果为0，否则为1 | (A \| B) 得到 61 |
| ^ | 如果相对应位值相同，则结果为0，否则为1 | (A ^ B) 得到 49 |
| ~ | 按位取反运算符翻转操作数的每一位 | (~A) 得到 -61 |
| << | 按位左移运算符。左操作数按位左移右操作数指定的位数 | A << 2 得到 240 |
| >> | 按位右移运算符。左操作数按位右移右操作数指定的位数 | A >> 2 得到 15 |
| >>> | 按位右移补零操作符 | A >>> 2 得到 15 |

```java
public class Test {
    public static void main(String[] args) {
        int a = 60;
        int b = 13;

        System.out.println("a & b = " + (a & b));
        System.out.println("a | b = " + (a | b));
        System.out.println("a ^ b = " + (a ^ b));
        System.out.println("~a = " + (~a));
        System.out.println("a << 2 = " + (a << 2));
        System.out.println("a >> 2 = " + (a >> 2));
        System.out.println("a >>> 2 = " + (a >>> 2));
    }
}
```

### 6.5 逻辑运算符

| 操作符 | 描述 | 例子 |
|--------|------|------|
| && | 称为逻辑与运算符。当且仅当两个操作数都为真，条件才为真 | (A && B) 为假 |
| \|\| | 称为逻辑或操作符。如果任何两个操作数任何一个为真，条件为真 | (A \|\| B) 为真 |
| ! | 称为逻辑非运算符。用来反转操作数的逻辑状态 | !(A && B) 为真 |

```java
public class Test {
    public static void main(String[] args) {
        boolean a = true;
        boolean b = false;

        System.out.println("a && b = " + (a && b));
        System.out.println("a || b = " + (a || b));
        System.out.println("!(a && b) = " + !(a && b));
    }
}
```

**短路逻辑运算符**：当使用与逻辑运算符时，在两个操作数都为 true 时，结果才为 true，但是当得到第一个操作为 false 时，其结果就必定是 false，这时候就不会再判断第二个操作了。

```java
public class LuoJi {
    public static void main(String[] args) {
        int a = 5;
        boolean b = (a < 4) && (a++ < 10);
        System.out.println("使用短路逻辑运算符的结果为 " + b);
        System.out.println("a 的结果为 " + a);
    }
}
```

输出结果：

```
使用短路逻辑运算符的结果为 false
a 的结果为 5
```

> 解析：该程序使用到了短路逻辑运算符(&&)，首先判断 a<4 的结果为 false，则 b 的结果必定是 false，所以不再执行第二个操作 a++<10 的判断，所以 a 的值为 5。

### 6.6 赋值运算符

| 操作符 | 描述 | 例子 |
|--------|------|------|
| = | 简单的赋值运算符，将右操作数的值赋给左侧操作数 | C = A + B |
| += | 加和赋值操作符 | C += A 等价于 C = C + A |
| -= | 减和赋值操作符 | C -= A 等价于 C = C - A |
| *= | 乘和赋值操作符 | C *= A 等价于 C = C * A |
| /= | 除和赋值操作符 | C /= A 等价于 C = C / A |
| %= | 取模和赋值操作符 | C %= A 等价于 C = C % A |
| <<= | 左移位赋值运算符 | C <<= 2 等价于 C = C << 2 |
| >>= | 右移位赋值运算符 | C >>= 2 等价于 C = C >> 2 |
| &= | 按位与赋值运算符 | C &= 2 等价于 C = C & 2 |
| ^= | 按位异或赋值操作符 | C ^= 2 等价于 C = C ^ 2 |
| \|= | 按位或赋值操作符 | C \|= 2 等价于 C = C \| 2 |

### 6.7 条件运算符（?:）

条件运算符也被称为三元运算符。该运算符有3个操作数，并且需要判断布尔表达式的值。

```java
variable x = (expression) ? value if true : value if false
```

```java
public class Test {
    public static void main(String[] args) {
        int a, b;
        a = 10;
        b = (a == 1) ? 20 : 30;
        System.out.println("Value of b is : " + b);

        b = (a == 10) ? 20 : 30;
        System.out.println("Value of b is : " + b);
    }
}
```

输出结果：

```
Value of b is : 30
Value of b is : 20
```

### 6.8 instanceof 运算符

该运算符用于操作对象实例，检查该对象是否是一个特定类型（类类型或接口类型）。

```java
( Object reference variable ) instanceof (class/interface type)
```

```java
String name = "James";
boolean result = name instanceof String; // 返回 true
```

```java
class Vehicle {}

public class Car extends Vehicle {
    public static void main(String[] args) {
        Vehicle a = new Car();
        boolean result = a instanceof Car;
        System.out.println(result);
    }
}
```

输出结果：

```
true
```

---

## 七、运算符优先级

下表中具有最高优先级的运算符在表格的最上面，最低优先级的在表格的底部。

| 类别 | 操作符 | 关联性 |
|------|--------|--------|
| 后缀 | () [] . | 左到右 |
| 一元 | expr++ expr-- | 左到右 |
| 一元 | ++expr --expr + - ~ ! | 从右到左 |
| 乘性 | * / % | 左到右 |
| 加性 | + - | 左到右 |
| 移位 | >> >>> << | 左到右 |
| 关系 | > >= < <= | 左到右 |
| 相等 | == != | 左到右 |
| 按位与 | & | 左到右 |
| 按位异或 | ^ | 左到右 |
| 按位或 | \| | 左到右 |
| 逻辑与 | && | 左到右 |
| 逻辑或 | \|\| | 左到右 |
| 条件 | ?: | 从右到左 |
| 赋值 | = += -= *= /= %= >>= <<= &= ^= \|= | 从右到左 |
| 逗号 | , | 左到右 |

例如：

```java
x = 7 + 3 * 2;  // x 得到 13，而不是 20
// 因为乘法运算符比加法运算符有较高的优先级
```

---

## 八、练习

1. 声明 byte、short、int、long、float、double、char、boolean 类型的变量
2. 创建一个程序，使用各种算术运算符计算两个数的运算结果
3. 练习自增自减运算符的前缀和后缀用法
4. 编写程序演示自动类型转换和强制类型转换
5. 使用关系运算符比较两个数的大小
6. 使用逻辑运算符组合多个条件
7. 编写程序演示三元运算符的用法
8. 验证运算符的优先级
