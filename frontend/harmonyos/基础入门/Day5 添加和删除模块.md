# Day5 添加和删除模块

> 来源：[华为开发者文档 - 添加和删除模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-add-new-module)
> 更新时间：2026-04-30

## 一、模块概述

**模块（Module）** 是应用/元服务的基本功能单元，包含：
- 源代码
- 资源文件
- 第三方库
- 应用/元服务配置文件

一个应用/元服务通常包含一个或多个模块。

### 模块类型

| 类型 | 说明 |
|------|------|
| **entry** | 应用/元服务的主模块，必须存在 |
| **feature** | 特性模块（仅应用工程支持） |
| **har** | 静态共享包 |
| **shared** | 动态共享包（HSP） |

## 二、创建新的模块

### 方法1：工程目录右键创建

1. 鼠标移到工程目录顶部
2. 单击右键 → **New > Module...**
3. 模块将创建在工程根目录下

### 方法2：菜单栏创建

1. 选中工程目录中任意文件
2. 菜单栏 → **File > New > Module...**
3. 模块将创建在工程根目录下

### 方法3：指定目录创建

1. 在工程根目录下创建一个新的Directory
2. 在该目录下单击右键 → **New > Module...**
3. 模块将创建在该文件目录下（便于分类管理）

> **注意**：暂不支持在以下目录创建模块：
> - AppScope
> - hvigor
> - oh_modules
> - build
> - 以点开头的目录（如.hvigor、.idea）

### 模块配置

在 **New Project Module** 界面：

1. **选择模板** → 单击 **Next**

2. **配置模块信息**：

| 配置项 | 说明 |
|--------|------|
| **Module name** | 模块名称，不可与工程名/其他模块名相同 |
| **Module type** | Feature或Entry类型（仅Ability模板） |
| **Device type** | 模块支持的设备类型 |
| **Enable native** | 创建可调用C/C++的共享包（仅Library模板） |
| **C++ Standard** | C++标准库：Toolchain Default/C++11/C++14 |

3. **Ability配置**（如模板类型为Ability）：
   - **Ability name**：Ability名称
   - **Exported**：是否可被其他应用/元服务调用
     - ✅ 勾选（true）：可被其他应用调用
     - ⬜ 不勾选（false）：不能被其他应用调用

4. 单击 **Finish**，等待创建完成

### 模块类型说明

**Entry模块**：
- 同一工程仅支持创建一个entry模块
- 如需构建多个entry类型模块，可在 `module.json5` 中修改type字段
- 同一设备类型已存在entry模块时，新entry模块需[配置分发策略](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#distributionfilter标签)

**Feature模块**：
- 只能选择该工程原有的设备类型

## 三、删除模块

1. 在工程目录中选中要删除的模块
2. 单击鼠标右键 → **Delete**
3. 在弹出的对话框中单击 **Delete** 确认

## 四、模块配置管理

工程中所包含模块的信息可在 `build-profile.json5` 中的 `modules` 字段进行配置：

```json5
{
  "modules": [
    {
      "name": "entry",
      "srcPath": "./entry",
      "targets": [
        {
          "name": "default",
          "applyToProducts": ["default"]
        }
      ]
    }
  ]
}
```

## 五、版本说明

从 **DevEco Studio 6.0.1 Beta1** 开始：
- 创建Native C++模块支持选择C++版本
- 创建Library模板支持选择C++版本

## 六、相关文档

- [module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)
- [模块管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-module-management)
- [导入和引用模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-import-module)
- [开发动态共享包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hsp)
