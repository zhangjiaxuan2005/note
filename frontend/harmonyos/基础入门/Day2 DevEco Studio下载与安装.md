# Day2 DevEco Studio下载与安装

> 来源：[华为开发者文档 - 下载与安装DevEco Studio](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-software-install)
> 更新时间：2026-04-22

## 一、下载软件

请前往[下载中心](https://developer.huawei.com/consumer/cn/download/deveco-studio)，登录华为账号后下载DevEco Studio，并根据页面**工具完整性**指导进行完整性校验。

## 二、Windows环境安装

### 运行环境要求

| 配置项 | 要求 |
|--------|------|
| 操作系统 | Windows10 64位、Windows11 64位 |
| 内存 | 16GB及以上 |
| 硬盘 | 100GB及以上 |
| 分辨率 | 1280×800像素及以上 |

### 安装步骤

1. **运行安装程序**
   - 双击下载的 `deveco-studio-xxxx.exe`
   - 选择安装路径（默认：`C:\Program Files`）

2. **选择安装选项**
   - 勾选 **DevEco Studio**
   - 点击下一步直至安装完成

3. **完成安装**
   - 点击 **Finish**
   - 首次运行时选择 **Do not import settings**

### 开箱即用特性

- HarmonyOS SDK已嵌入，无需额外下载
- 包含Node.js、Hvigor、OHPM、模拟器平台
- SDK位置：`DevEco Studio\sdk` 目录

## 三、macOS环境安装

### 运行环境要求

| 配置项 | 要求 |
|--------|------|
| 操作系统 | macOS(X86) 11/12/13/14/15、macOS(ARM) 12/13/14/15 |
| 内存 | 8GB及以上 |
| 硬盘 | 100GB及以上 |
| 分辨率 | 1280×800像素及以上 |

### 安装步骤

1. 将 **DevEco-Studio.app** 拖拽到 **Applications** 文件夹
2. 等待安装完成

## 四、诊断开发环境

DevEco Studio提供开发环境诊断功能：

- **欢迎页面**：单击 **Diagnose**
- **菜单栏**：**Help > Diagnostic Tools > Diagnose Development Environment**

诊断项包括：
- 电脑配置检查
- 网络连通情况
- 依赖工具安装状态

## 五、启用中文化插件

> 该功能仅支持中国境内（香港、澳门、台湾除外）

### DevEco Studio 6.0.0 Beta1 及以上版本

1. 菜单栏：**File > Settings...**（macOS：**DevEco Studio > Preferences/Settings**）
2. 路径：**Appearance & Behavior > System Settings > Language**
3. 语言选择：**Chinese**（6.1.0+ 为 **Chinese(Simplified)**）
4. 点击 **Apply** → **Restart** 重启

### DevEco Studio 6.0.0 Beta1 以下版本

1. 菜单栏：**File > Settings**（macOS：**DevEco Studio > Preferences**）
2. 选择 **Plugins > Installed**
3. 搜索框输入 "Chinese"
4. 找到 **Chinese(Simplified)**，单击 **Enable**
5. 点击 **OK** → **Restart** 重启

## 六、网络配置

在企业网络受限的情况下，需要[配置代理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-environment-config)信息。

## 七、OpenHarmony SDK

如需进行OpenHarmony应用开发：
- **Windows**：`File > Settings > OpenHarmony SDK`
- **macOS**：`DevEco Studio > Preferences/Settings > OpenHarmony SDK`
