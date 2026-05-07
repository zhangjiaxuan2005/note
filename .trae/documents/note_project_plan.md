# 笔记项目规划文档

## 1. 项目概述

本项目是一个综合性笔记应用，融合了前端、后端、人工智能和嵌入式技术，旨在提供智能、高效的笔记管理体验。

## 2. 技术栈选择

### 2.1 前端技术栈
| 分类 | 技术 | 版本 | 说明 |
|------|------|------|------|
| 框架 | React | 18.x | 现代化前端框架，支持组件化开发 |
| 状态管理 | Redux/Toolkit | 1.x | 集中式状态管理 |
| 路由 | React Router | 6.x | 单页应用路由管理 |
| UI库 | Ant Design | 5.x | 企业级UI组件库 |
| 构建工具 | Vite | 6.x | 快速构建工具 |
| 语言 | TypeScript | 5.x | 类型安全 |

### 2.2 后端技术栈
| 分类 | 技术 | 版本 | 说明 |
|------|------|------|------|
| 框架 | NestJS | 10.x | 企业级Node.js框架 |
| 数据库 | PostgreSQL | 16.x | 关系型数据库 |
| ORM | TypeORM | 0.x | 数据库ORM工具 |
| 认证 | JWT | - | JSON Web Token认证 |
| API文档 | Swagger | - | 自动生成API文档 |

### 2.3 人工智能技术栈
| 分类 | 技术 | 版本 | 说明 |
|------|------|------|------|
| 框架 | Python | 3.11 | AI开发语言 |
| 机器学习 | PyTorch | 2.x | 深度学习框架 |
| 自然语言处理 | Transformers | 4.x | HuggingFace NLP库 |
| 向量数据库 | Pinecone/Chroma | - | 向量检索 |
| API框架 | FastAPI | 0.100+ | 高性能API框架 |

### 2.4 嵌入式技术栈
| 分类 | 技术 | 版本 | 说明 |
|------|------|------|------|
| 语言 | C/C++ | - | 嵌入式开发语言 |
| 框架 | ESP-IDF | 5.x | ESP32开发框架 |
| 通信 | MQTT | - | 物联网通信协议 |
| 存储 | SQLite | - | 轻量级嵌入式数据库 |

## 3. 项目结构

```
/workspace/
├── frontend/                 # 前端应用
│   ├── src/
│   │   ├── components/       # UI组件
│   │   ├── pages/            # 页面组件
│   │   ├── store/            # Redux状态管理
│   │   ├── api/              # API调用
│   │   ├── types/            # 类型定义
│   │   └── utils/            # 工具函数
│   ├── public/               # 静态资源
│   ├── package.json
│   ├── vite.config.ts
│   └── tsconfig.json
├── backend/                  # 后端服务
│   ├── src/
│   │   ├── modules/          # 业务模块
│   │   │   ├── notes/        # 笔记模块
│   │   │   ├── users/        # 用户模块
│   │   │   └── ai/           # AI集成模块
│   │   ├── shared/           # 共享模块
│   │   ├── config/           # 配置文件
│   │   └── main.ts           # 入口文件
│   ├── package.json
│   ├── nest-cli.json
│   └── tsconfig.json
├── ai/                       # 人工智能服务
│   ├── src/
│   │   ├── models/           # AI模型
│   │   ├── services/         # AI服务
│   │   ├── api/              # API路由
│   │   └── main.py           # 入口文件
│   ├── requirements.txt
│   └── Dockerfile
├── embedded/                 # 嵌入式固件
│   ├── main/
│   │   ├── app.c             # 主应用
│   │   ├── components/       # 硬件组件驱动
│   │   ├── network/          # 网络通信
│   │   └── storage/          # 本地存储
│   ├── CMakeLists.txt
│   ├── sdkconfig
│   └── platformio.ini
├── docker-compose.yml        # Docker Compose配置
├── .env                      # 环境变量
└── README.md                 # 项目说明
```

## 4. 核心功能模块

### 4.1 前端功能
| 模块 | 功能描述 | 优先级 |
|------|----------|--------|
| 用户认证 | 登录、注册、密码找回 | 高 |
| 笔记管理 | 创建、编辑、删除、搜索笔记 | 高 |
| 笔记分类 | 文件夹、标签管理 | 高 |
| 富文本编辑 | Markdown支持、图片上传 | 中 |
| 协作功能 | 笔记分享、多人编辑 | 中 |
| 移动端适配 | 响应式设计 | 中 |

### 4.2 后端功能
| 模块 | 功能描述 | 优先级 |
|------|----------|--------|
| 用户API | 用户注册、登录、信息管理 | 高 |
| 笔记API | CRUD操作、权限控制 | 高 |
| 分类API | 文件夹、标签管理 | 高 |
| 文件存储 | 图片、附件上传管理 | 中 |
| 同步服务 | 多设备数据同步 | 中 |
| 消息队列 | 异步任务处理 | 低 |

