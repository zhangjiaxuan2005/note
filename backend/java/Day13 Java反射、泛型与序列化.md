# Day13 Java反射、泛型与序列化

## 一、Java 反射（Reflection）

### 1.1 反射概述

**反射**是 Java 的一个强大特性，允许程序在运行时查询、访问和修改类、接口、字段和方法的信息。

**反射的主要用途：**
- 运行时分析类的能力
- 运行时查看对象
- 实现通用的数组操作代码
- 利用 Method 对象

**核心类：**
- `java.lang.Class` - 表示类的对象
- `java.lang.reflect.Field` - 表示类的字段
- `java.lang.reflect.Method` - 表示类的方法
- `java.lang.reflect.Constructor` - 表示类的构造方法

### 1.2 获取 Class 对象

有三种方式获取 Class 对象：

```java
// 方式1：通过类名.class
Class<?> clazz1 = String.class;

// 方式2：通过对象.getClass()
String str = "Hello";
Class<?> clazz2 = str.getClass();

// 方式3：通过 Class.forName()
Class<?> clazz3 = Class.forName("java.lang.String");
```

### 1.3 获取类信息

```java
import java.lang.reflect.*;

public class ClassInfoDemo {
    public static void main(String[] args) throws Exception {
        Class<?> clazz = String.class;
        
        // 获取类名
        System.out.println("类名: " + clazz.getName());           // java.lang.String
        System.out.println("简单名: " + clazz.getSimpleName());   // String
        
        // 获取父类
        Class<?> superClass = clazz.getSuperclass();
        System.out.println("父类: " + superClass.getName());      // java.lang.Object
        
        // 获取实现的接口
        Class<?>[] interfaces = clazz.getInterfaces();
        for (Class<?> i : interfaces) {
            System.out.println("接口: " + i.getName());
        }
        
        // 获取所有公共方法
        Method[] methods = clazz.getMethods();
        for (Method m : methods) {
            System.out.println("方法: " + m.getName());
        }
        
        // 获取所有公共字段
        Field[] fields = clazz.getFields();
        
        // 获取所有公共构造方法
        Constructor<?>[] constructors = clazz.getConstructors();
    }
}
```

### 1.4 创建对象

```java
public class ReflectionNewInstance {
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Class.forName("java.util.ArrayList");
        
        // 方式1：使用无参构造方法
        Object obj1 = clazz.getDeclaredConstructor().newInstance();
        
        // 方式2：使用有参构造方法
        Class<?> stringClass = Class.forName("java.lang.String");
        Constructor<?> constructor = stringClass.getConstructor(String.class);
        Object obj2 = constructor.newInstance("Hello");
    }
}
```

### 1.5 访问和修改字段

```java
import java.lang.reflect.Field;

class Person {
    private String name;
    public int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

public class FieldAccessDemo {
    public static void main(String[] args) throws Exception {
        Person person = new Person("张三", 25);
        Class<?> clazz = person.getClass();
        
        // 访问公共字段
        Field ageField = clazz.getField("age");
        System.out.println("年龄: " + ageField.get(person));  // 25
        
        // 修改公共字段
        ageField.set(person, 30);
        System.out.println("修改后年龄: " + person.age);  // 30
        
        // 访问私有字段
        Field nameField = clazz.getDeclaredField("name");
        nameField.setAccessible(true);  // 设置可访问
        System.out.println("姓名: " + nameField.get(person));  // 张三
        
        // 修改私有字段
        nameField.set(person, "李四");
        System.out.println("修改后姓名: " + nameField.get(person));  // 李四
    }
}
```

### 1.6 调用方法

```java
import java.lang.reflect.Method;

public class MethodInvokeDemo {
    public static void main(String[] args) throws Exception {
        String str = "Hello World";
        Class<?> clazz = str.getClass();
        
        // 调用无参方法
        Method lengthMethod = clazz.getMethod("length");
        int length = (int) lengthMethod.invoke(str);
        System.out.println("长度: " + length);  // 11
        
        // 调用有参方法
        Method substringMethod = clazz.getMethod("substring", int.class, int.class);
        String result = (String) substringMethod.invoke(str, 0, 5);
        System.out.println("子串: " + result);  // Hello
        
        // 调用静态方法
        Method valueOfMethod = clazz.getMethod("valueOf", int.class);
        String numStr = (String) valueOfMethod.invoke(null, 123);
        System.out.println("字符串: " + numStr);  // 123
    }
}
```

