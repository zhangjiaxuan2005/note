# Day7 初识ArkTS语言

> 来源：[华为开发者文档 - 初识ArkTS语言](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-get-started)
> 更新时间：2026-03-09

## 一、ArkTS概述

**ArkTS**是HarmonyOS应用的默认开发语言，在TypeScript（简称TS）生态基础上做了扩展，保持TS的基本风格。通过规范定义，强化了开发期的静态检查和分析，提升了程序执行的稳定性和性能。

## 二、ArkTS的核心特性

自API version 10起，ArkTS进一步通过规范强化静态检查和分析，主要特性包括：

### 1. 强制使用静态类型

静态类型是ArkTS最重要的特性之一。如果使用静态类型，那么程序中变量的类型就是确定的。同时，由于所有类型在程序实际运行前都是已知的，编译器可以验证代码的正确性，从而减少运行时的类型检查，有助于性能提升。

### 2. 禁止在运行时改变对象布局

为实现最优性能，ArkTS禁止在程序执行期间更改对象布局。

### 3. 限制运算符语义

为获得更好的性能并鼓励编写清晰的代码，ArkTS限制了部分运算符的语义。例如，一元加法运算符仅能作用于数字，不能用于其他类型变量。

### 4. 不支持Structural typing

根据实际场景的需求和反馈，后续会重新考虑是否支持Structural typing。

## 三、ArkTS与TypeScript的关系

```
JavaScript (JS)
    ↓ 添加类型
TypeScript (TS)
    ↓ 扩展和优化
ArkTS
```

- ArkTS兼容TS/JavaScript（简称JS）生态
- 开发者可以使用TS/JS进行开发或复用已有代码
- 保持了TypeScript的大部分语法，为现有TypeScript开发者提供高度兼容的体验

## 四、ArkTS的演进方向

未来，ArkTS会结合应用开发/运行的需求持续演进，逐步增强：

- 并行和并发能力
- 扩展系统类型
- 引入分布式开发范式等更多特性

## 五、学习资源

### ArkTS学习路线
- [ArkTS学习路线](https://developer.huawei.com/consumer/cn/arkts/)
- [ArkTS视频课程](https://developer.huawei.com/consumer/cn/training/course/slightMooc/C101717496870909384?pathId=101667550095504391)

### 相关文档
- [ArkTS具体指南](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-overview)
- [ArkTS语言介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/introduction-to-arkts)
- [ArkTS语法适配背景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/arkts-migration-background)
- [从TypeScript到ArkTS的适配规则](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/typescript-to-arkts-migration-guide)

## 六、快速入门建议

1. **熟悉TypeScript基础**：ArkTS基于TypeScript，建议先掌握TS语法
2. **理解静态类型优势**：掌握ArkTS的静态类型约束
3. **遵循编码规范**：参考官方ArkTS编程规范
4. **实践高性能编程**：学习ArkTS高性能编程实践
5. **项目迁移准备**：如有TS项目，学习迁移规则

## 七、总结

ArkTS是一门专为HarmonyOS应用开发设计的高性能编程语言，在保持TypeScript易用性的同时，通过静态类型约束和性能优化，为移动应用开发提供了更好的开发体验和运行效率。
