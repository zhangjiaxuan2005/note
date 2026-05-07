# Day10 IO流与文件操作

## 一、IO流概述

### 1.1 流的分类

```
IO流
├── 字节流
│   ├── InputStream（输入）
│   │   ├── FileInputStream
│   │   ├── BufferedInputStream
│   │   └── DataInputStream
│   └── OutputStream（输出）
│       ├── FileOutputStream
│       ├── BufferedOutputStream
│       └── DataOutputStream
└── 字符流
    ├── Reader（输入）
    │   ├── FileReader
    │   ├── BufferedReader
    │   └── InputStreamReader
    └── Writer（输出）
        ├── FileWriter
        ├── BufferedWriter
        └── OutputStreamWriter
```

### 1.2 字节流 vs 字符流

| 特性 | 字节流 | 字符流 |
|------|--------|--------|
| 处理单位 | 字节（8位） | 字符（16位） |
| 适用场景 | 二进制文件（图片、音频、视频） | 文本文件 |
| 编码处理 | 不处理编码 | 自动处理编码 |

## 二、字节流

### 2.1 FileInputStream

```java
import java.io.FileInputStream;
import java.io.IOException;

public class FileInputStreamExample {
    public static void main(String[] args) {
        try (FileInputStream fis = new FileInputStream("input.txt")) {
            int data;
            while ((data = fis.read()) != -1) {
                System.out.print((char) data);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 2.2 FileOutputStream

```java
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutputStreamExample {
    public static void main(String[] args) {
        String content = "Hello, World!";
        
        try (FileOutputStream fos = new FileOutputStream("output.txt")) {
            // 写入字节数组
            fos.write(content.getBytes());
            System.out.println("文件写入成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 2.3 字节流复制文件

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileCopyExample {
    public static void main(String[] args) {
        String source = "source.jpg";
        String dest = "dest.jpg";
        
        try (FileInputStream fis = new FileInputStream(source);
             FileOutputStream fos = new FileOutputStream(dest)) {
            
            byte[] buffer = new byte[1024];
            int bytesRead;
            
            while ((bytesRead = fis.read(buffer)) != -1) {
                fos.write(buffer, 0, bytesRead);
            }
            System.out.println("文件复制成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## 三、字符流

### 3.1 FileReader

```java
import java.io.FileReader;
import java.io.IOException;

public class FileReaderExample {
    public static void main(String[] args) {
        try (FileReader reader = new FileReader("input.txt")) {
            int data;
            while ((data = reader.read()) != -1) {
                System.out.print((char) data);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 3.2 FileWriter

```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWriterExample {
    public static void main(String[] args) {
        String content = "你好，世界！";
        
        try (FileWriter writer = new FileWriter("output.txt")) {
            writer.write(content);
            System.out.println("文件写入成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 3.3 BufferedReader

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class BufferedReaderExample {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("input.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 3.4 BufferedWriter

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class BufferedWriterExample {
    public static void main(String[] args) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"))) {
            writer.write("第一行");
            writer.newLine(); // 换行
            writer.write("第二行");
            writer.newLine();
            writer.write("第三行");
            System.out.println("文件写入成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## 四、转换流

### 4.1 InputStreamReader

```java
import java.io.FileInputStream;
import java.io.InputStreamReader;
import java.io.IOException;

public class InputStreamReaderExample {
    public static void main(String[] args) {
        try (FileInputStream fis = new FileInputStream("input.txt");
             InputStreamReader isr = new InputStreamReader(fis, "UTF-8")) {
            
            int data;
            while ((data = isr.read()) != -1) {
                System.out.print((char) data);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 4.2 OutputStreamWriter

```java
import java.io.FileOutputStream;
import java.io.OutputStreamWriter;
import java.io.IOException;

public class OutputStreamWriterExample {
    public static void main(String[] args) {
        try (FileOutputStream fos = new FileOutputStream("output.txt");
             OutputStreamWriter osw = new OutputStreamWriter(fos, "UTF-8")) {
            
            osw.write("中文内容");
            System.out.println("文件写入成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## 五、File 类

### 5.1 文件操作

```java
import java.io.File;
import java.io.IOException;

public class FileExample {
    public static void main(String[] args) {
        File file = new File("example.txt");
        
        try {
            // 创建文件
            if (file.createNewFile()) {
                System.out.println("文件创建成功");
            } else {
                System.out.println("文件已存在");
            }
            
            // 获取文件信息
            System.out.println("文件名: " + file.getName());
            System.out.println("路径: " + file.getPath());
            System.out.println("绝对路径: " + file.getAbsolutePath());
            System.out.println("大小: " + file.length() + " 字节");
            System.out.println("是否是文件: " + file.isFile());
            System.out.println("是否是目录: " + file.isDirectory());
            
            // 删除文件
            if (file.delete()) {
                System.out.println("文件删除成功");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 5.2 目录操作

```java
import java.io.File;

public class DirectoryExample {
    public static void main(String[] args) {
        File dir = new File("mydir");
        
        // 创建目录
        if (dir.mkdir()) {
            System.out.println("目录创建成功");
        }
        
        // 创建多级目录
        File nestedDir = new File("parent/child/grandchild");
        if (nestedDir.mkdirs()) {
            System.out.println("多级目录创建成功");
        }
        
        // 列出目录内容
        File[] files = dir.listFiles();
        if (files != null) {
            for (File file : files) {
                System.out.println(file.getName());
            }
        }
        
        // 删除目录（必须为空）
        if (dir.delete()) {
            System.out.println("目录删除成功");
        }
    }
}
```

## 六、NIO（Java 7+）

### 6.1 Path 与 Files

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.io.IOException;
import java.util.List;

public class NIOExample {
    public static void main(String[] args) {
        Path path = Paths.get("example.txt");
        
        try {
            // 创建文件
            if (Files.notExists(path)) {
                Files.createFile(path);
            }
            
            // 写入内容
            String content = "Hello NIO!";
            Files.write(path, content.getBytes());
            
            // 读取内容
            byte[] bytes = Files.readAllBytes(path);
            System.out.println(new String(bytes));
            
            // 读取所有行
            List<String> lines = Files.readAllLines(path);
            for (String line : lines) {
                System.out.println(line);
            }
            
            // 复制文件
            Path dest = Paths.get("copy.txt");
            Files.copy(path, dest);
            
            // 删除文件
            Files.delete(path);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 6.2 文件遍历

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.io.IOException;

public class FileWalkExample {
    public static void main(String[] args) {
        Path start = Paths.get(".");
        
        try {
            Files.walk(start)
                 .filter(Files::isRegularFile)
                 .forEach(path -> System.out.println(path));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## 七、练习

1. 使用字节流复制图片文件
2. 使用字符流读取文本文件并统计行数
3. 使用 BufferedReader 和 BufferedWriter 实现文件内容复制
4. 使用 File 类遍历指定目录下的所有文件
5. 使用 NIO 的 Files 类实现文件的读写操作