### 1.7 反射应用示例

```java
import java.lang.reflect.*;
import java.util.*;

// 通用对象打印工具
public class ObjectAnalyzer {
    
    public static String toString(Object obj) throws Exception {
        if (obj == null) return "null";
        
        Class<?> clazz = obj.getClass();
        StringBuilder sb = new StringBuilder(clazz.getName());
        sb.append("[");
        
        // 获取所有字段
        Field[] fields = clazz.getDeclaredFields();
        for (int i = 0; i < fields.length; i++) {
            Field f = fields[i];
            f.setAccessible(true);
            
            sb.append(f.getName()).append("=");
            sb.append(f.get(obj));
            
            if (i < fields.length - 1) {
                sb.append(", ");
            }
        }
        sb.append("]");
        return sb.toString();
    }
    
    public static void main(String[] args) throws Exception {
        ArrayList<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        
        System.out.println(toString(list));
    }
}
```

---

## 二、Java 泛型

### 2.1 泛型概述

**泛型**是 JDK 5 引入的特性，提供了编译时类型安全检测机制。

**泛型的优点：**
- 类型安全：编译时检查类型错误
- 消除强制类型转换
- 提高代码重用性

**常用类型参数：**
- `E` - Element（元素）
- `T` - Type（类型）
- `K` - Key（键）
- `V` - Value（值）
- `N` - Number（数值）
- `?` - 通配符

### 2.2 泛型类

```java
// 定义泛型类
public class Box<T> {
    private T content;
    
    public void setContent(T content) {
        this.content = content;
    }
    
    public T getContent() {
        return content;
    }
    
    public static void main(String[] args) {
        // 创建Integer类型的Box
        Box<Integer> intBox = new Box<>();
        intBox.setContent(100);
        Integer value = intBox.getContent();
        
        // 创建String类型的Box
        Box<String> strBox = new Box<>();
        strBox.setContent("Hello");
        String str = strBox.getContent();
    }
}
```

### 2.3 泛型方法

```java
public class GenericMethodDemo {
    
    // 泛型方法
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }
    
    // 泛型方法返回泛型类型
    public static <T> T getFirst(T[] array) {
        return array.length > 0 ? array[0] : null;
    }
    
    // 有界类型参数
    public static <T extends Comparable<T>> T max(T a, T b) {
        return a.compareTo(b) > 0 ? a : b;
    }
    
    public static void main(String[] args) {
        Integer[] intArray = {1, 2, 3, 4, 5};
        String[] strArray = {"A", "B", "C"};
        
        printArray(intArray);  // 1 2 3 4 5
        printArray(strArray);  // A B C
        
        System.out.println(max(10, 20));      // 20
        System.out.println(max("A", "B"));    // B
    }
}
```

### 2.4 有界类型参数

```java
// 上界：T必须是Number或其子类
public class NumberBox<T extends Number> {
    private T number;
    
    public NumberBox(T number) {
        this.number = number;
    }
    
    public double doubleValue() {
        return number.doubleValue();
    }
    
    public static void main(String[] args) {
        NumberBox<Integer> intBox = new NumberBox<>(100);
        NumberBox<Double> doubleBox = new NumberBox<>(3.14);
        
        System.out.println(intBox.doubleValue());    // 100.0
        System.out.println(doubleBox.doubleValue()); // 3.14
        
        // NumberBox<String> strBox = new NumberBox<>("hello"); // 编译错误
    }
}
```

### 2.5 通配符

