# Day8 ArkTS语言基础语法

> 来源：[华为开发者文档 - ArkTS语言介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/introduction-to-arkts)
> 更新时间：2026-04-30

## 一、基础声明

### 1.1 变量声明

使用`let`声明的变量可以在程序执行期间具有不同的值：

```typescript
let hi: string = 'hello';
hi = 'hello, world';
```

### 1.2 常量声明

使用`const`声明的常量为只读类型，只能被赋值一次：

```typescript
const hello: string = 'hello';
// 对常量重新赋值会造成编译时错误
```

### 1.3 自动类型推断

如果变量或常量的声明包含初始值，开发者无需显式指定类型：

```typescript
let hi1: string = 'hello';  // 显式指定类型
let hi2 = 'hello, world';    // 自动推断为string类型
```

## 二、基本类型

### 2.1 number类型

ArkTS提供number类型，任何整数和浮点数都可以赋给此类型的变量：

```typescript
let n1 = 3.14;
let n2 = 1e2;  // 科学计数法

// 整数字面量
let decimal = 42;        // 十进制
let hex = 0xFF;          // 十六进制
let octal = 0o777;       // 八进制
let binary = 0b11;       // 二进制
```

### 2.2 boolean类型

```typescript
let isDone: boolean = false;
if (isDone) {
  console.info('Done!');
}
```

### 2.3 string类型

```typescript
let s1 = 'Hello, world!\n';
let s2 = 'this is a string';
let s3 = `The result is ${s1}`;  // 模板字符串
```

### 2.4 void类型

用于指定函数没有返回值：

```typescript
function noReturn(): void {
  // 没有返回值
}
```

### 2.5 Object类型

```typescript
let o1: Object = 'Alice';
let o2: Object = ['a', 'b'];
let o3: Object = 1;
```

### 2.6 array类型

```typescript
let names: string[] = ['Alice', 'Bob', 'Carol'];
let numbers: Array<number> = [1, 2, 3];
```

### 2.7 enum类型

```typescript
enum ColorSet { Red, Green, Blue }
let c: ColorSet = ColorSet.Red;

// 带值的枚举
enum ColorSet2 { White = 0xFF, Grey = 0x7F, Black = 0x00 }
```

### 2.8 Union类型

```typescript
type Animal = Cat | Dog | Frog | number | string | null | undefined;
let animal: Animal = new Cat();
animal = 42;
animal = 'dog';
```

### 2.9 Aliases类型

```typescript
// 二维数组类型
type Matrix = number[][];

// 函数类型
type Handler = (s: string, no: number) => string;

// 泛型函数类型
type Predicate<T> = (x: T) => boolean;
```

## 三、运算符

### 3.1 赋值运算符

```typescript
let a = 10;
a += 5;  // a = a + 5
a -= 3;  // a = a - 3
```

### 3.2 比较运算符

| 运算符 | 说明 |
|--------|------|
| === | 严格相等（值和类型都相等） |
| !== | 严格不相等 |
| == | 值相等（会进行类型转换） |
| != | 值不相等 |

### 3.3 算术运算符

```typescript
let sum = 5 + 3;   // 加法
let diff = 5 - 3;  // 减法
let product = 5 * 3;  // 乘法
let quotient = 15 / 3;  // 除法
let remainder = 10 % 3; // 取余
```

### 3.4 逻辑运算符

```typescript
if (a > 0 && b > 0) { }  // 逻辑与
if (a > 0 || b > 0) { }  // 逻辑或
if (!isEmpty) { }        // 逻辑非
```

### 3.5 instanceof运算符

```typescript
if (animal instanceof Frog) {
  animal.leap();
}
```

## 四、控制语句

### 4.1 if语句

```typescript
if (condition1) {
  // 语句1
} else if (condition2) {
  // 语句2
} else {
  // else语句
}
```

### 4.2 switch语句

```typescript
switch (expression) {
  case label1:
    // 语句1
    break;
  case label2:
  case label3:
    // label2或label3匹配时执行
    break;
  default:
    // 默认语句
}
```

