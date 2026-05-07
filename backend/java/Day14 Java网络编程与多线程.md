# Day14 Java网络编程与多线程

## 一、Java 网络编程

### 1.1 网络编程概述

**网络编程**是指编写运行在多个设备（计算机）的程序，这些设备通过网络连接。

**Java 网络编程主要涉及：**
- `java.net` 包中的类和接口
- TCP（传输控制协议）：面向连接、可靠
- UDP（用户数据报协议）：无连接、不可靠

### 1.2 IP 地址和端口

```java
import java.net.InetAddress;

public class InetAddressDemo {
    public static void main(String[] args) throws Exception {
        // 获取本地主机
        InetAddress localHost = InetAddress.getLocalHost();
        System.out.println("本地主机名: " + localHost.getHostName());
        System.out.println("本地IP地址: " + localHost.getHostAddress());
        
        // 根据主机名获取IP地址
        InetAddress baidu = InetAddress.getByName("www.baidu.com");
        System.out.println("百度IP: " + baidu.getHostAddress());
        
        // 根据IP地址获取主机名
        InetAddress byAddress = InetAddress.getByName("14.215.177.38");
        System.out.println("主机名: " + byAddress.getHostName());
    }
}
```

### 1.3 URL 处理

```java
import java.net.URL;
import java.io.*;

public class URLDemo {
    public static void main(String[] args) throws Exception {
        URL url = new URL("https://www.runoob.com:80/index.html?name=java#top");
        
        System.out.println("协议: " + url.getProtocol());    // https
        System.out.println("主机: " + url.getHost());        // www.runoob.com
        System.out.println("端口: " + url.getPort());        // 80
        System.out.println("路径: " + url.getPath());        // /index.html
        System.out.println("查询: " + url.getQuery());       // name=java
        System.out.println("锚点: " + url.getRef());         // top
        
        // 读取网页内容
        URL runoob = new URL("https://www.runoob.com");
        BufferedReader reader = new BufferedReader(
            new InputStreamReader(runoob.openStream()));
        
        String line;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
        reader.close();
    }
}
```

### 1.4 Socket 编程（TCP）

Socket 使用 TCP 提供了两台计算机之间的通信机制。

#### 服务端程序

```java
import java.io.*;
import java.net.*;

public class ServerDemo {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(8888)) {
            System.out.println("服务器启动，等待客户端连接...");
            
            // 等待客户端连接
            Socket socket = serverSocket.accept();
            System.out.println("客户端已连接: " + socket.getInetAddress());
            
            // 获取输入流，读取客户端消息
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream()));
            
            // 获取输出流，向客户端发送消息
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            
            String message;
            while ((message = in.readLine()) != null) {
                System.out.println("收到客户端消息: " + message);
                out.println("服务器回复: " + message);
                
                if ("bye".equalsIgnoreCase(message)) {
                    break;
                }
            }
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### 客户端程序

```java
import java.io.*;
import java.net.*;

public class ClientDemo {
    public static void main(String[] args) {
        try (Socket socket = new Socket("localhost", 8888)) {
            System.out.println("已连接到服务器");
            
            // 获取输出流，向服务器发送消息
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            
            // 获取输入流，读取服务器回复
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream()));
            
            // 读取控制台输入
            BufferedReader console = new BufferedReader(
                new InputStreamReader(System.in));
            
            String userInput;
            while ((userInput = console.readLine()) != null) {
                out.println(userInput);
                System.out.println(in.readLine());
                
                if ("bye".equalsIgnoreCase(userInput)) {
                    break;
                }
            }
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 1.5 多线程服务器

```java
import java.io.*;
import java.net.*;

public class MultiThreadServer {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(8888)) {
            System.out.println("多线程服务器启动...");
            
            while (true) {
                Socket socket = serverSocket.accept();
                System.out.println("新客户端连接: " + socket.getInetAddress());
                
                // 为每个客户端创建一个新线程
                new ClientHandler(socket).start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

class ClientHandler extends Thread {
    private Socket socket;
    
    public ClientHandler(Socket socket) {
        this.socket = socket;
    }
    
    @Override
    public void run() {
        try (
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream()));
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true)
        ) {
            String message;
            while ((message = in.readLine()) != null) {
                System.out.println("来自 " + socket.getInetAddress() + ": " + message);
                out.println("收到: " + message);
                
                if ("bye".equalsIgnoreCase(message)) {
                    break;
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                socket.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

### 1.6 UDP 编程

```java
import java.net.*;

// UDP 发送端
public class UDPSender {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket();
        