```java
import java.util.*;

public class WildcardDemo {
    
    // 无界通配符：接受任意类型
    public static void printList(List<?> list) {
        for (Object obj : list) {
            System.out.println(obj);
        }
    }
    
    // 上界通配符：接受Number及其子类
    public static double sum(List<? extends Number> list) {
        double total = 0;
        for (Number n : list) {
            total += n.doubleValue();
        }
        return total;
    }
    
    // 下界通配符：接受Integer及其父类
    public static void addNumbers(List<? super Integer> list) {
        for (int i = 1; i <= 10; i++) {
            list.add(i);
        }
    }
    
    public static void main(String[] args) {
        List<Integer> intList = Arrays.asList(1, 2, 3);
        List<Double> doubleList = Arrays.asList(1.1, 2.2, 3.3);
        List<String> strList = Arrays.asList("A", "B", "C");
        
        printList(intList);
        printList(strList);
        
        System.out.println(sum(intList));     // 6.0
        System.out.println(sum(doubleList));  // 6.6
        
        List<Number> numList = new ArrayList<>();
        addNumbers(numList);
        System.out.println(numList);  // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    }
}
```

### 2.6 泛型接口

```java
// 定义泛型接口
interface Comparable<T> {
    int compareTo(T o);
}

// 实现泛型接口
class Student implements Comparable<Student> {
    private String name;
    private int score;
    
    public Student(String name, int score) {
        this.name = name;
        this.score = score;
    }
    
    @Override
    public int compareTo(Student other) {
        return this.score - other.score;
    }
    
    @Override
    public String toString() {
        return name + ": " + score;
    }
}
```

### 2.7 类型擦除

Java 泛型使用**类型擦除**实现，编译时会擦除类型参数，替换为它们的上界（通常是 Object）。

```java
// 编译前
List<String> strList = new ArrayList<>();
strList.add("Hello");
String s = strList.get(0);

// 编译后（类型擦除）
List strList = new ArrayList();
strList.add("Hello");
String s = (String) strList.get(0);  // 强制类型转换
```

---

## 三、Java 序列化

### 3.1 序列化概述

**序列化**：将对象转换为字节流，便于存储或传输  
**反序列化**：将字节流恢复为对象

**实现序列化的条件：**
1. 实现 `java.io.Serializable` 接口（标记接口）
2. 所有属性必须是可序列化的

### 3.2 序列化对象

```java
import java.io.*;

// 实现 Serializable 接口
class Employee implements Serializable {
    private static final long serialVersionUID = 1L;
    
    public String name;
    public String address;
    public transient int SSN;  // transient：不序列化此字段
    public int number;
    
    public void mailCheck() {
        System.out.println("Mailing a check to " + name + " " + address);
    }
}

public class SerializeDemo {
    public static void main(String[] args) {
        Employee e = new Employee();
        e.name = "张三";
        e.address = "北京市";
        e.SSN = 11122333;
        e.number = 101;
        
        try {
            // 创建输出流
            FileOutputStream fileOut = new FileOutputStream("employee.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);
            
            // 写入对象
            out.writeObject(e);
            
            // 关闭流
            out.close();
            fileOut.close();
            
            System.out.println("序列化数据已保存到 employee.ser");
        } catch (IOException i) {
            i.printStackTrace();
        }
    }
}
```

### 3.3 反序列化对象

```java
import java.io.*;

public class DeserializeDemo {
    public static void main(String[] args) {
        Employee e = null;
        
        try {
            // 创建输入流
            FileInputStream fileIn = new FileInputStream("employee.ser");
            ObjectInputStream in = new ObjectInputStream(fileIn);
            
            // 读取对象
            e = (Employee) in.readObject();
            
            // 关闭流
            in.close();
            fileIn.close();
        } catch (IOException i) {
            i.printStackTrace();
            return;
        } catch (ClassNotFoundException c) {
            System.out.println("Employee 类未找到");
            c.printStackTrace();
            return;
        }
        
        System.out.println("反序列化 Employee...");
        System.out.println("姓名: " + e.name);
        System.out.println("地址: " + e.address);
        System.out.println("SSN: " + e.SSN);  // 0，因为transient
        System.out.println("编号: " + e.number);
    }
}
```

### 3.4 serialVersionUID

`serialVersionUID` 是序列化版本号，用于验证序列化和反序列化的类是否兼容。

```java
class User implements Serializable {
    // 显式声明 serialVersionUID
    private static final long serialVersionUID = 1L;
    
    private String name;
    private int age;
    
    // 如果类结构改变，但 serialVersionUID 不变，仍可反序列化
    // 如果 serialVersionUID 改变，会抛出 InvalidClassException
}
```

### 3.5 自定义序列化

