# Day6 继承与多态

## 一、Java 继承

继承是 Java 面向对象编程技术的一块基石，它允许创建分等级层次的类。子类继承父类的特征和行为，使得子类对象具有父类的实例域和方法。

### 1.1 类的继承格式

在 Java 中通过 `extends` 关键字可以声明一个类是从另一个类继承而来的：

```java
class 父类 { }
class 子类 extends 父类 { }
```

### 1.2 为什么需要继承

通过继承可以消除重复代码，提高代码复用性。例如：

**公共父类 Animal：**

```java
public class Animal {
    private String name;
    private int id;
    
    public Animal(String myName, int myid) {
        name = myName;
        id = myid;
    }
    
    public void eat() {
        System.out.println(name + "正在吃");
    }
    
    public void sleep() {
        System.out.println(name + "正在睡");
    }
    
    public void introduction() {
        System.out.println("大家好！我是" + id + "号" + name + ".");
    }
}
```

**子类 Penguin：**

```java
public class Penguin extends Animal {
    public Penguin(String myName, int myid) {
        super(myName, myid);
    }
}
```

**子类 Mouse：**

```java
public class Mouse extends Animal {
    public Mouse(String myName, int myid) {
        super(myName, myid);
    }
}
```

### 1.3 继承的特性

- 子类拥有父类非 private 的属性、方法
- 子类可以拥有自己的属性和方法，对父类进行扩展
- 子类可以用自己的方式实现父类的方法
- Java 的继承是单继承，但支持多重继承
- 提高了类之间的耦合性（这也是继承的缺点）

### 1.4 super 与 this 关键字

**super 关键字：** 引用当前对象的父类成员

**this 关键字：** 引用当前对象自身

```java
class Animal {
    void eat() {
        System.out.println("animal: eat");
    }
}

class Dog extends Animal {
    void eat() {
        System.out.println("dog: eat");
    }
    
    void eatTest() {
        this.eat();   // 调用自己的 eat 方法
        super.eat();  // 调用父类的 eat 方法
    }
}

public class Test {
    public static void main(String[] args) {
        Animal a = new Animal();
        a.eat();
        
        Dog d = new Dog();
        d.eatTest();
    }
}
```

输出结果：

```
animal: eat
dog: eat
animal: eat
```

### 1.5 final 关键字

final 可以用来修饰类、方法和变量：

```java
// final 类：不能被继承
final class FinalClass { }

// final 方法：不能被子类重写
class Parent {
    final public void method() { }
}

// final 变量：常量，不能修改
class Example {
    final int MAX_VALUE = 100;
}
```

### 1.6 构造器的调用

子类不继承父类的构造器，但可以通过 `super` 调用：

```java
class SuperClass {
    public SuperClass() {
        System.out.println("SuperClass()");
    }
    
    public SuperClass(int n) {
        System.out.println("SuperClass(int n)");
    }
}

class SubClass extends SuperClass {
    public SubClass() {
        super(); // 调用父类无参构造器
        System.out.println("SubClass()");
    }
    
    public SubClass(int n) {
        super(300); // 调用父类有参构造器
        System.out.println("SubClass(int n): " + n);
    }
}
```

---

## 二、重写(Override)与重载(Overload)

### 2.1 重写(Override)

重写是子类定义了一个与其父类具有相同名称、参数列表和返回类型的方法。

```java
class Animal {
    public void move() {
        System.out.println("动物可以移动");
    }
}

class Dog extends Animal {
    public void move() {
        System.out.println("狗可以跑和走");
    }
}

public class TestDog {
    public static void main(String args[]) {
        Animal a = new Animal();
        Animal b = new Dog();
        
        a.move(); // 调用 Animal 类的方法
        b.move(); // 调用 Dog 类的方法
    }
}
```

输出结果：

```
动物可以移动
狗可以跑和走
```

### 2.2 方法重写规则

- 参数列表必须完全相同
- 返回类型必须相同（Java 7+ 可以是父类返回值的派生类）
- 访问权限不能比父类更低
- final 方法不能被重写
- 静态方法不能被重写，但可以被再次声明

### 2.3 使用 super 调用父类方法

```java
class Animal {
    public void move() {
        System.out.println("动物可以移动");
    }
}

class Dog extends Animal {
    public void move() {
        super.move(); // 调用父类方法
        System.out.println("狗可以跑和走");
    }
}
```

