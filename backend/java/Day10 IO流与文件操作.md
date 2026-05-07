# Day10 IO流与文件操作

## 一、Java 流(Stream)、文件(File)和IO

Java 中的流（Stream）、文件（File）和 IO（输入输出）是处理数据读取和写入的基础设施，它们允许程序与外部数据（如文件、网络、系统输入等）进行交互。

java.io 包是 Java 标准库中的一个核心包，提供了用于系统输入和输出的类，它包含了处理数据流（字节流和字符流）、文件读写、序列化以及数据格式化的工具。

一个流可以理解为一个数据的序列。输入流表示从一个源读取数据，输出流表示向一个目标写数据。

### 1.1 字节流和字符流

| 类型 | 处理单位 | 适用场景 |
| --- | --- | --- |
| 字节流 | 字节（8位） | 二进制文件（图片、音频、视频） |
| 字符流 | 字符（16位） | 文本文件 |

---

## 二、读取控制台输入

Java 的控制台输入由 System.in 完成。为了获得一个绑定到控制台的字符流，可以把 System.in 包装在一个 BufferedReader 对象中来创建一个字符流。

### 2.1 从控制台读取多字符输入

**BRRead.java 文件代码：**

```java
import java.io.*;

public class BRRead {
    public static void main(String[] args) throws IOException {
        char c;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        System.out.println("输入字符, 按下 'q' 键退出。");
        do {
            c = (char) br.read();
            System.out.println(c);
        } while (c != 'q');
    }
}
```

输出结果：

```
输入字符, 按下 'q' 键退出。
runoob
r
u
n
o
o
b

q
q
```

### 2.2 从控制台读取字符串

**BRReadLines.java 文件代码：**

```java
import java.io.*;

public class BRReadLines {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str;
        System.out.println("Enter lines of text.");
        System.out.println("Enter 'end' to quit.");
        do {
            str = br.readLine();
            System.out.println(str);
        } while (!str.equals("end"));
    }
}
```

输出结果：

```
Enter lines of text.
Enter 'end' to quit.
This is line one
This is line one
This is line two
This is line two
end
end
```

---

## 三、FileInputStream

该流用于从文件读取数据，它的对象可以用关键字 new 来创建。

### 3.1 创建 FileInputStream

```java
// 使用字符串类型的文件名
InputStream f = new FileInputStream("C:/java/hello");

// 使用文件对象
File f = new File("C:/java/hello");
InputStream in = new FileInputStream(f);
```

### 3.2 FileInputStream 方法

| 方法 | 描述 |
| --- | --- |
| `int read()` | 读取一个字节的数据，返回值为 0 到 255 之间的整数。如果到达流的末尾，返回 -1 |
| `int read(byte[] b)` | 从输入流中读取字节，并将其存储在字节数组 b 中，返回实际读取的字节数 |
| `void close()` | 关闭输入流并释放与该流相关的所有资源 |

### 3.3 读取文件示例

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

---

## 四、FileOutputStream

该类用来创建一个文件并向文件中写数据。如果该流在打开文件进行输出前，目标文件不存在，那么该流会创建该文件。

### 4.1 创建 FileOutputStream

```java
// 使用字符串类型的文件名
OutputStream f = new FileOutputStream("C:/java/hello");

// 使用文件对象
File f = new File("C:/java/hello");
OutputStream fOut = new FileOutputStream(f);
```

### 4.2 FileOutputStream 方法

| 方法 | 描述 |
| --- | --- |
| `void write(int b)` | 将指定的字节写入输出流 |
| `void write(byte[] b)` | 将字节数组 b 中的所有字节写入输出流 |
| `void flush()` | 刷新输出流并强制写出所有缓冲的数据 |
| `void close()` | 关闭输出流并释放与该流相关的所有资源 |

### 4.3 写入文件示例

```java
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutputStreamExample {
    public static void main(String[] args) {
        String content = "Hello, World!";
        
        try (FileOutputStream fos = new FileOutputStream("output.txt")) {
            fos.write(content.getBytes());
            System.out.println("文件写入成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 4.4 字节流复制文件

**fileStreamTest.java 文件代码：**

```java
import java.io.*;