```java
import java.io.*;

class Person implements Serializable {
    private String name;
    private transient String password;  // 敏感信息不序列化
    
    public Person(String name, String password) {
        this.name = name;
        this.password = password;
    }
    
    // 自定义序列化
    private void writeObject(ObjectOutputStream out) throws IOException {
        out.defaultWriteObject();  // 序列化非transient字段
        // 对密码进行加密后序列化
        out.writeObject(encrypt(password));
    }
    
    // 自定义反序列化
    private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
        in.defaultReadObject();  // 反序列化非transient字段
        // 解密密码
        password = decrypt((String) in.readObject());
    }
    
    private String encrypt(String str) {
        // 简单加密示例
        return "encrypted_" + str;
    }
    
    private String decrypt(String str) {
        return str.replace("encrypted_", "");
    }
}
```

### 3.6 序列化注意事项

1. **静态变量**不会被序列化
2. **transient** 修饰的字段不会被序列化
3. 父类没有实现 Serializable，子类需要额外处理
4. 序列化不保存对象引用关系，会重新创建对象

---

## 四、练习题目

### 题目1：反射获取类信息
编写程序，使用反射获取 String 类的所有方法，并统计以 "get" 开头的方法数量。

<details>
<summary>点击查看答案</summary>

```java
import java.lang.reflect.Method;

public class ReflectionExercise {
    public static void main(String[] args) {
        Class<?> clazz = String.class;
        Method[] methods = clazz.getMethods();
        
        int count = 0;
        for (Method m : methods) {
            if (m.getName().startsWith("get")) {
                count++;
                System.out.println(m.getName());
            }
        }
        System.out.println("以 'get' 开头的方法数量: " + count);
    }
}
```
</details>

### 题目2：泛型工具类
编写一个泛型工具类，实现两个任意类型对象的交换。

<details>
<summary>点击查看答案</summary>

```java
public class GenericSwap {
    
    public static <T> void swap(T[] array, int i, int j) {
        if (array == null || i < 0 || j < 0 || 
            i >= array.length || j >= array.length) {
            return;
        }
        T temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
    
    public static void main(String[] args) {
        Integer[] intArray = {1, 2, 3, 4, 5};
        swap(intArray, 0, 4);
        for (Integer n : intArray) {
            System.out.print(n + " ");  // 5 2 3 4 1
        }
        
        String[] strArray = {"A", "B", "C"};
        swap(strArray, 0, 2);
        for (String s : strArray) {
            System.out.print(s + " ");  // C B A
        }
    }
}
```
</details>

### 题目3：序列化练习
创建一个 Student 类，包含姓名、年龄和成绩，实现序列化和反序列化。

<details>
<summary>点击查看答案</summary>

```java
import java.io.*;

class Student implements Serializable {
    private static final long serialVersionUID = 1L;
    
    private String name;
    private int age;
    private double score;
    
    public Student(String name, int age, double score) {
        this.name = name;
        this.age = age;
        this.score = score;
    }
    
    @Override
    public String toString() {
        return "Student{name='" + name + "', age=" + age + ", score=" + score + "}";
    }
}

public class SerializationExercise {
    public static void main(String[] args) throws Exception {
        Student student = new Student("张三", 20, 85.5);
        String filename = "student.ser";
        
        // 序列化
        try (ObjectOutputStream oos = new ObjectOutputStream(
                new FileOutputStream(filename))) {
            oos.writeObject(student);
            System.out.println("序列化: " + student);
        }
        
        // 反序列化
        try (ObjectInputStream ois = new ObjectInputStream(
                new FileInputStream(filename))) {
            Student restored = (Student) ois.readObject();
            System.out.println("反序列化: " + restored);
        }
    }
}
```
</details>

---

## 五、总结

| 知识点 | 核心内容 |
|--------|----------|
| 反射 | Class对象获取、字段访问、方法调用、对象创建 |
| 泛型 | 泛型类、泛型方法、通配符、有界类型 |
| 序列化 | Serializable接口、transient、serialVersionUID |

**重点掌握：**
1. 反射的基本使用：获取Class对象、访问字段、调用方法
2. 泛型的类型参数、通配符的使用场景
3. 序列化的实现方式和注意事项
4. 理解类型擦除机制
