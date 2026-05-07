# Day4 创建一个新的工程

> 来源：[华为开发者文档 - 创建一个新的工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-create-new-project)
> 更新时间：2026-04-30

## 一、创建HarmonyOS工程

### 步骤1：打开工程创建向导

**方式一**：欢迎页 → **Create Project**

**方式二**：菜单栏 → **File > New > Create Project**

### 步骤2：选择工程模板

1. 选择创建 **Application**（应用）或 **Atomic Service**（元服务）
2. 选择需要的 **Ability工程模板**
3. 单击 **Next**

> **说明**：
> - 从API 11版本开始支持Atomic Service元服务工程开发
> - Atomic Service元服务工程暂不支持Native开发

### 步骤3：配置工程信息

| 配置项 | 说明 | 要求 |
|--------|------|------|
| **Project name** | 工程名称 | 1~200字符，字母/数字/下划线，字母开头 |
| **Bundle name** | 应用包名 | 7~128字符，三段以上，如 `com.example.myapplication` |
| **Save location** | 存储路径 | 不能包含中文字符 |
| **Compatible SDK** | 兼容的最低API Version | 根据需求选择 |
| **Module name** | 模块名称 | 自定义 |
| **Device type** | 支持的设备类型 | 参考deviceTypes标签 |
| **C++ Standard** | C++标准库 | Toolchain Default/C++11/C++14 |

### 包名命名规则

```
com.example.myapplication
│   │       │
│   │       └── 应用名（数字/字母开头，数字/字母结尾）
│   └── 公司/组织名（数字/字母开头）
└── 顶级域名（英文字母开头）
```

**约束**：
- 至少包含三段，以点号分隔
- 不允许多个点号连续出现
- 每段仅允许英文字母、数字、下划线

### 步骤4：完成创建

单击 **Finish**，工具自动生成示例代码和相关资源，等待工程创建完成。

## 二、创建OpenHarmony工程（可选）

### 修改build-profile.json5

在已创建的HarmonyOS工程基础上，修改工程级 `build-profile.json5`：

```json5
{
  "app": {
    "signingConfigs": [],
    "products": [
      {
        "name": "default",
        "signingConfig": "default",
        "compileSdkVersion": 24,      // 指定编译版本
        "targetSdkVersion": 24,       // 目标SDK版本
        "compatibleSdkVersion": 24,   // 兼容最低版本
        "runtimeOS": "OpenHarmony",   // 修改为OpenHarmony
        "buildOption": {
          "strictMode": {
            "caseSensitiveCheck": true,
            "useNormalizedOHMUrl": true
          }
        }
      }
    ]
  }
}
```

### 同步工程

1. 单击 **Sync Now** 进行同步
2. 在弹窗中点击 **Yes**
3. 同意将 `module.json5/config.json` 中的设备类型切换为OpenHarmony支持的default类型

### Native C++工程特殊配置

若选择Native C++模板创建OpenHarmony应用，且需要在RK开发板上运行：

在对应Native模块的 `build-profile.json5` 文件中，添加 `abiFilters`：

```json5
{
  "buildOption": {
    "externalNativeOptions": {
      "abiFilters": "armeabi-v7a"
    }
  }
}
```

## 三、工程模板说明

DevEco Studio提供多种工程模板，不同模板支持：
- 不同的设备类型
- 不同的API Version
- 不同的开发场景

创建前请参考[工程模板介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-template)了解各模板详情。

## 四、性能建议

运行DevEco Studio工程时，建议每个运行窗口有 **2GB以上** 的可用内存空间。

## 五、相关文档

- [工程模板介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-template)
- [模块管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-module-management)
- [工程目录结构介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-project-structure)
- [创建元服务工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-create-faproject)
