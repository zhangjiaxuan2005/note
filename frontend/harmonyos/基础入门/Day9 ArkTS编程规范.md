# Day9 ArkTS编程规范

> 来源：[华为开发者文档 - ArkTS编程规范](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-coding-style-guide)
> 更新时间：2026-04-30

## 一、目标和适用范围

本文参考业界标准和实践，结合ArkTS语言特点，提供编码指南，以提高代码的**规范性**、**安全性**和**性能**。

**规则级别**：
- **要求**：原则上应该遵从
- **建议**：属于最佳实践，可结合实际情况考虑

## 二、命名规范

### 2.1 标识符命名原则

好的标识符命名应遵循：
- 清晰表达意图，避免使用单个字母或非标准缩写
- 使用正确的英文单词并符合英文语法，不要使用中文拼音
- 确保语句清晰，避免歧义

### 2.2 类名、枚举名、命名空间名 - UpperCamelCase

```typescript
// 类名 - 首字母大写的驼峰命名法
class User {
  username: string
  constructor(username: string) {
    this.username = username;
  }
  sayHi() {
    console.info('hi' + this.username);
  }
}

// 枚举名
enum UserType {
  TEACHER = 0,
  STUDENT = 1
};

// 命名空间
namespace Base64Utils {
  export function encrypt() { }
  export function decrypt() { }
};
```

### 2.3 变量名、方法名、参数名 - lowerCamelCase

```typescript
let msg = 'Hello world';
let userName = 'Zhangsan';

function sendMsg(msg: string) {
  // ...
}

function findUser(userName: string) {
  // ...
}
```

### 2.4 常量名、枚举值名 - 全大写+下划线

```typescript
enum UserType1 {
  TEACHER = 0,
  STUDENT = 1
};

const MAX_USER_SIZE = 10000;
const DEFAULT_TIMEOUT = 3000;
```

### 2.5 布尔变量命名

避免使用否定的布尔变量名，建议加上表达是非意义的前缀：

```typescript
// ❌ 反例
let isNoError = true;
let isNotFound = false;

// ✅ 正例
let isError = false;
let isFound = true;
```

## 三、格式规范

### 3.1 缩进 - 使用空格，禁止Tab

```typescript
// 建议使用2个空格缩进
class DataSource {
  id: number = 0
  title: string = ''
}
```

### 3.2 行宽 - 不超过120个字符

代码行宽不宜过长，否则不利于阅读。

### 3.3 条件语句和循环语句 - 使用大括号

```typescript
// ❌ 反例
if (condition)
  console.info('success');

// ✅ 正例
if (condition) {
  console.info('success');
}
```

### 3.4 switch语句 - case缩进

```typescript
switch (condition) {
  case 0: {
    doSomething();
    break;
  }
  case 1: {
    doOtherthing();
    break;
  }
  default:
    break;
}
```

### 3.5 表达式换行 - 运算符放行末

```typescript
if (userCount > MAX_USER_COUNT ||
  userCount < MIN_USER_COUNT) {
  doSomething();
}
```

### 3.6 变量声明 - 每行一个

```typescript
// ❌ 反例
let maxCount = 10, isCompleted = false;

// ✅ 正例
let maxCount = 10;
let isCompleted = false;
```

### 3.7 空格使用规则

```typescript
// if, for, while, switch与左括号之间加空格
if (isJedi) { }

// 函数名与左括号之间不加空格
function fight(): void { }

// else或catch与大括号之间加空格
if (flag) {
  // ...
} else {
  // ...
}

// 二元运算符前后加空格
let sum = a + b;

// 逗号后加空格，逗号前不加
const arr = [1, 2, 3];
```

### 3.8 字符串 - 建议使用单引号

```typescript
// ❌ 反例
let message1 = "world";

// ✅ 正例
let message2 = 'world';
```

### 3.9 对象字面量 - 超过4个属性需换行

```typescript
// ❌ 反例
let obj1 = { name: 'tom', age: 16, value: 1, sum: 2, foo: true, bar: false }

// ✅ 正例
let obj2 = {
  name: 'tom',
  age: 16,
  value: 1,
  sum: 2,
  foo: true,
  bar: false
}
```

### 3.10 else/catch放在同一行

```typescript
// ✅ 正例
if (isOk) {
  doThing1();
} else {
  doThing3();
}

// ✅ 正例
try {
  doSomething();
} catch (err) {
  // 处理错误
}
```

### 3.11 大括号与语句同一行

```typescript
// ❌ 反例
function foo1()
{
  // ...
}

// ✅ 正例
function foo2() {
  // ...
}
```

## 四、编程实践

### 4.1 添加类属性的可访问修饰符

```typescript
// ❌ 反例
class C1 {
  count: number = 0
  getCount(): number {
    return this.count
  }
}

// ✅ 正例
class C2 {
  private count: number = 0
  public getCount(): number {
    return this.count
  }
}
```

### 4.2 浮点数小数点前后加0

```typescript
// ❌ 反例
const num1 = .5;
const num2 = 2.;
const num3 = -.7;

// ✅ 正例
const num4 = 0.5;
const num5 = 2.0;
const num6 = -0.7;
```

### 4.3 Number.NaN判断 - 必须使用Number.isNaN()

```typescript
// ❌ 反例
if (foo == Number.NaN) { }

// ✅ 正例
if (Number.isNaN(foo)) { }
```

### 4.4 数组遍历 - 优先使用Array方法

```typescript
const numbers = [1, 2, 3, 4, 5];

// ❌ 反例
const increasedByOne1: number[] = [];
for (let i = 0; i < numbers.length; i++) {
  increasedByOne1.push(numbers[i] + 1);
}

// ✅ 正例 - 使用map
const increasedByOne2: number[] = numbers.map(num => num + 1);
```

### 4.5 不要在条件表达式中执行赋值

```typescript
// ❌ 反例
if (isFoo = false) {
  // ...
}

// ✅ 正例
const isFoo = false;
if (isFoo) {
  // ...
}
```

### 4.6 finally块 - 不要使用return/break/continue/throw

```typescript
// ❌ 反例
function foo4() {
  try {
    return 1;
  } catch (err) {
    return 2;
  } finally {
    return 3;  // 错误：finally中return
  }
}

// ✅ 正例
function foo5() {
  try {
    return 1;
  } catch (err) {
    return 2;
  } finally {
    console.info('Finally!');
  }
}
```

### 4.7 避免使用ESObject

ESObject主要用于跨语言调用场景，在非跨语言调用场景中使用会带来额外性能开销：

```typescript
// ✅ 建议直接使用接口类型
import { getObject2, I } from './lib';
let obj2: I = getObject2(123);
```

### 4.8 数组类型表示

```typescript
// ✅ 使用T[]表示数组类型
let arr: number[] = [1, 2, 3];
```

## 五、ArkTS vs TypeScript主要差异

| 特性 | ArkTS | TypeScript |
|------|-------|------------|
| 类型系统 | 强制静态类型 | 支持动态类型 |
| any类型 | 不支持 | 支持 |
| 对象布局 | 禁止运行时变更 | 允许 |
| 运算符 | 限制语义 | 完整支持 |
| 性能 | 优化 | 标准 |

## 六、总结

遵循ArkTS编程规范可以：
- 提高代码可读性和可维护性
- 减少运行时错误
- 提升应用性能
- 便于团队协作

建议在开发过程中使用ESLint等工具进行代码检查，确保代码符合规范要求。