        String message = "Hello, UDP!";
        byte[] data = message.getBytes();
        
        DatagramPacket packet = new DatagramPacket(
            data, data.length, 
            InetAddress.getByName("localhost"), 9999
        );
        
        socket.send(packet);
        System.out.println("消息已发送");
        
        socket.close();
    }
}

// UDP 接收端
public class UDPReceiver {
    public static void main(String[] args) throws Exception {
        DatagramSocket socket = new DatagramSocket(9999);
        
        byte[] buffer = new byte[1024];
        DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
        
        System.out.println("等待接收消息...");
        socket.receive(packet);
        
        String received = new String(packet.getData(), 0, packet.getLength());
        System.out.println("收到消息: " + received);
        System.out.println("来自: " + packet.getAddress() + ":" + packet.getPort());
        
        socket.close();
    }
}
```

---

## 二、Java 多线程编程

### 2.1 线程概述

**线程**是进程中单一顺序的控制流，一个进程中可以并发多个线程。

**线程的生命周期：**
- **新建（New）**：线程对象被创建
- **就绪（Runnable）**：调用 start() 方法后
- **运行（Running）**：获得 CPU 资源执行 run()
- **阻塞（Blocked）**：等待锁、sleep、wait 等
- **终止（Terminated）**：run() 方法执行完毕

### 2.2 创建线程的三种方式

#### 方式1：继承 Thread 类

```java
class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
            try {
                Thread.sleep(1000);  // 休眠1秒
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

public class ThreadDemo1 {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        
        t1.setName("线程1");
        t2.setName("线程2");
        
        t1.start();  // 启动线程
        t2.start();
    }
}
```

#### 方式2：实现 Runnable 接口

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println(Thread.currentThread().getName() + ": " + i);
        }
    }
}

public class ThreadDemo2 {
    public static void main(String[] args) {
        MyRunnable runnable = new MyRunnable();
        
        Thread t1 = new Thread(runnable, "线程A");
        Thread t2 = new Thread(runnable, "线程B");
        
        t1.start();
        t2.start();
    }
}
```

#### 方式3：实现 Callable 接口（带返回值）

```java
import java.util.concurrent.*;

class MyCallable implements Callable<String> {
    @Override
    public String call() throws Exception {
        Thread.sleep(2000);
        return "任务完成";
    }
}

public class ThreadDemo3 {
    public static void main(String[] args) throws Exception {
        MyCallable callable = new MyCallable();
        FutureTask<String> futureTask = new FutureTask<>(callable);
        
        Thread thread = new Thread(futureTask);
        thread.start();
        
        // 获取返回值（会阻塞直到任务完成）
        String result = futureTask.get();
        System.out.println("结果: " + result);
    }
}
```

### 2.3 线程常用方法

```java
public class ThreadMethods {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new Thread(() -> {
            System.out.println("子线程运行中...");
        });
        
        // 设置线程名
        t.setName("工作线程");
        
        // 设置优先级（1-10，默认5）
        t.setPriority(Thread.MAX_PRIORITY);  // 10
        
        // 设置为守护线程
        t.setDaemon(true);
        
        // 启动线程
        t.start();
        
        // 等待线程结束
        t.join();
        
        // 判断线程状态
        System.out.println("是否存活: " + t.isAlive());
        System.out.println("是否中断: " + t.isInterrupted());
        
        // 获取当前线程
        Thread current = Thread.currentThread();
        System.out.println("当前线程: " + current.getName());
        
        // 线程休眠
        Thread.sleep(1000);
        
        // 让出 CPU
        Thread.yield();
    }
}
```

### 2.4 线程同步

当多个线程访问共享资源时，需要使用同步机制。

#### synchronized 关键字

```java
class BankAccount {
    private double balance;
    
    public BankAccount(double balance) {
        this.balance = balance;
    }
    
    // 同步方法
    public synchronized void deposit(double amount) {
        double newBalance = balance + amount;
        try {
            Thread.sleep(10);  // 模拟处理时间
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        balance = newBalance;
    }
    
    // 同步代码块
    public void withdraw(double amount) {
        synchronized (this) {
            if (balance >= amount) {
                balance -= amount;
            }
        }
    }
    
    public double getBalance() {
        return balance;
    }
}
```

