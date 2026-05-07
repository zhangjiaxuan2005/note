# Day6 导入和引用模块

> 来源：[华为开发者文档 - 导入和引用模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-import-module)
> 更新时间：2026-04-30

## 一、两种方式导入模块

DevEco Studio支持两种方式导入其他工程下的模块：

| 方式 | 说明 | 特点 |
|------|------|------|
| **Import Module** | 将其他HarmonyOS模块的功能代码复制到当前工程 | 代码完全复制到本地 |
| **相对路径引用** | 在srcPath字段配置相对路径引用其他工程模块 | 仅引用信息，不复制代码 |

### 模型兼容性

- ✅ FA模型 → FA模型
- ✅ Stage模型 → Stage模型
- ❌ FA模型 → Stage模型（不支持）
- ❌ Stage模型 → FA模型（不支持）

## 二、导入模块（Import Module）

### 步骤

1. **打开导入对话框**
   - 菜单栏 → **File > New > Import... > Import Module**

2. **选择模块**
   - 在指定路径下选择要导入的模块
   - 支持文件夹或zip格式
   - 单击 **OK**

### 导入效果

- 模块代码完全复制到当前工程中
- 成为当前工程的一部分
- 可以独立编辑和构建

## 三、引用模块（相对路径）

### 适用场景

- 引用其他工程下的HAR模块
- 引用其他工程下的HSP模块
- 不需要将模块代码完全复制到本工程

### 配置方法

在**工程级** `build-profile.json5` 文件中，在 `modules > srcPath` 字段配置工程外模块的相对路径：

```json5
{
  "modules": [
    {
      "name": "entry",
      "srcPath": "./entry"
    },
    {
      "name": "myhar",
      "srcPath": "../other-project/myhar"  // 相对路径引用其他工程的HAR
    },
    {
      "name": "myhsp",
      "srcPath": "../shared-project/myhsp" // 相对路径引用其他工程的HSP
    }
  ]
}
```

### 引用特点

- 仅引用模块相关信息
- 不会将模块代码完全复制至本工程
- 模块源码保持独立，修改后同步生效
- 适合多工程共享公共模块的场景

## 四、HAR与HSP的区别

| 特性 | HAR（静态共享包） | HSP（动态共享包） |
|------|------------------|------------------|
| **打包方式** | 静态链接 | 动态加载 |
| **包体积** | 每个引用方都包含一份 | 多个引用方共享一份 |
| **适用场景** | 小型工具库、UI组件 | 大型公共模块、多应用共享 |
| **版本管理** | 独立版本 | 独立版本 |

## 五、模块引用最佳实践

### 场景1：团队内共享公共库

```
projects/
├── common-libs/           # 公共库工程
│   ├── network-har/
│   └── ui-components-har/
├── project-a/             # 项目A
│   └── 引用 ../common-libs/network-har
└── project-b/             # 项目B
    └── 引用 ../common-libs/ui-components-har
```

### 场景2：导入第三方模块

使用 **Import Module** 方式将第三方模块代码导入到工程中，便于修改和定制。

### 场景3：多模块协同开发

使用 **相对路径引用** 方式，保持各模块独立开发，通过相对路径关联。

## 六、常见问题

### Q1：导入模块后无法识别？

- 检查模型类型是否匹配（FA/Stage）
- 执行 **Sync Project** 同步工程
- 检查模块配置是否正确

### Q2：如何正确引用HAR/HSP包？

参考文档：[如何正确引用HAR/HSP包模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-faqs/faqs-package-structure-21)

### Q3：DevEco Studio无法识别复制的模块？

参考文档：[DevEco Studio无法识别复制的模块](https://developer.huawei.com/consumer/cn/doc/architecture-guides/architecture-v1-3_2-ts_77-0000002430310169)

## 七、相关文档

- [模块管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-module-management)
- [添加和删除模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-add-new-module)
- [引用及管理共享包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-har-import)
- [开发动态共享包](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hsp)
