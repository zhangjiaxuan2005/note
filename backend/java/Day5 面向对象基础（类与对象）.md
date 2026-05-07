# Java 面向对象基础（类与对象）

## 一、面向对象概述

Java 作为一种面向对象的编程语言，支持以下基本概念：

| 概念 | 描述 |
|------|------|
| **类（Class）** | 定义对象的蓝图，包括属性和方法 |
| **对象（Object）** | 类的实例，具有状态和行为 |
| **封装（Encapsulation）** | 将对象的状态私有化，通过公共方法访问 |
| **继承（Inheritance）** | 一个类可以继承另一个类的属性和方法 |
| **多态（Polymorphism）** | 对象可以表现为多种形态，通过方法重载和重写实现 |
| **抽象（Abstraction）** | 使用抽象类和接口定义必须实现的方法 |

### 1.1 类与对象的关系

- **类**：是对象的模板，描述一类对象的行为和状态
- **对象**：是类的一个实例，有状态和行为

### 1.2 现实世界的类比

拿一条狗来举例：
- **状态**：名字、品种、颜色、年龄
- **行为**：叫、摇尾巴、跑、吃

软件对象也有状态和行为：
- **状态** → 属性（成员变量）
- **行为** → 方法

---

## 二、Java 中的类

### 2.1 类的定义

类可以看成是创建 Java 对象的模板。

```java
public class Dog {
    String breed;    // 品种
    int size;        // 大小
    String colour;   // 颜色
    int age;         // 年龄
    
    void eat() {}    // 吃
    void run() {}    // 跑
    void sleep() {}  // 睡觉
    void bark() {}   // 叫
}
```

### 2.2 类的组成

一个类可以包含以下类型：

#### 变量类型

- **局部变量**：在方法、构造方法或者语句块中定义的变量，方法结束后自动销毁
- **成员变量**：定义在类中，方法体之外，创建对象时实例化
- **类变量**：声明在类中，方法体之外，必须声明为 `static` 类型

#### 方法

类的行为，包含在类中的函数。

### 2.3 源文件声明规则

- 一个源文件中只能有一个 `public` 类
- 源文件的名称应该和 `public` 类的类名保持一致
- `package` 语句应该在源文件的首行
- `import` 语句应该放在 `package` 语句和类定义之间

---

## 三、构造方法

### 3.1 构造方法的概念

每个类都有构造方法。如果没有显式地为类定义构造方法，Java 编译器将会为该类提供一个默认构造方法。

**构造方法的特点：**
- 方法名与类名相同
- 没有返回类型（连 `void` 都不写）
- 创建对象时自动调用
- 不能直接调用，只能通过 `new` 关键字调用
- 支持重载

### 3.2 构造方法的类型

**无参构造方法（默认构造方法）**

```java
public class Person {
    public Person() {
        System.out.println("Person 对象已创建");
    }
}
```

**有参构造方法**

```java
public class Person {
    String name;
    int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### 3.3 构造方法的重载

可以在同一个类中定义多个构造方法，只要参数列表不同即可。

```java
public class Person {
    String name;
    int age;
    
    // 无参构造
    public Person() {
        this.name = "Unknown";
        this.age = 0;
    }
    
    // 单参数构造
    public Person(String name) {
        this.name = name;
        this.age = 0;
    }
    