#### Lock 接口

```java
import java.util.concurrent.locks.*;

class SafeBankAccount {
    private double balance;
    private final Lock lock = new ReentrantLock();
    
    public void deposit(double amount) {
        lock.lock();  // 获取锁
        try {
            balance += amount;
        } finally {
            lock.unlock();  // 释放锁
        }
    }
    
    public void withdraw(double amount) {
        lock.lock();
        try {
            if (balance >= amount) {
                balance -= amount;
            }
        } finally {
            lock.unlock();
        }
    }
}
```

### 2.5 线程间通信

```java
class Message {
    private String content;
    private boolean empty = true;
    
    // 消费者使用
    public synchronized String read() {
        while (empty) {
            try {
                wait();  // 等待生产者生产
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        empty = true;
        notifyAll();  // 通知生产者
        return content;
    }
    
    // 生产者使用
    public synchronized void write(String content) {
        while (!empty) {
            try {
                wait();  // 等待消费者消费
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        this.content = content;
        empty = false;
        notifyAll();  // 通知消费者
    }
}

class Producer implements Runnable {
    private Message message;
    
    public Producer(Message message) {
        this.message = message;
    }
    
    @Override
    public void run() {
        String[] messages = {"消息1", "消息2", "消息3"};
        for (String msg : messages) {
            message.write(msg);
            System.out.println("生产: " + msg);
        }
    }
}

class Consumer implements Runnable {
    private Message message;
    
    public Consumer(Message message) {
        this.message = message;
    }
    
    @Override
    public void run() {
        for (int i = 0; i < 3; i++) {
            String msg = message.read();
            System.out.println("消费: " + msg);
        }
    }
}
```

### 2.6 线程池

```java
import java.util.concurrent.*;

public class ThreadPoolDemo {
    public static void main(String[] args) {
        // 创建固定大小的线程池
        ExecutorService executor = Executors.newFixedThreadPool(5);
        
        // 提交任务
        for (int i = 0; i < 10; i++) {
            final int taskId = i;
            executor.submit(() -> {
                System.out.println("任务 " + taskId + 
                    " 由 " + Thread.currentThread().getName() + " 执行");
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            });
        }
        
        // 关闭线程池
        executor.shutdown();
        
        // 等待所有任务完成
        try {
            executor.awaitTermination(60, TimeUnit.SECONDS);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

### 2.7 线程安全集合

```java
import java.util.concurrent.*;

