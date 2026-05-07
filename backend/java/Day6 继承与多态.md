# Day6 继承与多态

## 一、继承的概念

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

## 二、方法重写（Override）

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

## 三、多态

### 3.1 多态的概念
- 同一个方法调用，根据对象的实际类型不同，执行不同的实现
- 实现方式：方法重写 + 父类引用指向子类对象

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
- 符合开闭原则

## 四、类型转换

### 4.1 向上转型（自动转换）

```java
Animal animal = new Dog("旺财", 3, "金毛"); // 自动向上转型
```

### 4.2 向下转型（强制转换）

```java
Animal animal = new Dog("旺财", 3, "金毛");

// 需要强制转换
Dog dog = (Dog) animal;
dog.bark(); // 调用 Dog 特有方法
```

### 4.3 instanceof 关键字

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

## 五、final 关键字

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

## 六、Object 类

### 6.1 Object 是所有类的根类

```java
// 所有类默认继承 Object
public class Person extends Object {
    // ...
}
```

### 6.2 Object 类的常用方法

```java
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

## 七、练习

1. 创建一个 `Shape` 父类，包含计算面积的方法，然后创建 `Circle`、`Rectangle`、`Triangle` 子类继承并实现具体的面积计算
2. 创建一个 `Employee` 父类，包含姓名、工号属性和工作方法，然后创建 `Manager`、`Developer`、`Tester` 子类
3. 使用多态实现动物叫声模拟器
4. 重写 `equals`、`hashCode` 和 `toString` 方法
5. 使用 instanceof 进行类型判断和转换