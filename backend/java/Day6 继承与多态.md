# Day6 继承与多态

---

## 一、继承的概念

继承是 Java 面向对象编程技术的一块基石，因为它允许创建分层次等级的类。

继承就是子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。

### 1.1 继承的基本语法

```java
// 父类（基类）
public class Animal {
    protected String name;
    protected int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void eat() {
        System.out.println(name + "正在吃东西");
    }
    
    public void sleep() {
        System.out.println(name + "正在睡觉");
    }
}

// 子类（派生类）使用 extends 关键字继承
public class Dog extends Animal {
    private String breed;
    
    public Dog(String name, int age, String breed) {
        // 调用父类构造方法
        super(name, age);
        this.breed = breed;
    }
    
    // 子类特有方法
    public void bark() {
        System.out.println(name + "汪汪汪");
    }
}
```

### 1.2 super 关键字

`super` 关键字用于访问父类的成员，包括构造方法、属性和方法。

```java
public class Cat extends Animal {
    public Cat(String name, int age) {
        super(name, age); // 调用父类构造方法，必须在第一行
    }
    
    @Override
    public void eat() {
        super.eat(); // 调用父类的 eat 方法
        System.out.println(name + "喜欢吃鱼");
    }
}
```

### 1.3 继承的特点

- Java 只支持单继承，一个类只能有一个直接父类
- 子类继承父类的所有非私有成员（属性和方法）
- 子类可以扩展自己特有的属性和方法
- 提高代码复用性

---

## 二、方法重写（Override）

方法重写是指子类重新定义父类中已有的方法。

### 2.1 方法重写的规则

- 方法名相同
- 参数列表相同
- 返回值类型相同或为其子类
- 访问修饰符不能比父类更严格

```java
public class Bird extends Animal {
    public Bird(String name, int age) {
        super(name, age);
    }
    
    // 重写父类的 eat 方法
    @Override
    public void eat() {
        System.out.println(name + "正在吃虫子");
    }
    
    // 重写父类的 sleep 方法
    @Override
    public void sleep() {
        System.out.println(name + "在树上睡觉");
    }
    
    // 子类特有方法
    public void fly() {
        System.out.println(name + "正在飞翔");
    }
}
```

### 2.2 @Override 注解

- 用于标识这是一个重写方法
- 编译器会检查是否符合重写规则
- 提高代码可读性

---

## 三、多态

### 3.1 多态的概念

多态是指同一个方法调用，根据对象的实际类型不同，执行不同的实现。

实现方式：**方法重写 + 父类引用指向子类对象**

```java
public class Main {
    public static void main(String[] args) {
        // 父类引用指向子类对象
        Animal animal1 = new Dog("旺财", 3, "金毛");
        Animal animal2 = new Cat("咪咪", 2);
        Animal animal3 = new Bird("小鸟", 1);
        
        // 调用同一个方法，表现出不同行为
        animal1.eat(); // 输出：旺财正在吃东西（Dog 的实现）
        animal2.eat(); // 输出：咪咪正在吃虫子（Cat 的实现）
        animal3.eat(); // 输出：小鸟正在吃虫子（Bird 的实现）
    }
}
```

### 3.2 多态的好处

- 提高代码的可扩展性
- 降低代码耦合度
- 符合开闭原则（对扩展开放，对修改关闭）

---

## 四、类型转换

### 4.1 向上转型（自动转换）

向上转型是自动进行的，子类对象可以直接赋值给父类引用。

```java
Animal animal = new Dog("旺财", 3, "金毛"); // 自动向上转型
```

### 4.2 向下转型（强制转换）

向下转型需要显式进行强制转换。

```java
Animal animal = new Dog("旺财", 3, "金毛");

// 需要强制转换
Dog dog = (Dog) animal;
dog.bark(); // 调用 Dog 特有方法
```

### 4.3 instanceof 关键字

用于判断对象是否为指定类型或其子类。

```java
Animal animal = new Dog("旺财", 3, "金毛");

// 判断对象是否为指定类型
if (animal instanceof Dog) {
    Dog dog = (Dog) animal;
    dog.bark();
} else if (animal instanceof Cat) {
    Cat cat = (Cat) animal;
    // ...
}
```

### 4.4 Java 14+ 模式匹配

```java
if (animal instanceof Dog dog) {
    dog.bark(); // 直接使用，无需强制转换
}
```

---

## 五、final 关键字

`final` 关键字可以用来修饰类、方法和变量。

### 5.1 final 修饰类

```java
// 不能被继承
final public class FinalClass {
    // ...
}
```

### 5.2 final 修饰方法

```java
public class Parent {
    // 不能被子类重写
    final public void method() {
        // ...
    }
}
```

### 5.3 final 修饰变量

