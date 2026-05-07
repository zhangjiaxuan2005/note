# Day1 Java开发环境配置与基础语法

## 一、JDK安装与环境变量配置

### 1.1 JDK下载与安装
- 访问 Oracle 官网或 OpenJDK 官网下载对应版本的 JDK
- 安装路径建议不要包含中文和空格

### 1.2 环境变量配置

#### Windows 系统：
1. 新建系统变量 `JAVA_HOME`，值为 JDK 安装目录
2. 编辑系统变量 `Path`，添加 `%JAVA_HOME%\bin`

#### Linux/Mac 系统：
编辑 `~/.bash_profile` 或 `~/.zshrc`：
```bash
export JAVA_HOME=/path/to/jdk
export PATH=$JAVA_HOME/bin:$PATH
```

### 1.3 验证安装
```bash
java -version
javac -version
```

## 二、第一个Java程序

### 2.1 HelloWorld.java
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

### 2.2 编译与运行
```bash
javac HelloWorld.java
java HelloWorld
```

## 三、Java基础语法

### 3.1 基本结构
- **包声明**: `package com.example;`
- **导入语句**: `import java.util.Scanner;`
- **类声明**: `public class ClassName { ... }`
- **主方法**: `public static void main(String[] args) { ... }`

### 3.2 注释
```java
// 单行注释

/*
 * 多行注释
 */

/**
 * 文档注释（可生成API文档）
 */
```

### 3.3 标识符命名规则
- 以字母、下划线 `_`、美元符号 `$` 开头
- 由字母、数字、下划线、美元符号组成
- 大小写敏感
- 不能使用Java关键字

### 3.4 Java关键字
常见关键字：`public`, `class`, `static`, `void`, `main`, `String`, `int`, `if`, `else`, `for`, `while` 等

## 四、开发工具推荐

### 4.1 IDE选择
- **IntelliJ IDEA**: 功能强大，智能提示优秀
- **Eclipse**: 开源免费，插件丰富
- **VS Code**: 轻量级，配合Java插件使用

### 4.2 IntelliJ IDEA 配置
1. 安装JDK并配置SDK
2. 创建新项目
3. 配置代码风格和快捷键