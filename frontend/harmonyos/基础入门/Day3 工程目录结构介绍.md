# Day3 工程目录结构介绍

> 来源：[华为开发者文档 - 工程目录结构介绍](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-project-structure)
> 更新时间：2026-04-28

## 一、ArkTS工程目录结构（Stage模型）

Stage模型支持API Version 10及以上版本，是目前推荐的开发模型。

```
工程根目录
├── AppScope/
│   └── app.json5              # 应用全局配置信息
├── entry/                     # 应用/元服务模块（生成一个HAP）
│   ├── src/
│   │   ├── main/
│   │   │   ├── ets/
│   │   │   │   ├── entryability/      # 应用/元服务入口
│   │   │   │   ├── entrybackupability/# 扩展备份恢复能力
│   │   │   │   └── pages/             # 应用页面
│   │   │   ├── resources/             # 资源文件
│   │   │   │   ├── base/element/      # 字符串、颜色、样式等
│   │   │   │   ├── base/media/        # 图片、视频、音频
│   │   │   │   └── rawfile/           # 原始资源文件
│   │   │   └── module.json5           # 模块配置文件
│   │   ├── mock/                      # Mock能力配置
│   │   ├── ohosTest/                  # Instrument Test测试类
│   │   └── test/                      # Local Test测试类
│   ├── build-profile.json5            # 模块编译配置
│   ├── hvigorfile.ts                  # 模块级构建脚本
│   ├── obfuscation-rules.txt          # 混淆规则文件
│   └── oh-package.json5               # 三方包信息
├── oh_modules/                        # 三方库依赖
├── build-profile.json5                # 应用级配置
├── code-linter.json5                  # 代码检查规则
├── hvigorfile.ts                      # 应用级构建脚本
├── oh-package.json5                   # 全局配置
└── oh-package-lock.json5              # 依赖版本锁定
```

### 资源文件说明

| 资源目录 | 资源文件说明 |
|----------|--------------|
| `base/element` | boolean.json、color.json、float.json、intarray.json、integer.json、pattern.json、plural.json、strarray.json、string.json |
| `base/media` | .png、.gif、.mp3、.mp4等多媒体文件 |
| `rawfile` | 任意格式的原始资源文件，需指定路径引用 |

## 二、C++工程目录结构（Stage模型）

支持API Version 10以上版本，可使用ArkTS和C++进行开发。

```
entry/
├── src/
│   ├── main/
│   │   ├── cpp/
│   │   │   ├── types/
│   │   │   │   └── libentry/
│   │   │   │       ├── index.d.ts         # C++ API接口描述
│   │   │   │       └── oh-package.json5   # .so三方包声明
│   │   │   ├── CMakeLists.txt             # CMake配置
│   │   │   └── napi_init.cpp              # C++ API接口定义
│   │   ├── ets/                           # ArkTS源码
│   │   └── resources/                     # 资源文件
│   │   └── module.json5                   # 模块配置
│   └── ...
└── ...
```

## 三、JS工程目录结构（FA模型）

FA模型仅支持JS开发，适用于旧版本兼容。

```
entry/
├── src/
│   ├── main/
│   │   ├── js/
│   │   │   └── MainAbility/       # 应用入口
│   │   │       ├── i18n/          # 多语言资源
│   │   │       ├── pages/         # 页面
│   │   │       └── app.js         # Ability生命周期
│   │   └── resources/             # 资源文件
│   │   └── config.json            # 模块配置
│   └── ...
└── ...
```

## 四、关键配置文件说明

### app.json5（应用级配置）

应用的全局配置信息，位于 `AppScope` 目录下。

### module.json5（模块级配置）

Stage模型的模块配置文件，包含：
- HAP的配置信息
- 应用在具体设备上的配置信息
- 应用的全局配置信息

### build-profile.json5（编译配置）

- **应用级**：签名、产品配置等
- **模块级**：buildOption、targets配置等

### hvigorfile.ts（构建脚本）

- **应用级**：应用级编译构建任务
- **模块级**：模块级编译构建任务

## 五、模型对比

| 特性 | Stage模型 | FA模型 |
|------|-----------|--------|
| 推荐程度 | ⭐⭐⭐ 推荐 | 兼容旧版本 |
| API版本 | 10+ | 所有版本 |
| 开发语言 | ArkTS/C++ | JS |
| 配置文件 | module.json5 | config.json |
| 架构 | 更现代化 | 传统架构 |

## 六、相关文档

- [module.json5配置文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file)
- [资源分类与访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/resource-categories-and-access)
- [应用配置文件概述（Stage模型）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/application-configuration-file-overview-stage)
