# Day1 DevEco Studio工具概述

> 来源：[华为开发者文档 - 工具概述](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-tools-overview)
> 更新时间：2026-03-17

## 一、HarmonyOS应用/元服务开发

### DevEco Studio集成开发环境

**HUAWEI DevEco Studio**（以下简称DevEco Studio）是基于IntelliJ IDEA Community开源版本打造，面向HarmonyOS应用/元服务开发场景的一站式集成开发环境。

### 核心功能

| 功能 | 说明 |
|------|------|
| **CodeGenie AI辅助编程** | 智能知识问答、代码生成&补全、万能卡片生成、UI界面生成 |
| **智能代码编辑** | ArkTS、JS和C/C++代码智能补全、代码重构 |
| **多端双向实时预览** | UI编码时快速预览多种设备上的显示效果 |
| **Hvigor轻量级构建工具** | 支持源码、资源、构建流程自定义，灵活构建多目标产物 |
| **跨语言调试** | ArkTS&C++语言调试、汇编调试、lldb命令调试、反向调试 |
| **Profiler应用调优** | 内存泄漏、组件耗时、网络请求、应用启动、界面卡顿分析 |
| **AppAnalyzer应用体检** | 发现兼容性、性能、功耗、稳定性等问题 |
| **本地模拟器** | 手机（含折叠屏）、平板、PC/2in1等类型模拟器 |
| **依赖管理（ohpm）** | 安装、更新、删除和管理HAR、HSP或模块依赖 |

## 二、开发流程

开发一个应用/元服务的完整流程：

```
┌─────────────┐    ┌─────────────┐    ┌─────────────────┐    ┌─────────────┐
│  一、开发准备  │ → │ 二、开发应用/元服务│ → │ 三、运行调试和测试  │ → │ 四、发布应用/元服务│
└─────────────┘    └─────────────┘    └─────────────────┘    └─────────────┘
       │                  │                   │                    │
       ▼                  ▼                   ▼                    ▼
   下载安装IDE        创建工程向导         真机调试              发布到应用市场
   配置网络环境        定义UI界面          单步调试              应用市场签名
                      开发业务功能          Instrument Test
                      使用预览器            Local Test
```

## 三、命令行开发工具

针对流水线或命令行开发场景，提供Command Line Tools：

- **codelinter** - 代码检查与快速修复
- **ohpm** - 三方包管理工具
- **hstack** - 堆栈解析工具（Release应用混淆后还原）
- **hvigorw** - 命令行构建工具

## 四、约束与限制

以下功能仅支持中国境内（香港、澳门、台湾除外）：

1. Partner SDK功能
2. Template Market模板市场
3. Sample导入功能
4. 端云一体化工程创建及开发
5. 软件包及符号表上传功能
6. Collect Logs and Diagnostic Data日志回传功能
7. Operation Analyzer运维服务
8. AppAnalyzer应用与元服务体检
9. AI辅助编程工具DevEco CodeGenie
10. OHPM Index OpenHarmony开源中心仓

## 五、相关链接

- [下载DevEco Studio](https://developer.huawei.com/consumer/cn/download/)
- [配置代理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-environment-config)
- [应用开发导读](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-dev-guide)
- [API接口文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/development-intro-api)
