# Day5 面向对象基础（类与对象）

## 一、面向对象概念

### 1.1 面向对象的三大特征
- **封装（Encapsulation）**: 将数据和操作数据的方法绑定在一起，隐藏内部实现
- **继承（Inheritance）**: 一个类可以继承另一个类的属性和方法
- **多态（Polymorphism）**: 同一接口可以有不同的实现方式

### 1.2 类与对象的关系
- **类（Class）**: 是对象的模板，定义了对象的属性和行为
- **对象（Object）**: 是类的实例，是具体存在的实体

## 二、类的定义

### 2.1 类的基本结构

```java
public class Person {
    // 属性（成员变量）
    private String name;
    private int age;
    private String gender;
    
    // 构造方法
    public Person() {
        // 默认构造方法
    }
    
    public Person(String name, int age, String gender) {
        this.name = name;
        this.age = age;
        this.gender = gender;
    }
    
    // 方法（行为）
    public void introduce() {
        System.out.println("我叫" + name + "，今年" + age + "岁");
    }
    
    public void birthday() {
        age++;
        System.out.println("生日快乐！现在" + age + "岁了");
    }
}
```

### 2.2 成员变量与局部变量

```java
public class Car {
    // 成员变量（类级别，有默认值）
    private String color;
    private int speed;
    
    public void drive() {
        // 局部变量（方法级别，必须初始化）
        int currentSpeed = 60;
        speed = currentSpeed;
        System.out.println("车速: " + speed);
    }
}
```

### 2.3 访问修饰符

| 修饰符 | 本类 | 同包 | 子类 | 其他包 |
|--------|------|------|------|--------|
| private | ✓ | ✗ | ✗ | ✗ |
| default（无修饰符） | ✓ | ✓ | ✗ | ✗ |
| protected | ✓ | ✓ | ✓ | ✗ |
| public | ✓ | ✓ | ✓ | ✓ |

## 三、构造方法

### 3.1 构造方法的特点
- 方法名与类名相同
- 没有返回值类型（连 void 都没有）
- 用于初始化对象

### 3.2 构造方法重载

```java
public class Student {
    private String name;
    private int age;
    private String major;
    
    // 无参构造
    public Student() {
        this.name = "未知";
        this.age = 0;
        this.major = "未选择";
    }
    
    // 带一个参数的构造
    public Student(String name) {
        this.name = name;
        this.age = 0;
        this.major = "未选择";
    }
    
    // 带两个参数的构造
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
        this.major = "未选择";
    }
    
    // 带三个参数的构造
    public Student(String name, int age, String major) {
        this.name = name;
        this.age = age;
        this.major = major;
    }
}
```

### 3.3 this 关键字

```java
public class Person {
    private String name;
    
    public void setName(String name) {
        this.name = name; // this.name 指成员变量，name 指参数
    }
    
    public void introduce() {
        System.out.println("我的名字是: " + this.name);
    }
    
    // 在构造方法中调用另一个构造方法
    public Person() {
        this("默认名字"); // 必须在第一行
    }
    
    public Person(String name) {
        this.name = name;
    }
}
```

## 四、封装与访问器方法

### 4.1 Getter 和 Setter 方法

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
            System.out.println("年龄必须在0-150之间");
        }
    }
}
```

### 4.2 使用对象

```java
public class Main {
    public static void main(String[] args) {
        // 创建对象
        Person person = new Person();
        
        // 使用 setter 设置属性
        person.setName("张三");
        person.setAge(25);
        
        // 使用 getter 获取属性
        System.out.println("姓名: " + person.getName());
        System.out.println("年龄: " + person.getAge());
        
        // 调用方法
        person.introduce();
    }
}
```

## 五、静态成员

### 5.1 静态变量（类变量）

```java
public class Counter {
    // 静态变量，属于类，所有对象共享
    private static int count = 0;
    
    public Counter() {
        count++; // 每次创建对象，计数器加1
    }
    
    public static int getCount() {
        return count;
    }
}

// 使用
Counter c1 = new Counter();
Counter c2 = new Counter();
System.out.println(Counter.getCount()); // 输出 2
```

### 5.2 静态方法

```java
public class MathUtil {
    // 静态方法，无需创建对象即可调用
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

### 5.3 静态代码块

```java
public class Configuration {
    private static String config;
    
    // 静态代码块，在类加载时执行
    static {
        System.out.println("加载配置...");
        config = loadConfig();
    }
    
    private static String loadConfig() {
        return "配置内容";
    }
}
```

## 六、代码块

### 6.1 实例代码块

```java
public class Person {
    private String name;
    
    // 实例代码块，在每次创建对象时执行
    {
        System.out.println("初始化对象...");
        this.name = "默认名字";
    }
    
    public Person() {
        System.out.println("构造方法执行");
    }
}
```

### 6.2 执行顺序
1. 静态代码块（类加载时执行，只执行一次）
2. 实例代码块（每次创建对象时执行）
3. 构造方法（每次创建对象时执行）

## 七、练习

1. 定义一个 `Circle` 类，包含半径属性和计算面积、周长的方法
2. 定义一个 `Student` 类，包含学号、姓名、成绩属性，提供 getter/setter 方法
3. 定义一个 `BankAccount` 类，实现存款、取款功能
4. 创建一个 `Calculator` 工具类，提供静态方法实现加减乘除运算
5. 使用 `Counter` 类统计某个类创建了多少个对象