### 4.3 人工智能功能
| 模块 | 功能描述 | 优先级 |
|------|----------|--------|
| 智能摘要 | 自动生成笔记摘要 | 高 |
| 关键词提取 | 提取笔记关键词 | 高 |
| 语义搜索 | 基于内容的智能搜索 | 高 |
| 分类推荐 | 自动分类建议 | 中 |
| 情感分析 | 分析笔记情感倾向 | 低 |
| 图像识别 | OCR文字识别 | 低 |

### 4.4 嵌入式功能
| 模块 | 功能描述 | 优先级 |
|------|----------|--------|
| 本地存储 | 离线笔记存储 | 高 |
| 同步功能 | 与云端同步 | 高 |
| 低功耗模式 | 电池优化 | 中 |
| 语音输入 | 语音转文字 | 中 |
| 墨水屏支持 | E-ink显示适配 | 低 |

## 5. 数据库设计

### 5.1 用户表 (users)
| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| id | UUID | PRIMARY KEY | 用户唯一标识 |
| email | VARCHAR(255) | UNIQUE, NOT NULL | 邮箱 |
| password | VARCHAR(255) | NOT NULL | 加密密码 |
| name | VARCHAR(100) | NOT NULL | 用户名 |
| created_at | TIMESTAMP | DEFAULT NOW() | 创建时间 |
| updated_at | TIMESTAMP | DEFAULT NOW() | 更新时间 |

### 5.2 笔记表 (notes)
| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| id | UUID | PRIMARY KEY | 笔记唯一标识 |
| user_id | UUID | FOREIGN KEY | 所属用户 |
| title | VARCHAR(255) | NOT NULL | 标题 |
| content | TEXT | - | 内容 |
| folder_id | UUID | FOREIGN KEY | 所属文件夹 |
| created_at | TIMESTAMP | DEFAULT NOW() | 创建时间 |
| updated_at | TIMESTAMP | DEFAULT NOW() | 更新时间 |

### 5.3 文件夹表 (folders)
| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| id | UUID | PRIMARY KEY | 文件夹唯一标识 |
| user_id | UUID | FOREIGN KEY | 所属用户 |
| name | VARCHAR(100) | NOT NULL | 文件夹名称 |
| parent_id | UUID | FOREIGN KEY | 父文件夹 |
| created_at | TIMESTAMP | DEFAULT NOW() | 创建时间 |

### 5.4 标签表 (tags)
| 字段 | 类型 | 约束 | 说明 |
|------|------|------|------|
| id | UUID | PRIMARY KEY | 标签唯一标识 |
| user_id | UUID | FOREIGN KEY | 所属用户 |
| name | VARCHAR(50) | NOT NULL | 标签名称 |

## 6. API接口设计

### 6.1 用户接口
| 方法 | 路径 | 描述 |
|------|------|------|
| POST | /api/auth/register | 用户注册 |
| POST | /api/auth/login | 用户登录 |
| GET | /api/users/me | 获取当前用户 |
| PUT | /api/users/me | 更新用户信息 |
| DELETE | /api/users/me | 删除用户 |

### 6.2 笔记接口
| 方法 | 路径 | 描述 |
|------|------|------|
| GET | /api/notes | 获取笔记列表 |
| POST | /api/notes | 创建笔记 |
| GET | /api/notes/:id | 获取笔记详情 |
| PUT | /api/notes/:id | 更新笔记 |
| DELETE | /api/notes/:id | 删除笔记 |

### 6.3 AI接口
| 方法 | 路径 | 描述 |
|------|------|------|
| POST | /api/ai/summary | 生成摘要 |
| POST | /api/ai/keywords | 提取关键词 |
| POST | /api/ai/search | 语义搜索 |

## 7. 部署方案

### 7.1 开发环境
```bash
# 启动后端
cd backend && npm run start:dev

# 启动前端
cd frontend && npm run dev

# 启动AI服务
cd ai && python main.py
```

### 7.2 生产环境
使用 Docker Compose 一键部署：
```bash
docker-compose up -d
```

## 8. 安全性考虑

| 安全项 | 措施 |
|--------|------|
| 用户认证 | JWT + 密码加密 |
| 数据传输 | HTTPS/TLS |
| 输入验证 | 参数校验 |
| SQL注入 | ORM参数化查询 |
| XSS攻击 | 前端转义 |
| 文件上传 | 类型检查、大小限制 |

## 9. 计划进度

| 阶段 | 时间 | 任务 |
|------|------|------|
| 第一阶段 | 第1-2周 | 后端API开发 |
| 第二阶段 | 第3-4周 | 前端界面开发 |
| 第三阶段 | 第5-6周 | AI功能集成 |
| 第四阶段 | 第7-8周 | 嵌入式开发 |
| 第五阶段 | 第9-10周 | 测试与部署 |

## 10. 风险评估

| 风险 | 等级 | 应对措施 |
|------|------|----------|
| AI模型性能 | 中 | 使用预训练模型，优化推理速度 |
| 嵌入式兼容性 | 中 | 选择主流硬件平台 |
| 数据同步冲突 | 中 | 实现版本控制和冲突检测 |
| 安全漏洞 | 高 | 定期安全审计，依赖更新 |

---

**文档版本**: v1.0  
**创建日期**: 2026-05-07  
**状态**: 待审批