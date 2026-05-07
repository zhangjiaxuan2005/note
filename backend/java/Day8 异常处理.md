# Day8 异常处理

## 一、异常的概念

### 1.1 什么是异常
- 程序运行时发生的不正常情况
- 破坏了正常的执行流程
- Java 使用异常处理机制来处理这些情况

### 1.2 异常分类

```
Throwable
├── Error（错误）
│   ├── OutOfMemoryError
│   ├── StackOverflowError
│   └── VirtualMachineError
└── Exception（异常）
    ├── RuntimeException（运行时异常）
    │   ├── NullPointerException
    │   ├── ArrayIndexOutOfBoundsException
    │   ├── ClassCastException
    │   └── IllegalArgumentException
    └── Checked Exception（受检异常）
        ├── IOException
        ├── SQLException
        └── ParseException
```

### 1.3 异常对比

| 类型 | 特点 | 是否必须处理 | 示例 |
|------|------|-------------|------|
| Error | 严重错误，JVM级别的问题 | 无法处理 | OutOfMemoryError |
| RuntimeException | 编程错误，可避免 | 可选处理 | NullPointerException |
| Checked Exception | 预期可能发生的异常 | 必须处理 | IOException |

## 二、异常处理机制

### 2.1 try-catch 语句

```java
public class ExceptionExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3};
        
        try {
            // 可能抛出异常的代码
            int result = numbers[5]; // 数组越界
            System.out.println("结果: " + result);
        } catch (ArrayIndexOutOfBoundsException e) {
            // 处理异常
            System.out.println("数组索引越界: " + e.getMessage());
        }
        
        System.out.println("程序继续执行...");
    }
}
```

### 2.2 多 catch 语句

```java
public class MultiCatchExample {
    public static void main(String[] args) {
        try {
            String str = null;
            int num = Integer.parseInt(str);
            int[] arr = {1, 2};
            arr[5] = 10;
        } catch (NullPointerException e) {
            System.out.println("空指针异常: " + e.getMessage());
        } catch (NumberFormatException e) {
            System.out.println("数字格式异常: " + e.getMessage());
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("数组越界异常: " + e.getMessage());
        }
    }
}
```

### 2.3 catch 异常顺序
- 子类异常必须放在父类异常之前
- 否则子类异常的 catch 块永远不会执行

### 2.4 finally 语句

```java
public class FinallyExample {
    public static void main(String[] args) {
        FileInputStream fis = null;
        
        try {
            fis = new FileInputStream("file.txt");
            // 读取文件
        } catch (IOException e) {
            System.out.println("读取文件失败: " + e.getMessage());
        } finally {
            // 无论是否发生异常，都会执行
            try {
                if (fis != null) {
                    fis.close();
                }
            } catch (IOException e) {
                System.out.println("关闭文件失败: " + e.getMessage());
            }
        }
    }
}
```

### 2.5 try-with-resources（Java 7+）

```java
public class TryWithResourcesExample {
    public static void main(String[] args) {
        // 自动关闭资源，无需手动 close
        try (FileInputStream fis = new FileInputStream("file.txt")) {
            // 读取文件
        } catch (IOException e) {
            System.out.println("读取文件失败: " + e.getMessage());
        }
    }
}
```

## 三、抛出异常

### 3.1 throw 关键字

```java
public class ThrowExample {
    public static void checkAge(int age) {
        if (age < 0 || age > 150) {
            throw new IllegalArgumentException("年龄必须在0-150之间");
        }
        System.out.println("年龄合法: " + age);
    }
    
    public static void main(String[] args) {
        try {
            checkAge(200);
        } catch (IllegalArgumentException e) {
            System.out.println("捕获异常: " + e.getMessage());
        }
    }
}
```

### 3.2 throws 关键字

```java
import java.io.IOException;

public class ThrowsExample {
    // 声明方法可能抛出的异常
    public static void readFile(String path) throws IOException {
        FileInputStream fis = new FileInputStream(path);
        // ...
    }
    
    public static void main(String[] args) {
        try {
            readFile("file.txt");
        } catch (IOException e) {
            System.out.println("文件读取失败: " + e.getMessage());
        }
    }
}
```

## 四、自定义异常

### 4.1 创建自定义异常类

```java
// 自定义受检异常
public class InvalidAgeException extends Exception {
    public InvalidAgeException() {
        super();
    }
    
    public InvalidAgeException(String message) {
        super(message);
    }
    
    public InvalidAgeException(String message, Throwable cause) {
        super(message, cause);
    }
}

// 自定义运行时异常
public class BusinessException extends RuntimeException {
    public BusinessException(String message) {
        super(message);
    }
}
```

### 4.2 使用自定义异常

```java
public class UserService {
    public void register(String username, int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("年龄必须满18岁才能注册");
        }
        System.out.println("用户注册成功: " + username);
    }
    
    public void login(String username, String password) {
        if (username == null || username.isEmpty()) {
            throw new BusinessException("用户名不能为空");
        }
        // ...
    }
}
```

## 五、异常处理最佳实践

### 5.1 原则
1. 只捕获能处理的异常
2. 提供有意义的错误信息
3. 不要吞掉异常
4. 使用 finally 或 try-with-resources 清理资源

### 5.2 错误示例

```java
// 错误：吞掉异常
try {
    // ...
} catch (Exception e) {
    // 什么都不做
}

// 错误：捕获太宽泛的异常
try {
    // ...
} catch (Exception e) {
    System.out.println("出错了");
}
```

### 5.3 正确示例

```java
// 正确：只捕获特定异常
try {
    readFile("file.txt");
} catch (FileNotFoundException e) {
    System.out.println("文件不存在: " + e.getMessage());
} catch (IOException e) {
    System.out.println("文件读取失败: " + e.getMessage());
}

// 正确：重新抛出异常
try {
    // ...
} catch (SQLException e) {
    throw new BusinessException("数据库操作失败", e);
}
```

## 六、常见异常类型

### 6.1 RuntimeException 子类

| 异常类型 | 描述 |
|----------|------|
| NullPointerException | 空指针访问 |
| ArrayIndexOutOfBoundsException | 数组索引越界 |
| ClassCastException | 类型转换异常 |
| IllegalArgumentException | 非法参数 |
| NumberFormatException | 数字格式错误 |
| ArithmeticException | 算术运算异常（如除零） |

### 6.2 Checked Exception

| 异常类型 | 描述 |
|----------|------|
| IOException | I/O 操作失败 |
| SQLException | 数据库操作失败 |
| ParseException | 解析失败（如日期解析） |
| InterruptedException | 线程中断 |

## 七、练习

1. 编写程序，捕获数组越界异常和空指针异常
2. 创建一个自定义异常 `InsufficientFundsException`，模拟银行取款时余额不足的情况
3. 使用 try-with-resources 读取文件内容
4. 编写一个方法，声明抛出多个异常，然后在调用处处理
5. 编写一个计算器程序，处理除零异常和非法参数异常