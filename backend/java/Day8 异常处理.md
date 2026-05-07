# Day8 异常处理

## 一、异常的概念

异常是程序运行时发生的不正常情况，破坏了正常的执行流程。Java 使用异常处理机制来处理这些情况。

### 1.1 异常分类

Java 中的异常主要分为三类：

- **检查性异常（Checked Exception）：** 最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。

- **运行时异常（RuntimeException）：** 运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。

- **错误（Error）：** 错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到。

### 1.2 Exception 类的层次

所有的异常类是从 java.lang.Exception 类继承的子类。

Exception 类是 Throwable 类的子类。除了 Exception 类外，Throwable 还有一个子类 Error。

Java 程序通常不捕获错误。错误一般发生在严重故障时，它们在 Java 程序处理的范畴之外。

Error 用来指示运行时环境发生的错误。例如，JVM 内存溢出。一般地，程序不会从错误中恢复。

异常类有两个主要的子类：IOException 类和 RuntimeException 类。

---

## 二、Java 内置异常类

### 2.1 非检查性异常（运行时异常）

| 异常 | 描述 |
| --- | --- |
| ArithmeticException | 当出现异常的运算条件时，抛出此异常。例如，一个整数"除以零"时 |
| ArrayIndexOutOfBoundsException | 用非法索引访问数组时抛出的异常 |
| ClassCastException | 当试图将对象强制转换为不是实例的子类时，抛出该异常 |
| IllegalArgumentException | 抛出的异常表明向方法传递了一个不合法或不正确的参数 |
| NullPointerException | 当应用程序试图在需要对象的地方使用 null 时，抛出该异常 |
| NumberFormatException | 当应用程序试图将字符串转换成一种数值类型，但该字符串不能转换为适当格式时 |
| StringIndexOutOfBoundsException | 此异常由 String 方法抛出，指示索引或者为负，或者超出字符串的大小 |

### 2.2 检查性异常

| 异常 | 描述 |
| --- | --- |
| ClassNotFoundException | 应用程序试图加载类时，找不到相应的类，抛出该异常 |
| IllegalAccessException | 拒绝访问一个类的时候，抛出该异常 |
| InterruptedException | 一个线程被另一个线程中断，抛出该异常 |
| IOException | I/O 操作失败或中断时抛出 |
| SQLException | 数据库访问错误时抛出 |

---

## 三、捕获异常

使用 try 和 catch 关键字可以捕获异常。try/catch 代码块放在异常可能发生的地方。

### 3.1 try-catch 基本语法

```java
try {
   // 程序代码
} catch (ExceptionName e) {
   // Catch 块
}
```

### 3.2 异常捕获示例

**ExcepTest.java 文件代码：**

```java
import java.io.*;

public class ExcepTest {
    public static void main(String args[]) {
        try {
            int a[] = new int[2];
            System.out.println("Access element three: " + a[3]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Exception thrown: " + e);
        }
        System.out.println("Out of the block");
    }
}
```

输出结果：

```
Exception thrown: java.lang.ArrayIndexOutOfBoundsException: 3
Out of the block
```

### 3.3 多重捕获块

一个 try 代码块后面跟随多个 catch 代码块的情况就叫多重捕获。

```java
try {
    file = new FileInputStream(fileName);
    x = (byte) file.read();
} catch (FileNotFoundException f) {
    f.printStackTrace();
    return -1;
} catch (IOException i) {
    i.printStackTrace();
    return -1;
}
```

### 3.4 多异常合并捕获（Java 7+）

从 Java 7 开始，可以用一个 catch 块处理多个无继承关系的异常。

```java
try {
    // 同时可能抛出 SQL 和 IO 异常
    doSomething();
} catch (SQLException | IOException e) {
    System.out.println("发生了 SQL 或 IO 异常！");
    e.printStackTrace();
}
```

**注意：** 异常类型之间不能有继承关系，否则会导致编译错误。

---

## 四、throws/throw 关键字

### 4.1 throw 关键字

throw 关键字用于在当前方法中抛出一个异常。

```java
public void checkNumber(int num) {
    if (num < 0) {
        throw new IllegalArgumentException("Number must be positive");
    }
}
```

### 4.2 throws 关键字

throws 关键字用于在方法声明中指定该方法可能抛出的异常。

```java
public void readFile(String filePath) throws IOException {
    BufferedReader reader = new BufferedReader(new FileReader(filePath));
    String line = reader.readLine();
    while (line != null) {
        System.out.println(line);
        line = reader.readLine();
    }
    reader.close();
}
```

一个方法可以声明抛出多个异常，多个异常之间用逗号隔开：

```java
public void withdraw(double amount) throws RemoteException, InsufficientFundsException {
    // ...
}
```

---

## 五、finally 关键字

finally 关键字用来创建在 try 代码块后面执行的代码块。无论是否发生异常，finally 代码块中的代码总会被执行。

```java
try {
    // 程序代码
} catch (异常类型 异常变量) {
    // 异常处理
} finally {
    // 无论是否发生异常，都会执行
}
```

