# Day10 ArkTS高性能编程实践

> 来源：[华为开发者文档 - ArkTS高性能编程实践](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-high-performance-programming)
> 更新时间：2026-04-30

## 一、概述

本文提供应用性能敏感场景下的高性能编程建议，帮助开发者编写高性能应用。高性能编程实践是在开发过程中总结的一些高性能写法和建议。

## 二、声明与表达式

### 2.1 使用const声明不变的变量

不变的变量推荐使用const声明，编译器可以进行更多优化：

```typescript
const index = 10000; // 该变量在后续过程中未发生改变，建议声明成常量
```

### 2.2 number类型避免整型和浮点型混用

运行时在优化时会区分整型和浮点型数据，避免在初始化后改变数据类型：

```typescript
// ❌ 反例
let intNum = 1;
intNum = 1.1; // 该变量在声明时为整型数据，后续赋值浮点型数据

// ✅ 正例
let doubleNum = 1.1;
doubleNum = 2.2; // 保持数据类型一致
```

### 2.3 数值计算避免溢出

常见可能导致溢出的数值计算场景：
- 加法、减法、乘法、指数运算等，应避免数值大于INT32_MAX（2147483647）或小于INT32_MIN（-2147483648）
- &（and）、>>>（无符号右移）等运算，应避免数值大于INT32_MAX

```typescript
// ❌ 反例 - 可能溢出
let result = 2000000000 + 2000000000;

// ✅ 正例 - 避免溢出
if (value <= INT32_MAX && value >= INT32_MIN) {
  // 安全计算
}
```

### 2.4 循环中常量提取，减少属性访问次数

如果常量在循环中不会改变，可以将其提取到循环外部：

```typescript
// ❌ 反例 - 每次循环都访问Time.info和Time.start
class Time {
  static start: number = 0;
  static info: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
}

function getNum(num: number): number {
  let total: number = 348;
  for (let index: number = 0x8000; index > 0x8; index >>= 1) {
    total += ((Time.info[num - Time.start] & index) !== 0) ? 1 : 0;
  }
  return total;
}

// ✅ 正例 - 提取不变量到循环外部
function getNumBetter(num: number): number {
  let total: number = 348;
  const info = TimeBetter.info[num - TimeBetter.start]; // 从循环中提取不变量
  for (let index: number = 0x8000; index > 0x8; index >>= 1) {
    if ((info & index) != 0) {
      total++;
    }
  }
  return total;
}
```

## 三、函数

### 3.1 使用参数传递函数外的变量

使用闭包会造成额外的开销，在性能敏感场景中建议使用参数传递：

```typescript
// ❌ 反例 - 使用闭包
let arr = [0, 1, 2];
function fooWithout(): number {
  return arr[0] + arr[1]; // 闭包引用外部变量
}

// ✅ 正例 - 使用参数传递
let arr_ = [0, 1, 2];
function fooWithArray(array: number[]): number {
  return array[0] + array[1];
}
fooWithArray(arr_);
```

### 3.2 避免使用可选参数

可选参数表示参数可能为undefined，使用时需要进行非空判断，造成额外开销：

```typescript
// ❌ 反例 - 使用可选参数
function add(left?: number, right?: number): number | undefined {
  if (left != undefined && right != undefined) {
    return left + right;
  }
  return undefined;
}

// ✅ 正例 - 使用默认参数
function addWithParams(left: number = 0, right: number = 0): number {
  return left + right;
}
```

## 四、数组

### 4.1 数值数组推荐使用TypedArray

涉及纯数值计算时，推荐使用TypedArray数据结构：

```typescript
// ❌ 反例 - 使用Array
const arr1 = new Array<number>(1, 2, 3);
const arr2 = new Array<number>(4, 5, 6);
let res = new Array<number>(3);
for (let i = 0; i < 3; i++) {
  res[i] = arr1[i] + arr2[i];
}

// ✅ 正例 - 使用TypedArray
const typedArray1 = Int8Array.from([1, 2, 3]);
const typedArray2 = Int8Array.from([4, 5, 6]);
let res1 = new Array<number>(3);
for (let i = 0; i < 3; i++) {
  res1[i] = typedArray1[i] + typedArray2[i];
}
```

### 4.2 避免使用稀疏数组

运行时在分配超过1024大小的数组或稀疏数组时，会采用hash表来存储元素，访问速度较慢：

```typescript
// ❌ 反例 - 创建稀疏数组
let result: number[] = [];
result[9999] = 0; // 创建稀疏数组

// ❌ 反例 - 预分配大数组
let count = 100000;
let res: number[] = new Array(count).fill(0);

// ✅ 正例 - 按需创建数组
let result: number[] = [];
for (let i = 0; i < 10; i++) {
  result.push(i);
}
```

### 4.3 避免使用联合类型数组

避免在数值数组中混合使用整型数据和浮点型数据：

```typescript
// ❌ 反例 - 联合类型数组
let arrUnion: (number | string)[] = [1, 'hello'];

// ❌ 反例 - 混合整型和浮点型
let arrNum: number[] = [1, 1.1, 2];

// ✅ 正例 - 相同类型数组
let arrInt: number[] = [1, 2, 3];
let arrDouble: number[] = [0.1, 0.2, 0.3];
let arrString: string[] = ['hello', 'world'];
```

## 五、异常

### 5.1 避免频繁抛出异常

创建异常时会构造异常的栈帧，造成性能损耗。在性能敏感场景中应避免频繁抛出异常：

```typescript
// ❌ 反例 - 在循环中频繁抛出异常
function sum(num: number): number {
  let sum = 0;
  try {
    for (let t = 1; t < 100; t++) {
      sum += div(t, num); // 可能抛出异常
    }
  } catch (e) {
    console.info(e.message);
  }
  return sum;
}

// ✅ 正例 - 直接拦截异常场景
function sumBetter(num: number): number {
  let sum = 0;
  for (let t = 1; t < 100; t++) {
    if (num <= 0) { // 直接拦截异常场景
      console.info('Invalid numbers.');
    }
    sum += divBetter(t, num);
  }
  return sum;
}
```

## 六、性能优化最佳实践总结

### 6.1 声明优化
- ✅ 使用const声明不变变量
- ✅ 避免整型和浮点型混用
- ✅ 数值计算避免溢出

### 6.2 循环优化
- ✅ 提取循环中的常量
- ✅ 避免稀疏数组
- ✅ 使用TypedArray处理数值数组

### 6.3 函数优化
- ✅ 使用参数传递外部变量
- ✅ 避免使用可选参数
- ✅ 优先使用默认参数

### 6.4 类型优化
- ✅ 避免联合类型数组
- ✅ 保持数组元素类型一致
- ✅ 使用具体的类型而非any

### 6.5 异常优化
- ✅ 避免在循环中抛出异常
- ✅ 使用条件判断替代异常控制流

## 七、性能检测工具

使用DevEco Studio提供的性能检测工具：
- **Profiler应用调优**：分析内存泄漏、组件耗时、网络请求等
- **AppAnalyzer**：发现性能问题
- **开发态性能检测**：在开发阶段发现问题

## 八、相关资源

- [ArkTS编程规范](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-coding-style-guide)
- [适配指导案例](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-more-cases)
- [面向其他语言的ArkTS迁移指导](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-for-other-languages)
- [ArkTS高性能编程视频课程](https://developer.huawei.com/consumer/cn/training/course/introduction/C201765964164346054)