public class ConcurrentCollections {
    public static void main(String[] args) {
        // 线程安全的List
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
        
        // 线程安全的Set
        CopyOnWriteArraySet<String> set = new CopyOnWriteArraySet<>();
        
        // 线程安全的Map
        ConcurrentHashMap<String, String> map = new ConcurrentHashMap<>();
        
        // 阻塞队列
        BlockingQueue<String> queue = new LinkedBlockingQueue<>();
        
        // 生产者
        new Thread(() -> {
            try {
                queue.put("消息1");
                queue.put("消息2");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
        
        // 消费者
        new Thread(() -> {
            try {
                System.out.println(queue.take());
                System.out.println(queue.take());
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
    }
}
```

---

## 三、练习题目

### 题目1：简单聊天室
使用 Socket 实现一个简单的客户端-服务端聊天程序。

<details>
<summary>点击查看答案</summary>

```java
// 服务端
import java.io.*;
import java.net.*;
import java.util.*;

public class ChatServer {
    private static Set<PrintWriter> clients = new HashSet<>();
    
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(8888);
        System.out.println("聊天室服务器启动...");
        
        while (true) {
            Socket socket = serverSocket.accept();
            new ClientThread(socket).start();
        }
    }
    
    static class ClientThread extends Thread {
        private Socket socket;
        private PrintWriter out;
        
        public ClientThread(Socket socket) {
            this.socket = socket;
        }
        
        public void run() {
            try {
                BufferedReader in = new BufferedReader(
                    new InputStreamReader(socket.getInputStream()));
                out = new PrintWriter(socket.getOutputStream(), true);
                
                synchronized (clients) {
                    clients.add(out);
                }
                
                String message;
                while ((message = in.readLine()) != null) {
                    System.out.println("收到: " + message);
                    broadcast(message);
                }
            } catch (IOException e) {
                e.printStackTrace();
            } finally {
                synchronized (clients) {
                    clients.remove(out);
                }
            }
        }
        
        private void broadcast(String message) {
            synchronized (clients) {
                for (PrintWriter client : clients) {
                    client.println(message);
                }
            }
        }
    }
}

// 客户端
import java.io.*;
import java.net.*;

public class ChatClient {
    public static void main(String[] args) throws Exception {
        Socket socket = new Socket("localhost", 8888);
        
        BufferedReader in = new BufferedReader(
            new InputStreamReader(socket.getInputStream()));
        PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
        BufferedReader console = new BufferedReader(
            new InputStreamReader(System.in));
        
        // 接收消息的线程
        new Thread(() -> {
            try {
                String message;
                while ((message = in.readLine()) != null) {
                    System.out.println(message);
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }).start();
        
        // 发送消息
        String userInput;
        while ((userInput = console.readLine()) != null) {
            out.println(userInput);
        }
    }
}
```
</details>

### 题目2：生产者消费者模式
使用 wait/notify 实现生产者消费者模式。

<details>
<summary>点击查看答案</summary>

```java
import java.util.LinkedList;
import java.util.Queue;

class Buffer {
    private Queue<Integer> queue = new LinkedList<>();
    private int capacity = 5;
    
    public synchronized void produce(int value) throws InterruptedException {
        while (queue.size() == capacity) {
            wait();
        }
        queue.offer(value);
        System.out.println("生产: " + value + ", 库存: " + queue.size());
        notifyAll();
    }
    
    public synchronized int consume() throws InterruptedException {
        while (queue.isEmpty()) {
            wait();
        }
        int value = queue.poll();
        System.out.println("消费: " + value + ", 库存: " + queue.size());
        notifyAll();
        return value;
    }
}

public class ProducerConsumer {
    public static void main(String[] args) {
        Buffer buffer = new Buffer();
        
        // 生产者线程
        Thread producer = new Thread(() -> {
            for (int i = 0; i < 10; i++) {
                try {
                    buffer.produce(i);
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
        
        // 消费者线程
        Thread consumer = new Thread(() -> {
            for (int i = 0; i < 10; i++) {
                try {
                    buffer.consume();
                    Thread.sleep(200);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
        
        producer.start();
        consumer.start();
    }
}
```
</details>

### 题目3：多线程下载器
使用线程池实现多线程文件下载（模拟）。

<details>
<summary>点击查看答案</summary>

```java
import java.util.concurrent.*;

class DownloadTask implements Runnable {
    private String fileName;
    private int fileSize;
    
    public DownloadTask(String fileName, int fileSize) {
        this.fileName = fileName;
        this.fileSize = fileSize;
    }
    
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() + 
            " 开始下载: " + fileName);
        
        try {
            // 模拟下载过程
            for (int i = 0; i <= 100; i += 20) {
                Thread.sleep(fileSize * 100);  // 模拟下载时间
                System.out.println(fileName + " 下载进度: " + i + "%");
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println(fileName + " 下载完成!");
    }
}

public class MultiThreadDownloader {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);
        
        String[] files = {"file1.zip", "file2.zip", "file3.zip", 
                          "file4.zip", "file5.zip"};
        
        for (String file : files) {
            executor.submit(new DownloadTask(file, 1));
        }
        
        executor.shutdown();
    }
}
```
</details>

---

## 四、总结

| 知识点 | 核心内容 |
|--------|----------|
| 网络编程 | Socket、TCP/UDP、ServerSocket、多线程服务器 |
| 多线程 | 创建方式、生命周期、同步、通信、线程池 |
| 并发集合 | ConcurrentHashMap、CopyOnWriteArrayList、BlockingQueue |

**重点掌握：**
1. Socket 通信的基本流程（服务端和客户端）
2. 三种创建线程的方式及其区别
3. synchronized 和 Lock 的使用
4. wait/notify 实现线程间通信
5. 线程池的创建和使用
6. 线程安全集合的选择

**注意事项：**
- 多线程访问共享资源必须同步
- 避免死锁：按固定顺序获取锁
- 线程池使用完毕后要关闭
- 网络编程要注意异常处理和资源释放
