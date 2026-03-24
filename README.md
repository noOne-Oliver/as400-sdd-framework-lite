# AS400-SDD Framework Lite

> Specification-Driven Development Framework for AS400 RPG Development with AI Assistance

## 概述

这是一套轻量级的 AS400 开发框架，核心理念是：

- **用模板驱动质量** — 规范化的 Spec 文档
- **用流程控制速度** — 简洁的 3 阶段流程
- **用清单保障一致** — Review 检查清单
- **用 Fix Format 提升效率** — 自动修复格式问题

## 适用场景

- 封闭环境（仅有 GitHub Copilot + OpenCode CLI）
- 团队协作开发（5-15 人）
- 新功能开发为主
- 需要在保证质量的前提下提升开发速度

## 快速开始

1. 克隆此仓库
2. 阅读 [入门指南](docs/getting-started.md)
3. 使用 [Spec 模板](templates/spec.md) 编写需求
4. 使用 [Prompt 模板](prompts/) 生成代码
5. 按照 [Review 清单](templates/review-checklist.md) 审查代码

## 目录结构

```
as400-sdd-framework-lite/
├── templates/           # 模板文件
│   ├── spec.md         # Spec 文档模板
│   ├── review-checklist.md  # Review 检查清单（含 Fix Format）
│   ├── static-checks.md     # 团队静态检查规则
│   └── prompt-library.md   # Prompt 库索引
├── prompts/            # Prompt 模板库
│   ├── pgm/           # 程序生成 Prompt
│   ├── spec/          # Spec 编写 Prompt
│   └── review/        # Review Prompt
│       ├── code-review.md  # 检查模式
│       └── fix-format.md  # 修复模式
├── docs/               # 文档
│   ├── getting-started.md
│   └── faq.md
└── examples/           # 示例
    ├── good/          # 好的示例
    └── bad/           # 常见错误示例
```

## 核心流程

```
Team Leader              开发者              Reviewer
    │                      │                    │
    ▼                      │                    │
  写 Spec                   │                    │
    │                      │                    │
    ├─────────────────────►│                    │
    │   领取任务            │                    │
    │                      │                    │
    │                      ▼                    │
    │                 Copilot 生成代码          │
    │                      │                    │
    │                      ├───────────────────►│
    │                      │   提交 PR         │
    │                      │                    │
    │                      │   Review 代码     │
    │                      │◄──────────────────┤
    │                      │   Fix Format（如需）│
    │                      │   修改问题         │
    │                      │                    │
    ▼                      ▼                    ▼
  合并上线              测试验证            质量守门
```

## 两种 Review 模式

### 检查模式（Review）
- 使用 `code-review.md`
- 目的：发现问题、记录问题
- 输出：问题列表 + 修复建议

### 修复模式（Fix Format）
- 使用 `fix-format.md`
- 目的：自动修复格式问题
- 输出：修复后的代码

## 核心组件

| 组件 | 位置 | 用途 |
|------|------|------|
| **Spec 模板** | `templates/spec.md` | Team Leader 编写需求文档 |
| **静态检查规则** | `templates/static-checks.md` | 团队代码规范（可自定义） |
| **Review 清单** | `templates/review-checklist.md` | Review 检查项 + Fix Format |
| **Prompt 库** | `prompts/` | Copilot 生成 Prompt |

## 团队配置

### 角色分工

| 角色 | 职责 |
|------|------|
| Team Leader | 编写 Spec，维护静态检查规则 |
| 开发者 | 拿 Spec 用 Copilot 生成代码 |
| Reviewer（轮流） | Review 代码 + Fix Format（如需） |

### Spec 编写规则

Team Leader 编写 Spec 时，必须包含：

1. **业务规则** — 完整的校验逻辑
2. **数据库设计** — PF/LF 文件的字段定义
3. **程序结构** — 关键逻辑的位置描述
4. **Copilot 注意事项** — 专门防止生成质量问题

详见 [Spec 模板说明](templates/spec.md)

### 静态检查规则

`templates/static-checks.md` 用于定义团队内部的静态检查规范，包括：

- 命名规范（程序/文件/字段）
- 代码格式（缩进/注释/大小写）
- RPG 特定规范（FREE 格式/错误处理）
- 安全检查（硬编码/SQL 注入）
- 性能检查（循环内查询/大数据量）

详见 [静态检查规则](templates/static-checks.md)

### Review 规则

1. 所有高严重度问题必须修复
2. Fix Format 问题可直接接受 Copilot 建议
3. Copilot 幻觉问题需记录反馈
4. 至少 1 人 Approve 才能合并

详见 [Review 清单](templates/review-checklist.md)

## License

MIT
