# Day7 接口与抽象类

## 一、Java 接口

接口（Interface）是一个抽象类型，是抽象方法的集合，接口通常以 `interface` 来声明。一个类通过实现接口的方式，从而来继承接口的抽象方法。

### 1.1 接口与类的区别

| 特性 | 接口 | 类 |
|------|------|----|
| 实例化 | 不能被实例化 | 可以被实例化 |
| 构造方法 | 没有 | 有 |
| 方法 | 默认为 `public abstract`（Java 8+ 可有默认方法） | 可以有各种方法 |
| 成员变量 | 只能是 `public static final` 常量 | 可以有各种类型 |
| 继承方式 | implements | extends |
| 多重继承 | 支持 | 不支持 |

### 1.2 接口的声明

接口的声明语法格式如下：

```java
[可见度] interface 接口名称 [extends 其他的接口名] {
    // 常量声明
    // 抽象方法声明
    // 默认方法（Java 8+）
    // 静态方法（Java 8+）
}
```

### 1.3 接口示例

**Animal.java 文件代码：**

```java
interface Animal {
    // 常量（默认 public static final）
    int MAX_AGE = 100;
    
    // 抽象方法（默认 public abstract）
    public void eat();
    public void travel();
}
```

### 1.4 接口的实现

当类实现接口的时候，类要实现接口中所有的方法。否则，类必须声明为抽象的类。

**MammalInt.java 文件代码：**

```java
public class MammalInt implements Animal {
    public void eat() {
        System.out.println("Mammal eats");
    }
    
    public void travel() {
        System.out.println("Mammal travels");
    }
    
    public int noOfLegs() {
        return 0;
    }
    
    public static void main(String args[]) {
        MammalInt m = new MammalInt();
        m.eat();
        m.travel();
    }
}
```

以上实例编译运行结果如下：

```
Mammal eats
Mammal travels
```

### 1.5 接口的继承

一个接口能继承另一个接口，使用 `extends` 关键字。

```java
public interface Sports {
    public void setHomeTeam(String name);
    public void setVisitingTeam(String name);
}

public interface Football extends Sports {
    public void homeTeamScored(int points);
    public void visitingTeamScored(int points);
    public void endOfQuarter(int quarter);
}
```

### 1.6 接口的多继承

在 Java 中，类的多继承是不合法的，但接口允许多继承。

```java
public interface Hockey extends Sports, Event {
    // 继承了 Sports 和 Event 接口的方法
}
```

---

## 二、Java 抽象类

在面向对象的概念中，所有的对象都是通过类来描绘的，但并不是所有的类都是用来描绘对象的。如果一个类中没有包含足够的信息来描绘一个具体的对象，这样的类就是抽象类。

### 2.1 抽象类的特点

- 抽象类不能被实例化
- 抽象类必须被继承才能使用
- 抽象类可以包含抽象方法和普通方法
- 抽象类可以包含构造方法和成员变量

### 2.2 抽象类的定义

使用 `abstract class` 来定义抽象类。

**Employee.java 文件代码：**

```java
public abstract class Employee {
    private String name;
    private String address;
    private int number;
    
    public Employee(String name, String address, int number) {
        System.out.println("Constructing an Employee");
        this.name = name;
        this.address = address;
        this.number = number;
    }
    
    public double computePay() {
        System.out.println("Inside Employee computePay");
        return 0.0;
    }
    
    public void mailCheck() {
        System.out.println("Mailing a check to " + this.name + " " + this.address);
    }
    
    // 抽象方法
    public abstract double calculateBonus();
}
```

### 2.3 继承抽象类

**Salary.java 文件代码：**

```java
public class Salary extends Employee {
    private double salary;
    
    public Salary(String name, String address, int number, double salary) {
        super(name, address, number);
        setSalary(salary);
    }
    
    public void mailCheck() {
        System.out.println("Within mailCheck of Salary class ");
        System.out.println("Mailing check to " + getName() + " with salary " + salary);
    }
    
    public double getSalary() {
        return salary;
    }
    
    public void setSalary(double newSalary) {
        if (newSalary >= 0.0) {
            salary = newSalary;
        }
    }
    
    public double computePay() {
        System.out.println("Computing salary pay for " + getName());
        return salary / 52;
    }
    
    // 实现抽象方法
    @Override
    public double calculateBonus() {
        return salary * 0.1;
    }
}
```

**AbstractDemo.java 文件代码：**

```java
public class AbstractDemo {
    public static void main(String[] args) {
        Salary s = new Salary("Mohd Mohtashim", "Ambehta, UP", 3, 3600.00);
        Employee e = new Salary("John Adams", "Boston, MA", 2, 2400.00);
        
        System.out.println("Call mailCheck using Salary reference --");
        s.mailCheck();
        
        System.out.println("\nCall mailCheck using Employee reference--");
        e.mailCheck();
    }
}
```

以上程序编译运行结果如下：

```
Constructing an Employee
Constructing an Employee
Call mailCheck using Salary reference --
Within mailCheck of Salary class
Mailing check to Mohd Mohtashim with salary 3600.0

Call mailCheck using Employee reference--
Within mailCheck of Salary class
Mailing check to John Adams with salary 2400.0
```

### 2.4 抽象方法

抽象方法只包含一个方法名，而没有方法体。

```java
public abstract class Employee {
    // 抽象方法，没有方法体
    public abstract double computePay();
}
```

声明抽象方法会造成以下两个结果：
- 如果一个类包含抽象方法，那么该类必须是抽象类
- 任何子类必须重写父类的抽象方法，或者声明自身为抽象类

---

## 三、抽象类和接口的区别

| 特性 | 抽象类 | 接口 |
|------|--------|------|
| 方法实现 | 可以有方法体 | 不能有方法体（Java 8+ 默认方法除外） |
| 成员变量 | 可以是各种类型 | 只能是 `public static final` |
| 静态方法 | 可以有 | Java 8+ 可以有 |
| 构造方法 | 可以有 | 没有 |
| 继承 | 单继承 | 多继承 |
| 设计目的 | 定义模板，强调"是什么" | 定义行为规范，强调"能做什么" |

---

## 四、Java 8 接口新特性

### 4.1 默认方法

使用 `default` 关键字修饰，可以在接口中提供方法的具体实现。

```java
interface Vehicle {
    void start();
    
    default void stop() {
        System.out.println("Vehicle stopped");
    }
}
```

### 4.2 静态方法

使用 `static` 关键字，可以在接口中定义静态方法。

```java
interface Vehicle {
    static void checkVehicle() {
        System.out.println("Checking vehicle...");
    }
}
```

---

## 五、标记接口

标记接口是没有任何方法和属性的接口，它仅仅表明它的类属于一个特定的类型。

```java
public interface Serializable {
    // 空接口，作为标记
}
```

标记接口的主要用途：
1. 建立一个公共的父接口
2. 向一个类添加数据类型

---

## 六、练习

1. 创建一个 `Shape` 接口，包含计算面积和周长的方法，然后创建 `Circle`、`Rectangle`、`Triangle` 类实现该接口
2. 创建一个抽象类 `Vehicle`，包含抽象方法 `drive()`，然后创建 `Car`、`Motorcycle` 子类
3. 设计一个接口 `Playable`，包含 `play()` 方法，让 `MusicPlayer` 和 `VideoPlayer` 类实现它
4. 区分什么时候应该使用接口，什么时候应该使用抽象类