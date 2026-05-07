# Day11 从TypeScript迁移到ArkTS

> 来源：[华为开发者文档 - 从TypeScript到ArkTS的适配规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/typescript-to-arkts-migration-guide)
> 更新时间：2026-04-30

## 一、概述

ArkTS规范约束了TypeScript中影响开发正确性或增加运行时开销的特性。本文罗列了ArkTS中限制的TS特性，并提供重构代码的建议。

**规则级别**：
- **错误**：必须遵从的约束，违反将导致程序编译失败
- **警告**：推荐遵从的约束，违反可能影响性能或未来导致编译失败

## 二、核心差异

### 2.1 TypeScript → ArkTS 演进图

```
TypeScript
    ├── 强制使用静态类型 ❌ 禁止any/unknown
    ├── 禁止运行时变更对象布局 ❌ 禁止动态添加属性
    ├── 限制运算符语义 ❌ 限制+、-、~等运算符
    └── 不支持Structural typing ❌ 必须使用nominal typing
```

### 2.2 主要限制

| 特性 | TypeScript | ArkTS | 级别 |
|------|-----------|-------|------|
| any类型 | ✅ 支持 | ❌ 禁止 | 错误 |
| 运行时对象变更 | ✅ 支持 | ❌ 禁止 | 错误 |
| 运算符重载语义 | ✅ 完整 | ❌ 限制 | 错误/警告 |
| Structural typing | ✅ 支持 | ❌ 不支持 | 错误 |

## 三、类型系统迁移

### 3.1 禁止使用any和unknown

```typescript
// ❌ TypeScript
let res: any = some_api_function('hello', 'world');
let value: unknown = getUnknownValue();

// ✅ ArkTS - 使用具体类型
class CallResult {
  public succeeded(): boolean {
    return false;
  }
  public errorMessage(): string {
    return '123';
  }
}

function some_api_function(param1: string, param2: string): CallResult {
  return new CallResult();
}

let res: CallResult = some_api_function('hello', 'world');
```

### 3.2 禁止运行时变更对象布局

```typescript
class Point {
  public x: number = 0
  public y: number = 0
}

// ❌ TypeScript - 可以通过as any绕过
let p1 = new Point(1.0, 1.0);
(p1 as any).z = 'Label'; // TS中不会报错

// ✅ ArkTS - 严格检查
let p2 = new Point(2.0, 2.0);
(p2 as any).z = 'Label'; // ArkTS中产生编译时错误
```

### 3.3 使用class而非call signature

```typescript
// ❌ TypeScript
type DescribableFunction = {
  description: string
  (someArg: string): string
}

// ✅ ArkTS - 使用类
class DescribableFunction {
  public description: string;
  public invoke(someArg: string): string {
    return someArg;
  }
  constructor() {
    this.description = 'desc';
  }
}
```

### 3.4 使用class而非构造签名

```typescript
// ❌ TypeScript
type SomeConstructor = {
  new(s: string): SomeObject
}

// ✅ ArkTS - 使用类构造函数
class SomeObject {
  public f: string;
  constructor(s: string) {
    this.f = s;
  }
}
```

### 3.5 使用继承而非intersection type

```typescript
// ❌ TypeScript
type Employee = Identity & Contact

// ✅ ArkTS - 使用接口继承
interface Employee extends Identity, Contact {}
```

### 3.6 不支持index signature

```typescript
// ❌ TypeScript
interface StringArray {
  [index: number]: string
}

// ✅ ArkTS - 使用数组
class X {
  public f: string[] = [];
}
let myArray: X = new X();
const secondItem = myArray.f[1];
```

## 四、变量声明迁移

### 4.1 使用let而非var

```typescript
// ❌ TypeScript - 支持var
function f(shouldInitialize: boolean) {
  if (shouldInitialize) {
    var x = 'b';
  }
  return x; // var函数级作用域
}

// ✅ ArkTS - 只支持let
function f(shouldInitialize: boolean): string {
  let x: string = 'a';
  if (shouldInitialize) {
    x = 'b';
  }
  return x; // let块级作用域
}
```

### 4.2 类型、命名空间命名必须唯一

```typescript
// ❌ TypeScript - 可以同名
let X: string
type X = number[] // 类型别名与变量同名

// ✅ ArkTS - 必须唯一
let X: string;
type T = number[]; // 使用不同的名称
```

## 五、运算符限制

### 5.1 一元运算符限制

```typescript
// ❌ TypeScript - 一元+可作用于字符串
let s = +'42'; // 合法

// ✅ ArkTS - 一元+只能作用于数值
let t = +42; // 合法
// let s = +'42'; // 编译时错误
```

### 5.2 不支持delete运算符

```typescript
// ❌ TypeScript
delete obj.property;

// ✅ ArkTS - 不支持delete运算符
// 需要通过其他方式处理
```

### 5.3 部分支持instanceof

```typescript
// ✅ ArkTS - 支持instanceof
if (animal instanceof Frog) {
  animal.leap();
}
```

### 5.4 不支持in运算符

```typescript
// ❌ TypeScript
if ('property' in obj) { }

// ✅ ArkTS - 不支持in运算符
// 需要使用其他方式检查属性
```

## 六、语法限制

### 6.1 不支持Symbol() API

```typescript
// ❌ TypeScript
let sym = Symbol('description');

// ✅ ArkTS - 不支持Symbol
// ArkTS只支持Symbol.iterator
```

### 6.2 不支持#私有字段

```typescript
// ❌ TypeScript
class C {
  #foo: number = 42
}

// ✅ ArkTS - 使用private关键字
class C {
  private foo: number = 42;
}
```

### 6.3 不支持解构赋值

