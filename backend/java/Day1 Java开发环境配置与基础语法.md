# Day1 Java开发环境配置与基础语法

## 一、Java 开发环境配置

本章节中我们将为大家介绍如何搭建 Java 开发环境。

## 二、Windows 系统安装 Java

### 2.1 下载 JDK

首先我们需要下载 Java 开发工具包 JDK，下载地址：[Oracle 官方下载页面](https://www.oracle.com/java/technologies/downloads/)

在下载页面中根据自己的系统选择对应的版本，本文以 Windows 64 位系统为例：

![JDK下载页面](https://www.runoob.com/wp-content/uploads/2013/12/jdk-download.png)

下载后 JDK 的安装根据提示进行，还有安装 JDK 的时候也会安装 JRE，一并安装就可以了。

安装 JDK，安装过程中可以自定义安装目录等信息，例如我们选择安装目录为 **C:\Program Files (x86)\Java\jdk1.8.0_91**。

### 2.2 配置环境变量

1. 安装完成后，右击"我的电脑"，点击"属性"，选择"高级系统设置"；

![系统属性](https://www.runoob.com/wp-content/uploads/2013/12/win-java1.png)

2. 选择"高级"选项卡，点击"环境变量"；

![高级系统设置](https://www.runoob.com/wp-content/uploads/2013/12/java-win2.png)

然后就会出现如下图所示的画面：

![环境变量](https://www.runoob.com/wp-content/uploads/2013/12/java-win3.png)

在"系统变量"中设置 3 项属性，**JAVA_HOME**、**PATH**、**CLASSPATH**（大小写无所谓），若已存在则点击"编辑"，不存在则点击"新建"。

> **注意：** 如果使用 1.5 以上版本的 JDK，不用设置 CLASSPATH 环境变量，也可以正常编译和运行 Java 程序。

**变量设置参数如下：**

| 变量名 | 变量值 | 说明 |
|--------|--------|------|
| JAVA_HOME | C:\Program Files (x86)\Java\jdk1.8.0_91 | 根据实际安装路径配置 |
| CLASSPATH | .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar; | 记得前面有个"." |
| Path | %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin; | 添加到现有Path值的前面 |

### 2.3 JAVA_HOME 设置

![设置JAVA_HOME](https://www.runoob.com/wp-content/uploads/2013/12/java-win4.png)

![配置JAVA_HOME路径](https://www.runoob.com/wp-content/uploads/2013/12/java-win5.png)

### 2.4 PATH 设置

![设置PATH](https://www.runoob.com/wp-content/uploads/2013/12/java-win6.png)

![配置PATH路径](https://www.runoob.com/wp-content/uploads/2013/12/java-win7.png)

> **注意：** 在 Windows 10 中，Path 变量里是分条显示的，我们需要将 **%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;** 分开添加，否则无法识别：
>
> ```
> %JAVA_HOME%\bin;
> %JAVA_HOME%\jre\bin;
> ```
>
> ![Windows 10 Path配置](https://www.runoob.com/wp-content/uploads/2013/12/44A70696-B2E6-4055-B88F-7FC0222DCCA4.png)

### 2.5 CLASSPATH 设置

![设置CLASSPATH](https://www.runoob.com/wp-content/uploads/2013/12/java-win8.png)

这是 Java 的环境配置，配置完成后，你可以启动 Eclipse 来编写代码，它会自动完成 java 环境的配置。

### 2.6 测试 JDK 是否安装成功

1. "开始"->"运行"，键入"cmd"；

2. 键入命令: **java -version** 、 **java** 、 **javac** 几个命令，出现以下信息，说明环境变量配置成功；

![验证JDK安装](https://www.runoob.com/wp-content/uploads/2013/12/java-win9.png)

---

## 三、Linux、UNIX、Solaris、FreeBSD 环境变量设置

环境变量 PATH 应该设定为指向 Java 二进制文件安装的位置。如果设置遇到困难，请参考 shell 文档。

例如，假设你使用 bash 作为 shell，你可以把下面的内容添加到你的 .bashrc 文件结尾:

```bash
export PATH=/path/to/java:$PATH
```

---

## 四、第一个 Java 程序

### 4.1 HelloWorld.java

安装配置好 JDK 后，我们就可以编写第一个 Java 程序了。

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

### 4.2 编译与运行

保存为 HelloWorld.java，打开命令行窗口，进入你保存文件的目录：

```bash
# 编译 Java 程序
javac HelloWorld.java

# 运行 Java 程序
java HelloWorld
```

执行以上命令，输出结果如下：

```
Hello World
```

---

## 五、Java 基础语法

### 5.1 基本结构

一个 Java 程序可以包含以下部分：

- **包声明**（可选）：`package com.example;`
- **导入语句**：`import java.util.Scanner;`
- **类声明**：`public class ClassName { ... }`
- **主方法**：`public static void main(String[] args) { ... }`

### 5.2 注释

```java
// 单行注释

/*
 * 多行注释
 */

/**
 * 文档注释（可生成API文档）
 */
```

### 5.3 标识符命名规则

- 以字母、下划线 `_`、美元符号 `$` 开头
- 由字母、数字、下划线、美元符号组成
- 大小写敏感
- 不能使用 Java 关键字

**命名规范：**

- 类名：首字母大写，如 `HelloWorld`
- 方法名：小驼峰命名法，如 `getName()`
- 常量：全大写，如 `MAX_VALUE`
- 包名：全小写，如 `com.example`

### 5.4 Java 关键字

常见关键字列表：

| 关键字 | 说明 |
|--------|------|
| public | 公共访问修饰符 |
| class | 类声明关键字 |
| static | 静态修饰符 |
| void | 无返回值 |
| int | 整数类型 |
| if | 条件语句 |
| else | 条件语句 |
| for | 循环语句 |
| while | 循环语句 |
| return | 返回语句 |

---

## 六、流行 Java 开发工具

正所谓工欲善其事必先利其器，我们在开发 Java 语言过程中同样需要一款不错的开发工具，目前市场上的 IDE 很多，本文为大家推荐以下几款 Java 开发工具：

### 6.1 IntelliJ IDEA

JetBrains 的 IDEA，现在很多人开始使用了，功能很强大。

下载地址：[https://www.jetbrains.com/idea/download/](https://www.jetbrains.com/idea/download/)

![IntelliJ IDEA](https://www.runoob.com/wp-content/uploads/2013/12/87862d740859eca8882bc2907500e9cb.png)

### 6.2 VS Code

VS Code（全称：Visual Studio Code）是一款由微软开发且跨平台的免费源代码编辑器。

下载地址：[https://code.visualstudio.com/](https://code.visualstudio.com/)

![VS Code](https://www.runoob.com/wp-content/uploads/2013/12/1f36f0810733df0f1a6900816fe7e0cc.png)

### 6.3 NetBeans

开源免费的 Java IDE。

下载地址：[https://www.netbeans.org/index.html](https://www.netbeans.org/index.html)

![NetBeans](https://www.runoob.com/wp-content/uploads/2013/12/bdb9eac1e0ccb689acefa1820de2d8ef.png)

### 6.4 Eclipse

另一个免费开源的 Java IDE。

下载地址：[https://www.eclipse.org/downloads/packages/](https://www.eclipse.org/downloads/packages/)

选择 **Eclipse IDE for Java Developers**：

![Eclipse](https://www.runoob.com/wp-content/uploads/2013/12/5A92DEAE-EFB9-493D-AC4D-808E529B533C.jpg)

---

## 七、使用 IntelliJ IDEA 创建第一个 Java 应用

1. 启动 IntelliJ IDEA。

2. 在欢迎屏幕中单击"新建项目"。

3. 在"新建项目"向导中，从左侧列表中选择"Java"。

4. 为项目命名（例如 HelloWorld）并根据需要更改默认位置。

5. 在本教程中，我们不会使用版本控制系统，因此请禁用"创建 Git 存储库"选项。

6. 确保在构建系统中选择了 IntelliJ。

![新建项目](https://www.runoob.com/wp-content/uploads/2013/12/java-tutorial-new-project-npw-1.png)

要在 IntelliJ IDEA 中开发 Java 应用程序，您需要 Java SDK (JDK)。

如果 IntelliJ IDEA 中已定义所需的 JDK，请从 JDK 列表中选择它。

如果您的计算机上安装了 JDK，但未在 IDE 中定义，请选择"添加 JDK"并指定 JDK 主目录的路径（例如，/Library/Java/JavaVirtualMachines/jdk-20.0.1.jdk）。

![添加JDK](https://www.runoob.com/wp-content/uploads/2013/12/java-t-create-new-project-npw-1.png)

创建包和类，在项目工具窗口中，右键单击 src 文件夹，选择新建，然后选择 Java 类。

在名称字段中，输入 **com.example.helloworld.HelloWorld** 并点击确定，IntelliJ IDEA 将创建 com.example.helloworld 包和 HelloWorld 类。

编写代码并运行：

```java
package com.example.helloworld;

public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

点击运行按钮或使用快捷键，即可看到输出结果。

---

## 八、使用 Eclipse 运行第一个 Java 程序

HelloWorld.java 文件代码：

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

在 Eclipse 中创建项目，将代码粘贴进去，点击运行按钮即可。

---

## 九、练习

1. 下载并安装 JDK（建议 JDK 11 或以上版本）
2. 配置 JAVA_HOME、Path 环境变量
3. 验证 JDK 安装成功（运行 java -version）
4. 下载安装 IntelliJ IDEA 或 Eclipse
5. 使用 IDE 创建并运行第一个 HelloWorld 程序
6. 练习使用命令行编译和运行 Java 程序