### 2.4 重载(Overload)

重载是在一个类里面，方法名字相同，参数不同：

```java
public class Overloading {
    public int test() {
        System.out.println("test1");
        return 1;
    }
    
    public void test(int a) {
        System.out.println("test2");
    }
    
    public String test(int a, String s) {
        System.out.println("test3");
        return "returntest3";
    }
    
    public String test(String s, int a) {
        System.out.println("test4");
        return "returntest4";
    }
}
```

### 2.5 重写与重载的区别

| 区别点 | 重载方法 | 重写方法 |
| --- | --- | --- |
| 参数列表 | 必须修改 | 一定不能修改 |
| 返回类型 | 可以修改 | 一定不能修改 |
| 异常 | 可以修改 | 可以减少或删除，不能抛出新的或更广的异常 |
| 访问 | 可以修改 | 不能做更严格的限制 |

---

## 三、Java 多态

多态是同一个行为具有多个不同表现形式或形态的能力。

### 3.1 多态存在的三个必要条件

1. **继承**
2. **重写**
3. **父类引用指向子类对象**

### 3.2 多态示例

```java
abstract class Animal {
    abstract void eat();
}

class Cat extends Animal {
    public void eat() {
        System.out.println("吃鱼");
    }
    
    public void work() {
        System.out.println("抓老鼠");
    }
}

class Dog extends Animal {
    public void eat() {
        System.out.println("吃骨头");
    }
    
    public void work() {
        System.out.println("看家");
    }
}

public class Test {
    public static void main(String[] args) {
        show(new Cat());
        show(new Dog());
        
        Animal a = new Cat();
        a.eat();
        Cat c = (Cat) a;
        c.work();
    }
    
    public static void show(Animal a) {
        a.eat();
        if (a instanceof Cat) {
            Cat c = (Cat) a;
            c.work();
        } else if (a instanceof Dog) {
            Dog c = (Dog) a;
            c.work();
        }
    }
}
```

输出结果：

```
吃鱼
抓老鼠
吃骨头
看家
吃鱼
抓老鼠
```

### 3.3 多态的优点

- 消除类型之间的耦合关系
- 可替换性
- 可扩充性
- 接口性
- 灵活性
- 简化性

### 3.4 类型转换

**向上转型（自动）：**

```java
Animal animal = new Dog("旺财", 3); // 自动向上转型
```

**向下转型（强制）：**

```java
Animal animal = new Dog("旺财", 3);
Dog dog = (Dog) animal; // 需要强制转换
```

**instanceof 关键字：**

```java
if (animal instanceof Dog) {
    Dog dog = (Dog) animal;
    dog.work();
}
```

---

## 四、Object 类

Object 是所有类的根类，所有类默认继承 Object。

### 4.1 Object 类的常用方法

**equals 方法：** 比较两个对象是否相等

```java
@Override
public boolean equals(Object obj) {
    if (this == obj) return true;
    if (obj == null || getClass() != obj.getClass()) return false;
    Person person = (Person) obj;
    return age == person.age && Objects.equals(name, person.name);
}
```

**hashCode 方法：** 返回对象的哈希码

```java
@Override
public int hashCode() {
    return Objects.hash(name, age);
}
```

**toString 方法：** 返回对象的字符串表示

```java
@Override
public String toString() {
    return "Person{" + "name='" + name + '\'' + ", age=" + age + '}';
}
```

### 4.2 == 与 equals 的区别

```java
String str1 = "Hello";
String str2 = "Hello";
String str3 = new String("Hello");

System.out.println(str1 == str2);        // true（同一对象）
System.out.println(str1 == str3);        // false（不同对象）
System.out.println(str1.equals(str3));   // true（内容相同）
```

---

## 五、练习

1. 创建一个 `Shape` 父类，包含计算面积的方法，然后创建 `Circle`、`Rectangle`、`Triangle` 子类继承并实现具体的面积计算
2. 创建一个 `Employee` 父类，包含姓名、工号属性和工作方法，然后创建 `Manager`、`Developer`、`Tester` 子类
3. 使用多态实现动物叫声模拟器
4. 重写 `equals`、`hashCode` 和 `toString` 方法
5. 使用 instanceof 进行类型判断和转换