    // 双参数构造
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

创建对象时，Java 会根据传入的参数自动选择匹配的构造方法：

```java
Person p1 = new Person();           // 调用无参构造
Person p2 = new Person("Alice");    // 调用单参数构造
Person p3 = new Person("Bob", 30);  // 调用双参数构造
```

### 3.4 this 关键字

在构造方法中，`this` 关键字通常用于：

**1、引用当前对象的属性**

当参数名与类属性名相同时，使用 `this` 来区分：

```java
public Person(String name, int age) {
    this.name = name;  // this.name 表示类的属性
    this.age = age;
}
```

**2、调用另一个构造方法**

使用 `this()` 调用当前类的其他构造方法，必须放在第一行：

```java
public Person(String name) {
    this(name, 0);  // 调用双参数构造方法
}

public Person(String name, int age) {
    this.name = name;
    this.age = age;
}
```

---

## 四、创建对象

对象是根据类创建的。在 Java 中，使用关键字 `new` 来创建一个新的对象。创建对象需要以下三步：

1. **声明**：声明一个对象，包括对象名称和对象类型
2. **实例化**：使用关键字 `new` 来创建一个对象
3. **初始化**：使用 `new` 创建对象时，会调用构造方法初始化对象

### 4.1 创建对象示例

```java
public class Puppy {
    public Puppy(String name) {
        System.out.println("小狗的名字是: " + name);
    }
    
    public static void main(String[] args) {
        Puppy myPuppy = new Puppy("Tommy");
    }
}
```

运行结果：

```
小狗的名字是: Tommy
```

### 4.2 访问实例变量和方法

通过已创建的对象来访问成员变量和成员方法：

```java
Object referenceVariable = new Constructor();
referenceVariable.variableName;
referenceVariable.methodName();
```

### 4.3 完整示例

```java
public class Puppy {
    private int age;
    private String name;
    
    public Puppy(String name) {
        this.name = name;
        System.out.println("小狗的名字是: " + name);
    }
    
    public void setAge(int age) {
        this.age = age;
    }
    
    public int getAge() {
        return age;
    }
    
    public String getName() {
        return name;
    }
    
    public static void main(String[] args) {
        Puppy myPuppy = new Puppy("Tommy");
        myPuppy.setAge(2);
        
        int age = myPuppy.getAge();
        System.out.println("小狗的年龄为: " + age);
        System.out.println("变量值: " + myPuppy.getAge());
    }
}
```

运行结果：

```
小狗的名字是: Tommy
小狗的年龄为: 2
变量值: 2
```

---

## 五、访问修饰符

Java 提供了 4 种访问权限修饰符：

| 修饰符 | 当前类 | 同一包内 | 子孙类(同一包) | 子孙类(不同包) | 其他包 |
|--------|--------|----------|----------------|----------------|--------|
| `public` | Y | Y | Y | Y | Y |
| `protected` | Y | Y | Y | Y/N | N |
| `default` | Y | Y | Y | N | N |
| `private` | Y | N | N | N | N |

### 5.1 默认访问修饰符

如果不使用任何修饰符，则为默认访问权限，只能被同一包中的类访问。

```java
class MyClass {
    int x = 10;
    
    void display() {
        System.out.println("Value of x is: " + x);
    }
}
```

### 5.2 私有访问修饰符 - private

被声明为 `private` 的方法、变量和构造方法只能被所属类访问。

```java
public class Logger {
    private String format;
    
    public String getFormat() {
        return this.format;
    }
    
    public void setFormat(String format) {
        this.format = format;
    }
}
```

### 5.3 公有访问修饰符 - public

被声明为 `public` 的类、方法、构造方法和接口能够被任何其他类访问。

```java
public static void main(String[] arguments) {
    // main 方法必须是 public
}
```

### 5.4 受保护的访问修饰符 - protected

被声明为 `protected` 的变量、方法和构造器：
- 能被同一个包中的任何其他类访问
- 能被子类访问（无论是否在同一包中）

```java
class AudioPlayer {
    protected boolean openSpeaker(Speaker sp) {
        // ...
    }
}

class StreamingAudioPlayer extends AudioPlayer {
    @Override
    protected boolean openSpeaker(Speaker sp) {
        // 子类可以访问并重写
    }
}
```

### 5.5 访问控制和继承

- 父类中声明为 `public` 的方法在子类中也必须为 `public`
- 父类中声明为 `protected` 的方法在子类中可以声明为 `protected` 或 `public`
- 父类中声明为 `private` 的方法，不能被子类继承

---

## 六、非访问修饰符

### 6.1 static 修饰符

**静态变量：**

`static` 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。

```java
public class InstanceCounter {
    private static int numInstances = 0;
    
    protected static int getCount() {
        return numInstances;
    }
    
    private static void addInstance() {
        numInstances++;
    }
    
    InstanceCounter() {
        InstanceCounter.addInstance();
    }
    
    public static void main(String[] arguments) {
        System.out.println("Starting with " + InstanceCounter.getCount() + " instances");
        
        for (int i = 0; i < 500; ++i) {
            new InstanceCounter();
        }
        
        System.out.println("Created " + InstanceCounter.getCount() + " instances");
    }
}
```

运行结果：

```
Starting with 0 instances
Created 500 instances
```

**静态方法：**

静态方法不能使用类的非静态变量，从参数列表得到数据。

```java
public class MathUtil {
    public static int add(int a, int b) {
        return a + b;
    }
    
    public static int max(int a, int b) {
        return a > b ? a : b;
    }
}

// 使用
int sum = MathUtil.add(5, 3);
int maxNum = MathUtil.max(10, 20);
```

### 6.2 final 修饰符

**final 变量：**

`final` 表示"最后的、最终的"含义，变量一旦赋值后，不能被重新赋值。

```java
public class Test {
    final int value = 10;
    public static final int BOXWIDTH = 6;
    static final String TITLE = "Manager";
}
```

**final 方法：**

父类中的 `final` 方法可以被子类继承，但不能被子类重写。

```java
public class Test {
    public final void changeName() {
        // 此方法不能被重写
    }
}
```

**final 类：**

`final` 类不能被继承。

```java
public final class Test {
    // 此类不能被继承
}
```

### 6.3 abstract 修饰符

**抽象类：**

抽象类不能用来实例化对象，声明抽象类的目的是为了将来对该类进行扩充。

```java
abstract class Caravan {
    private double price;
    private String model;
    
    public abstract void goFast();    // 抽象方法
    public abstract void changeColor();
}
```

**抽象方法：**

抽象方法是一种没有任何实现的方法，具体实现由子类提供。

```java
public abstract class SuperClass {
    abstract void m();  // 抽象方法，没有实现
}

class SubClass extends SuperClass {
    void m() {
        // 实现抽象方法
    }
}
```

### 6.4 synchronized 修饰符

`synchronized` 关键字声明的方法同一时间只能被一个线程访问。

```java
public synchronized void showDetails() {
    // 线程安全的方法
}
```

### 6.5 transient 修饰符

序列化的对象包含被 `transient` 修饰的实例变量时，JVM 会跳过该变量。

```java
public transient int limit = 55;
```

### 6.6 volatile 修饰符

`volatile` 修饰的成员变量在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。

```java
public class MyRunnable implements Runnable {
    private volatile boolean active;
    
    public void run() {
        active = true;
        while (active) {
            // 循环执行
        }
    }
    
    public void stop() {
        active = false;
    }
}
```

---

## 七、封装

### 7.1 封装的概念

封装是将数据和操作数据的方法绑定在一起，隐藏内部实现细节，只通过公共接口访问数据。

### 7.2 Getter 和 Setter 方法

```java
public class Person {
    // 私有属性
    private String name;
    private int age;
    
    // Getter 方法
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
    
    // Setter 方法（可以添加验证逻辑）
    public void setName(String name) {
        if (name != null && !name.isEmpty()) {
            this.name = name;
        } else {
            System.out.println("姓名不能为空");
        }
    }
    
    public void setAge(int age) {
        if (age >= 0 && age <= 150) {
            this.age = age;
        } else {
            System.out.println("年龄必须在 0-150 之间");
        }
    }
}
```

### 7.3 使用封装

```java
public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        
        person.setName("张三");
        person.setAge(25);
        
        System.out.println("姓名: " + person.getName());
        System.out.println("年龄: " + person.getAge());
    }
}
```

---

## 八、代码块

### 8.1 静态代码块

静态代码块在类加载时执行，只执行一次。

```java
public class Configuration {
    private static String config;
    
    static {
        System.out.println("加载配置...");
        config = loadConfig();
    }
    
    private static String loadConfig() {
        return "配置内容";
    }
}
```

### 8.2 实例代码块

实例代码块在每次创建对象时执行，在构造方法之前执行。

```java
public class Person {
    private String name;
    
    {
        System.out.println("初始化对象...");
        this.name = "默认名字";
    }
    
    public Person() {
        System.out.println("构造方法执行");
    }
}
```

### 8.3 执行顺序

1. 静态代码块（类加载时执行，只执行一次）
2. 实例代码块（每次创建对象时执行）
3. 构造方法（每次创建对象时执行）

---

## 九、完整示例：Employee 类

### Employee.java

```java
public class Employee {
    private String name;
    private int age;
    private String designation;
    private double salary;
    
    public Employee(String name) {
        this.name = name;
    }
    
    public void setAge(int age) {
        this.age = age;
    }
    
    public int getAge() {
        return age;
    }
    
    public void setDesignation(String designation) {
        this.designation = designation;
    }
    
    public String getDesignation() {
        return designation;
    }
    
    public void setSalary(double salary) {
        this.salary = salary;
    }
    
    public double getSalary() {
        return salary;
    }
    
    public void printEmployee() {
        System.out.println("名字: " + name);
        System.out.println("年龄: " + age);
        System.out.println("职位: " + designation);
        System.out.println("薪水: " + salary);
    }
}
```

### EmployeeTest.java

```java
public class EmployeeTest {
    public static void main(String[] args) {
        Employee empOne = new Employee("RUNOOB1");
        Employee empTwo = new Employee("RUNOOB2");
        
        empOne.setAge(26);
        empOne.setDesignation("高级程序员");
        empOne.setSalary(1000);
        empOne.printEmployee();
        
        empTwo.setAge(21);
        empTwo.setDesignation("菜鸟程序员");
        empTwo.setSalary(500);
        empTwo.printEmployee();
    }
}
```

运行结果：

```
名字: RUNOOB1
年龄: 26
职位: 高级程序员
薪水: 1000.0
名字: RUNOOB2
年龄: 21
职位: 菜鸟程序员
薪水: 500.0
```

---

## 十、练习

1. 定义一个 `Circle` 类，包含半径属性和计算面积、周长的方法
2. 定义一个 `Student` 类，包含学号、姓名、成绩属性，提供 getter/setter 方法
3. 定义一个 `BankAccount` 类，实现存款、取款功能
4. 创建一个 `Calculator` 工具类，提供静态方法实现加减乘除运算
5. 使用 `Counter` 类统计某个类创建了多少个对象
6. 定义一个抽象类 `Shape`，包含抽象方法 `draw()`，然后创建 `Circle`、`Rectangle`、`Triangle` 类实现该接口
7. 使用 `final` 关键字定义常量