```typescript
// ❌ TypeScript
let { a, b } = obj;
let [x, y] = arr;

// ✅ ArkTS - 不支持解构
let a = obj.a;
let b = obj.b;
```

### 6.4 不支持解构变量声明

```typescript
// ❌ TypeScript
const { name, age } = person;

// ✅ ArkTS - 逐个声明
const name = person.name;
const age = person.age;
```

### 6.5 逗号运算符仅用在for循环

```typescript
// ✅ ArkTS - for循环中可以使用
for (let i = 0, j = 0; i < 10; i++, j++) {
  // ...
}
```

### 6.6 不支持for..in

```typescript
// ❌ TypeScript
for (let key in obj) { }

// ✅ ArkTS - 使用Object.keys或其他方式
// Object.keys(obj).forEach(key => { });
```

### 6.7 不支持映射类型

```typescript
// ❌ TypeScript
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
}

// ✅ ArkTS - 不支持映射类型
```

### 6.8 不支持with语句

```typescript
// ❌ TypeScript
with (obj) {
  console.log(name);
}

// ✅ ArkTS - 不支持with语句
console.log(obj.name);
```

### 6.9 限制throw语句

```typescript
// ✅ ArkTS - throw只能抛出Error类型
throw new Error('message');
```

## 七、类和接口限制

### 7.1 不支持类表达式

```typescript
// ❌ TypeScript
const MyClass = class { };

// ✅ ArkTS - 使用标准类声明
class MyClass { }
```

### 7.2 不支持implements

```typescript
// ❌ TypeScript
class Dog implements Animal { }

// ✅ ArkTS - 不支持implements关键字
// 通过继承或组合实现
```

### 7.3 不支持修改对象的方法

```typescript
// ❌ TypeScript - 可以动态添加方法
obj.method = function() { };

// ✅ ArkTS - 不允许
// 类定义后不能再添加方法
```

### 7.4 类型转换仅支持as T语法

```typescript
// ✅ ArkTS - 只支持as语法
let str = value as string;

// ❌ TypeScript - 也支持<>语法
// let str = <string>value; // ArkTS不支持
```

### 7.5 不支持JSX

```typescript
// ❌ TypeScript - 支持JSX
// const element = <div>Hello</div>;

// ✅ ArkTS - 使用ArkUI声明式语法
Column() {
  Text('Hello')
}
```

### 7.6 仅支持一个静态块

```typescript
// ❌ TypeScript - 可以有多个静态块
class C {
  static s: string
  static {
    C.s = 'aa'
  }
  static {
    C.s = C.s + 'bb'
  }
}

// ✅ ArkTS - 只能有一个静态块
class C {
  public static s: string;
  static {
    C.s = 'aa';
    C.s = C.s + 'bb';
  }
}
```

## 八、模块限制

### 8.1 不支持export =语法

```typescript
// ❌ TypeScript
export = MyClass;

// ✅ ArkTS - 使用标准export
export class MyClass { }
```

### 8.2 不支持ambient module声明

```typescript
// ❌ TypeScript
declare module 'module-name' { }

// ✅ ArkTS - 不支持
```

### 8.3 限制import赋值表达式

```typescript
// ❌ TypeScript
import fs = require('fs');

// ✅ ArkTS - 使用标准import
import fs from '@kit.ArkUI';
```

## 九、其他限制

### 9.1 不支持new.target

```typescript
// ❌ TypeScript
function foo() {
  console.info(new.target);
}

// ✅ ArkTS - 不支持
```

### 9.2 不支持确定赋值断言

```typescript
// ❌ TypeScript
let x!: number;

// ✅ ArkTS - 必须显式初始化或赋值
let x: number;
```

### 9.3 不支持globalThis

```typescript
// ❌ TypeScript
globalThis.someValue;

// ✅ ArkTS - 不支持
```

### 9.4 不支持as const断言

```typescript
// ❌ TypeScript
const colors = ['red', 'green'] as const;

// ✅ ArkTS - 不支持
const colors: string[] = ['red', 'green'];
```

### 9.5 不支持导入断言

```typescript
// ❌ TypeScript
import data from './data.json' assert { type: 'json' };

// ✅ ArkTS - 不支持
```

### 9.6 class不能被用作对象

```typescript
// ❌ TypeScript
class MyClass { }
MyClass.someProperty = 'value';

// ✅ ArkTS - 不支持
// 需要使用静态属性
```

## 十、迁移工具和资源

### 10.1 迁移步骤

1. **代码审计** - 检查现有TS代码中使用的特性
2. **识别问题** - 找出需要修改的代码
3. **逐个修改** - 按照规范修改每个问题点
4. **测试验证** - 确保功能正常
5. **性能测试** - 验证性能改进

### 10.2 迁移检查清单

- [ ] 移除所有any和unknown类型
- [ ] 将var改为let
- [ ] 移除运行时对象属性变更
- [ ] 移除Symbol()使用
- [ ] 将#私有字段改为private
- [ ] 移除解构赋值
- [ ] 移除不支持的运算符
- [ ] 简化intersection type
- [ ] 移除不支持的语法

### 10.3 相关资源

- [ArkTS语法适配背景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-migration-background)
- [适配指导案例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-more-cases)
- [ArkTS语言介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/introduction-to-arkts)
- [ArkTS编程规范](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-coding-style-guide)
- [ArkTS高性能编程实践](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-high-performance-programming)

## 十一、总结

从TypeScript迁移到ArkTS需要：
1. **理解差异** - 熟悉ArkTS的限制
2. **逐个修改** - 按照规范调整代码
3. **测试验证** - 确保功能正确
4. **性能优化** - 利用ArkTS的性能优势

迁移虽然需要一定工作量，但能够获得更好的性能和稳定性。