### 4.3 条件表达式

```typescript
let message = Math.random() > 0.5 ? 'Valid' : 'Failed';
```

### 4.4 for循环

```typescript
let sum = 0;
for (let i = 0; i < 10; i += 2) {
  sum += i;
}
```

### 4.5 for-of循环

```typescript
for (let ch of 'a string object') {
  console.info(ch);
}
```

### 4.6 while循环

```typescript
let n = 0;
while (n < 3) {
  n++;
  x += n;
}
```

### 4.7 do-while循环

```typescript
let i = 0;
do {
  i += 1;
} while (i < 10);
```

### 4.8 break和continue

```typescript
while (true) {
  x++;
  if (x > 5) {
    break;  // 跳出循环
  }
}
```

### 4.9 异常处理

```typescript
throw new Error('this error');

try {
  // 可能抛出异常的代码
} catch (e) {
  // 异常处理
} finally {
  // 无论是否异常都会执行
}
```

## 五、函数

### 5.1 函数声明

```typescript
function add(x: string, y: string): string {
  let z: string = `${x} ${y}`;
  return z;
}
```

### 5.2 可选参数

```typescript
function hello(name?: string) {
  if (name == undefined) {
    console.info('Hello!');
  } else {
    console.info(`Hello, ${name}!`);
  }
}

// 默认参数
function multiply(n: number, coeff: number = 2): number {
  return n * coeff;
}
```

### 5.3 rest参数

```typescript
function sum(...numbers: number[]): number {
  let result = 0;
  for (let n of numbers) {
    result += n;
  }
  return result;
}
```

### 5.4 函数类型

```typescript
type BinaryFunction = (a: number, b: number) => number;
let add: BinaryFunction = (x, y) => x + y;
```

### 5.5 箭头函数

```typescript
let square = (x: number): number => x * x;
let print = (msg: string) => console.info(msg);
```

## 六、类和接口

### 6.1 类定义

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  introduce(): string {
    return `I am ${this.name}, ${this.age} years old.`;
  }
}
```

### 6.2 访问修饰符

```typescript
class Example {
  public publicField: string;      // 公有
  private privateField: number;     // 私有
  protected protectedField: boolean; // 受保护
}
```

### 6.3 抽象类

```typescript
abstract class Shape {
  abstract draw(): void;
}

class Circle extends Shape {
  draw(): void {
    console.info('Drawing a circle');
  }
}
```

### 6.4 接口

```typescript
interface Person {
  name: string;
  age: number;
}

interface Employee extends Person {
  employeeId: number;
}
```

## 七、泛型

### 7.1 泛型类

```typescript
class Container<T> {
  value: T;
  constructor(value: T) {
    this.value = value;
  }
}
```

### 7.2 泛型函数

```typescript
function identity<T>(arg: T): T {
  return arg;
}
```

### 7.3 泛型约束

```typescript
interface Lengthwise {
  length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.info(arg.length);
  return arg;
}
```

## 八、空安全

### 8.1 非空断言

```typescript
let name: string | null = null;
console.info(name!.length);  // 断言name不为null
```

### 8.2 空值合并

```typescript
let name: string | null = null;
let displayName = name ?? 'Unknown';  // 如果name为null，使用'Unknown'
```

### 8.3 可选链

```typescript
let length = name?.length;  // 如果name为null，返回undefined
```

## 九、模块

### 9.1 导出

```typescript
export class Person {
  name: string;
}

export const MAX_SIZE = 100;
```

### 9.2 导入

```typescript
import { Person, MAX_SIZE } from './module';
```

## 十、ArkUI支持

ArkTS原生支持ArkUI框架，可以声明式地构建UI：

```typescript
@Entry
@Component
struct MyComponent {
  @State message: string = 'Hello World'

  build() {
    Column() {
      Text(this.message)
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
    }
    .width('100%')
    .height('100%')
  }
}
```