```java
public class Example {
    final int MAX_VALUE = 100; // 常量，不能修改
    final String NAME;
    
    public Example() {
        NAME = "固定值"; // 可以在构造方法中赋值一次
    }
}
```

---

## 六、Object 类

### 6.1 Object 是所有类的根类

所有类默认继承 `Object` 类，它是 Java 类层次结构的根。

```java
// 所有类默认继承 Object
public class Person extends Object {
    // ...
}
```

### 6.2 Object 类的常用方法

```java
import java.util.Objects;

public class Person {
    private String name;
    private int age;
    
    // equals 方法：比较两个对象是否相等
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Person person = (Person) obj;
        return age == person.age && Objects.equals(name, person.name);
    }
    
    // hashCode 方法：返回对象的哈希码
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
    
    // toString 方法：返回对象的字符串表示
    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

### 6.3 == 与 equals 的区别

```java
String str1 = "Hello";
String str2 = "Hello";
String str3 = new String("Hello");

// == 比较引用（地址）
System.out.println(str1 == str2);   // true（同一对象）
System.out.println(str1 == str3);   // false（不同对象）

// equals 比较内容
System.out.println(str1.equals(str3)); // true
```

---

## 七、抽象类

在面向对象的概念中，所有的对象都是通过类来描绘的，但是反过来，并不是所有的类都是用来描绘对象的，如果一个类中没有包含足够的信息来描绘一个具体的对象，这样的类就是抽象类。

### 7.1 抽象类的定义

使用 `abstract class` 来定义抽象类。

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
    
    // 抽象方法，没有方法体
    public abstract double computePay();
    
    public void mailCheck() {
        System.out.println("Mailing a check to " + this.name + " " + this.address);
    }
}
```

### 7.2 抽象方法

抽象方法只包含一个方法名，而没有方法体。

```java
public abstract class Shape {
    // 抽象方法，由子类实现
    public abstract double getArea();
    public abstract double getPerimeter();
}
```

### 7.3 继承抽象类

子类必须实现父类的所有抽象方法，否则子类也必须声明为抽象类。

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
        if(newSalary >= 0.0) {
            salary = newSalary;
        }
    }
    
    // 实现抽象方法
    public double computePay() {
        System.out.println("Computing salary pay for " + getName());
        return salary / 52;
    }
}
```

### 7.4 抽象类的特点

- 抽象类不能被实例化
- 抽象类中不一定包含抽象方法，但有抽象方法的类必定是抽象类
- 抽象方法没有方法体
- 构造方法和静态方法不能声明为抽象方法
- 子类必须实现抽象类中的所有抽象方法

---

## 八、接口

接口（Interface）是一个抽象类型，是抽象方法的集合，接口通常以 `interface` 来声明。

### 8.1 接口与类的区别

| 特性 | 接口 | 类 |
|------|------|------|
| 实例化 | 不能实例化 | 可以实例化 |
| 构造方法 | 没有 | 有 |
| 方法 | 默认是 `public abstract` | 可以有各种修饰符 |
| 成员变量 | 默认是 `public static final` | 可以有各种类型 |
| 继承 | 支持多继承 | 只支持单继承 |

### 8.2 接口的声明

```java
public interface Animal {
    public void eat();
    public void travel();
}
```

### 8.3 接口的实现

使用 `implements` 关键字实现接口。

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

运行结果：

```
Mammal eats
Mammal travels
```

### 8.4 接口的继承

接口支持多继承。

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

### 8.5 标记接口

标记接口是没有任何方法和属性的接口，用于标识某个类属于一个特定的类型。

```java
public interface EventListener {
    // 空接口，作为标记
}
```

---

## 九、抽象类和接口的区别

| 特性 | 抽象类 | 接口 |
|------|--------|------|
| 方法实现 | 可以有方法体 | 不能有方法体（Java 8 后可有 default 方法） |
| 成员变量 | 可以有各种类型 | 只能是 `public static final` |
| 静态方法 | 可以有 | Java 8 后可以有 |
| 继承 | 单继承 | 多继承 |
| 设计目的 | 为子类提供通用模板 | 定义行为规范 |

---

## 十、练习

1. 创建一个 `Shape` 抽象类，包含计算面积的抽象方法，然后创建 `Circle`、`Rectangle`、`Triangle` 子类继承并实现具体的面积计算
2. 创建一个 `Employee` 抽象类，包含姓名、工号属性和工作方法，然后创建 `Manager`、`Developer`、`Tester` 子类
3. 定义一个 `Flyable` 接口，包含 `fly()` 方法，让 `Bird`、`Plane` 类实现该接口
4. 使用多态实现动物叫声模拟器
5. 重写 `equals`、`hashCode` 和 `toString` 方法
6. 使用 instanceof 进行类型判断和转换