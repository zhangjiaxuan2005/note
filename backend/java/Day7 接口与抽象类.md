# Day7 接口与抽象类

## 一、接口（Interface）

### 1.1 接口的定义

```java
public interface Flyable {
    // 常量（默认 public static final）
    int MAX_HEIGHT = 10000;
    
    // 抽象方法（默认 public abstract）
    void fly();
    
    // 抽象方法
    void land();
    
    // Java 8+ 默认方法
    default void prepareForFlight() {
        System.out.println("准备起飞...");
    }
    
    // Java 8+ 静态方法
    static void checkWeather() {
        System.out.println("检查天气状况");
    }
}
```

### 1.2 接口的实现

```java
// 实现接口使用 implements 关键字
public class Bird implements Flyable {
    private String name;
    
    public Bird(String name) {
        this.name = name;
    }
    
    // 必须实现接口的所有抽象方法
    @Override
    public void fly() {
        System.out.println(name + "正在飞翔");
    }
    
    @Override
    public void land() {
        System.out.println(name + "正在降落");
    }
    
    // 可以选择性地重写默认方法
    @Override
    public void prepareForFlight() {
        Flyable.super.prepareForFlight();
        System.out.println(name + "展开翅膀");
    }
}
```

### 1.3 接口的特点
- 接口不能被实例化
- 接口中的方法默认是 `public abstract`（Java 8+ 可以有默认方法和静态方法）
- 接口中的属性默认是 `public static final`（常量）
- 一个类可以实现多个接口
- 接口可以继承其他接口

### 1.4 多接口实现

```java
interface Swimable {
    void swim();
}

interface Runnable {
    void run();
}

// 一个类可以实现多个接口
public class Duck implements Flyable, Swimable, Runnable {
    @Override
    public void fly() {
        System.out.println("鸭子飞翔");
    }
    
    @Override
    public void land() {
        System.out.println("鸭子降落");
    }
    
    @Override
    public void swim() {
        System.out.println("鸭子游泳");
    }
    
    @Override
    public void run() {
        System.out.println("鸭子奔跑");
    }
}
```

### 1.5 接口继承

```java
interface Animal {
    void eat();
    void sleep();
}

// 接口可以继承其他接口
interface FlyingAnimal extends Animal {
    void fly();
}

public class Eagle implements FlyingAnimal {
    @Override
    public void eat() {
        System.out.println("鹰吃猎物");
    }
    
    @Override
    public void sleep() {
        System.out.println("鹰在树上睡觉");
    }
    
    @Override
    public void fly() {
        System.out.println("鹰在高空飞翔");
    }
}
```

## 二、抽象类（Abstract Class）

### 2.1 抽象类的定义

```java
public abstract class Animal {
    // 普通成员变量
    protected String name;
    protected int age;
    
    // 构造方法
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    // 普通方法
    public void sleep() {
        System.out.println(name + "正在睡觉");
    }
    
    // 抽象方法（没有实现，必须由子类实现）
    public abstract void eat();
    
    // 抽象方法
    public abstract void makeSound();
}
```

### 2.2 抽象类的继承

```java
// 继承抽象类，必须实现所有抽象方法
public class Dog extends Animal {
    private String breed;
    
    public Dog(String name, int age, String breed) {
        super(name, age);
        this.breed = breed;
    }
    
    @Override
    public void eat() {
        System.out.println(name + "正在吃狗粮");
    }
    
    @Override
    public void makeSound() {
        System.out.println("汪汪汪");
    }
}
```

### 2.3 抽象类的特点
- 抽象类不能被实例化
- 抽象类可以包含抽象方法和普通方法
- 抽象类可以包含构造方法
- 抽象类可以包含成员变量
- 子类继承抽象类时必须实现所有抽象方法

## 三、接口与抽象类的区别

| 特性 | 接口 | 抽象类 |
|------|------|--------|
| 继承方式 | implements | extends |
| 多重继承 | 支持（一个类可实现多个接口） | 不支持（一个类只能继承一个抽象类） |
| 方法实现 | 抽象方法（Java 8+ 可有默认/静态方法） | 可以有抽象方法和具体方法 |
| 成员变量 | 只能是常量（public static final） | 可以有普通成员变量 |
| 构造方法 | 没有 | 可以有 |
| 使用场景 | 定义行为规范，强调"能做什么" | 定义模板，强调"是什么" |

## 四、设计模式应用

### 4.1 策略模式（Strategy Pattern）

```java
// 策略接口
interface PaymentStrategy {
    void pay(double amount);
}

// 具体策略类
class CreditCardPayment implements PaymentStrategy {
    @Override
    public void pay(double amount) {
        System.out.println("使用信用卡支付: " + amount);
    }
}

class WeChatPayment implements PaymentStrategy {
    @Override
    public void pay(double amount) {
        System.out.println("使用微信支付: " + amount);
    }
}

class AlipayPayment implements PaymentStrategy {
    @Override
    public void pay(double amount) {
        System.out.println("使用支付宝支付: " + amount);
    }
}

// 上下文类
class ShoppingCart {
    private PaymentStrategy paymentStrategy;
    
    public void setPaymentStrategy(PaymentStrategy strategy) {
        this.paymentStrategy = strategy;
    }
    
    public void checkout(double amount) {
        paymentStrategy.pay(amount);
    }
}
```

### 4.2 模板方法模式（Template Method Pattern）

```java
abstract class Game {
    // 模板方法
    public final void play() {
        initialize();
        startPlay();
        endPlay();
    }
    
    protected abstract void initialize();
    protected abstract void startPlay();
    protected abstract void endPlay();
}

class Football extends Game {
    @Override
    protected void initialize() {
        System.out.println("足球游戏初始化");
    }
    
    @Override
    protected void startPlay() {
        System.out.println("足球游戏开始");
    }
    
    @Override
    protected void endPlay() {
        System.out.println("足球游戏结束");
    }
}
```

## 五、函数式接口（Java 8+）

### 5.1 函数式接口的定义

```java
// 使用 @FunctionalInterface 注解
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}
```

### 5.2 Lambda 表达式使用

```java
// 使用 Lambda 表达式实现函数式接口
Calculator add = (a, b) -> a + b;
Calculator multiply = (a, b) -> a * b;

System.out.println(add.calculate(5, 3));      // 8
System.out.println(multiply.calculate(5, 3)); // 15
```

### 5.3 常用内置函数式接口

```java
import java.util.function.*;

// Predicate: 接收一个参数，返回布尔值
Predicate<Integer> isEven = n -> n % 2 == 0;

// Function: 接收一个参数，返回一个结果
Function<String, Integer> length = s -> s.length();

// Consumer: 接收一个参数，无返回值
Consumer<String> print = s -> System.out.println(s);

// Supplier: 无参数，返回一个结果
Supplier<Double> random = () -> Math.random();
```

## 六、练习

1. 创建一个 `Shape` 接口，包含计算面积和周长的方法，然后创建 `Circle`、`Rectangle`、`Triangle` 类实现该接口
2. 创建一个抽象类 `Vehicle`，包含抽象方法 `drive()`，然后创建 `Car`、`Motorcycle`、`Bicycle` 子类
3. 使用策略模式实现不同的排序策略（冒泡排序、快速排序、插入排序）
4. 使用函数式接口和 Lambda 表达式实现简单的计算器
5. 分析何时使用接口，何时使用抽象类