**ExcepTest.java 文件代码：**

```java
public class ExcepTest {
    public static void main(String args[]) {
        int a[] = new int[2];
        try {
            System.out.println("Access element three: " + a[3]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Exception thrown: " + e);
        } finally {
            a[0] = 6;
            System.out.println("First element value: " + a[0]);
            System.out.println("The finally statement is executed");
        }
    }
}
```

输出结果：

```
Exception thrown: java.lang.ArrayIndexOutOfBoundsException: 3
First element value: 6
The finally statement is executed
```

**注意事项：**
- catch 不能独立于 try 存在
- 在 try/catch 后面添加 finally 块并非强制性要求
- try 代码后不能既没 catch 块也没 finally 块
- try, catch, finally 块之间不能添加任何代码

---

## 六、try-with-resources

JDK 7 之后，Java 新增了 try-with-resources 语法结构，能够自动关闭在 try 块中声明的资源。

```java
try (resource declaration) {
    // 使用的资源
} catch (ExceptionType e) {
    // 异常块
}
```

**注意：** try-with-resources 语句关闭所有实现 AutoCloseable 接口的资源。

**RunoobTest.java 文件代码：**

```java
import java.io.*;

public class RunoobTest {
    public static void main(String[] args) {
        String line;
        try (BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
            while ((line = br.readLine()) != null) {
                System.out.println("Line => " + line);
            }
        } catch (IOException e) {
            System.out.println("IOException in try block => " + e.getMessage());
        }
    }
}
```

### 6.1 处理多个资源

try-with-resources 语句中可以声明多个资源，使用分号分隔：

```java
import java.io.*;
import java.util.*;

class RunoobTest {
    public static void main(String[] args) throws IOException {
        try (Scanner scanner = new Scanner(new File("testRead.txt"));
             PrintWriter writer = new PrintWriter(new File("testWrite.txt"))) {
            while (scanner.hasNext()) {
                writer.print(scanner.nextLine());
            }
        }
    }
}
```

多个声明资源时，try-with-resources 语句以相反的顺序关闭这些资源。

---

## 七、声明自定义异常

在 Java 中可以自定义异常。编写自己的异常类时需要记住以下几点：

- 所有异常都必须是 Throwable 的子类
- 如果希望写一个检查性异常类，则需要继承 Exception 类
- 如果想写一个运行时异常类，那么需要继承 RuntimeException 类

### 7.1 自定义异常类

```java
class MyException extends Exception {
    public MyException(String message) {
        super(message);
    }
}
```

### 7.2 自定义异常示例

**InsufficientFundsException.java 文件代码：**

```java
import java.io.*;

public class InsufficientFundsException extends Exception {
    private double amount;
    
    public InsufficientFundsException(double amount) {
        this.amount = amount;
    }
    
    public double getAmount() {
        return amount;
    }
}
```

**CheckingAccount.java 文件代码：**

```java
import java.io.*;

public class CheckingAccount {
    private double balance;
    private int number;
    
    public CheckingAccount(int number) {
        this.number = number;
    }
    
    public void deposit(double amount) {
        balance += amount;
    }
    
    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount <= balance) {
            balance -= amount;
        } else {
            double needs = amount - balance;
            throw new InsufficientFundsException(needs);
        }
    }
    
    public double getBalance() {
        return balance;
    }
    
    public int getNumber() {
        return number;
    }
}
```

**BankDemo.java 文件代码：**

```java
public class BankDemo {
    public static void main(String[] args) {
        CheckingAccount c = new CheckingAccount(101);
        System.out.println("Depositing $500...");
        c.deposit(500.00);
        
        try {
            System.out.println("\nWithdrawing $100...");
            c.withdraw(100.00);
            System.out.println("\nWithdrawing $600...");
            c.withdraw(600.00);
        } catch (InsufficientFundsException e) {
            System.out.println("Sorry, but you are short $" + e.getAmount());
            e.printStackTrace();
        }
    }
}
```

输出结果：

```
Depositing $500...

Withdrawing $100...

Withdrawing $600...
Sorry, but you are short $200.0
InsufficientFundsException
        at CheckingAccount.withdraw(CheckingAccount.java:25)
        at BankDemo.main(BankDemo.java:13)
```

---

## 八、异常处理最佳实践

- 在合适的位置捕获异常，并对异常进行适当的处理，以确保程序的稳定性和可靠性
- 避免过度捕获异常，应该尽量精确捕获特定类型的异常
- 使用 finally 块或 try-with-resources 来释放资源
- 优先处理受检异常，避免将受检异常转换为非受检异常
- 提供有意义的错误信息，不要吞掉异常

---

## 九、练习

1. 编写程序，捕获数组越界异常和空指针异常
2. 创建一个自定义异常 `InsufficientFundsException`，模拟银行取款时余额不足的情况
3. 使用 try-with-resources 读取文件内容
4. 编写一个方法，声明抛出多个异常，然后在调用处处理
5. 编写一个计算器程序，处理除零异常和非法参数异常