public class fileStreamTest {
    public static void main(String[] args) {
        try {
            byte bWrite[] = { 11, 21, 3, 40, 5 };
            OutputStream os = new FileOutputStream("test.txt");
            for (int x = 0; x < bWrite.length; x++) {
                os.write(bWrite[x]);
            }
            os.close();
            
            InputStream is = new FileInputStream("test.txt");
            int size = is.available();
            for (int i = 0; i < size; i++) {
                System.out.print((char) is.read() + " ");
            }
            is.close();
        } catch (IOException e) {
            System.out.print("Exception");
        }
    }
}
```

---

## 五、字符流

字符流用于处理文本数据，例如读取和写入字符串或文件。

### 5.1 FileReader

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

### 5.2 FileWriter

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

### 5.3 BufferedReader

**fileStreamTest2.java 文件代码：**

```java
import java.io.*;

public class fileStreamTest2 {
    public static void main(String[] args) throws IOException {
        File f = new File("a.txt");
        FileOutputStream fop = new FileOutputStream(f);
        OutputStreamWriter writer = new OutputStreamWriter(fop, "UTF-8");
        writer.append("中文输入");
        writer.append("\r\n");
        writer.append("English");
        writer.close();
        fop.close();
        
        FileInputStream fip = new FileInputStream(f);
        InputStreamReader reader = new InputStreamReader(fip, "UTF-8");
        StringBuffer sb = new StringBuffer();
        while (reader.ready()) {
            sb.append((char) reader.read());
        }
        System.out.println(sb.toString());
        reader.close();
        fip.close();
    }
}
```

---

## 六、File 类

File 类用于表示文件或目录，并提供文件操作，如创建、删除、重命名等。

### 6.1 创建目录

File 类中有两个方法可以用来创建文件夹：

- **mkdir()** 方法创建一个文件夹，成功则返回 true，失败则返回 false
- **mkdirs()** 方法创建一个文件夹和它的所有父文件夹

**CreateDir.java 文件代码：**

```java
import java.io.File;

public class CreateDir {
    public static void main(String[] args) {
        String dirname = "/tmp/user/java/bin";
        File d = new File(dirname);
        d.mkdirs();
    }
}
```

### 6.2 读取目录

**DirList.java 文件代码：**

```java
import java.io.File;

public class DirList {
    public static void main(String args[]) {
        String dirname = "/tmp";
        File f1 = new File(dirname);
        if (f1.isDirectory()) {
            System.out.println("目录 " + dirname);
            String s[] = f1.list();
            for (int i = 0; i < s.length; i++) {
                File f = new File(dirname + "/" + s[i]);
                if (f.isDirectory()) {
                    System.out.println(s[i] + " 是一个目录");
                } else {
                    System.out.println(s[i] + " 是一个文件");
                }
            }
        } else {
            System.out.println(dirname + " 不是一个目录");
        }
    }
}
```

输出结果：

```
目录 /tmp
bin 是一个目录
lib 是一个目录
demo 是一个目录
test.txt 是一个文件
README 是一个文件
index.html 是一个文件
include 是一个目录
```

### 6.3 删除目录或文件

删除文件可以使用 java.io.File.delete() 方法。

**DeleteFileDemo.java 文件代码：**

```java
import java.io.File;

public class DeleteFileDemo {
    public static void main(String[] args) {
        File folder = new File("/tmp/java/");
        deleteFolder(folder);
    }
    
    public static void deleteFolder(File folder) {
        File[] files = folder.listFiles();
        if (files != null) {
            for (File f : files) {
                if (f.isDirectory()) {
                    deleteFolder(f);
                } else {
                    f.delete();
                }
            }
        }
        folder.delete();
    }
}
```

### 6.4 文件操作示例

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

---

## 七、NIO（Java 7+）

### 7.1 Path 与 Files

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

### 7.2 文件遍历

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

---

## 八、练习

1. 使用字节流复制图片文件
2. 使用字符流读取文本文件并统计行数
3. 使用 BufferedReader 和 BufferedWriter 实现文件内容复制
4. 使用 File 类遍历指定目录下的所有文件
5. 使用 NIO 的 Files 类实现文件的读写操作