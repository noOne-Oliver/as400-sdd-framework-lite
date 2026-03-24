# AS400-SDD Framework

> Specification-Driven Development Framework for AS400 RPG Development with AI Assistance

## 概述

这是一套轻量级的 AS400 开发框架，核心理念是：

- **用模板驱动质量** — 规范化的 Spec 文档
- **用流程控制速度** — 简洁的 3 阶段流程
- **用清单保障一致** — Review 检查清单

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
as400-sdd-framework/
├── templates/           # 模板文件
│   ├── spec.md         # Spec 文档模板
│   └── review-checklist.md  # Review 检查清单
├── prompts/            # Prompt 模板库
│   ├── pgm/           # 程序生成 Prompt
│   ├── spec/          # Spec 编写 Prompt
│   └── review/        # Review Prompt
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
    │                      │   修改问题         │
    │                      │                    │
    │                      ├───────────────────►│
    │                      │   Approve         │
    │                      │                    │
    ▼                      ▼                    ▼
  合并上线              测试验证            质量守门
```

## 团队配置

### 角色分工

| 角色 | 职责 |
|------|------|
| Team Leader | 编写 Spec，守住需求关 |
| 开发者 | 拿 Spec 用 Copilot 生成代码 |
| Reviewer（轮流） | 用清单 Review PR |

### Spec 编写规则

Team Leader 编写 Spec 时，必须包含：

1. **业务规则** — 完整的校验逻辑
2. **数据库设计** — PF/LF 文件的字段定义
3. **程序结构** — 关键逻辑的位置描述
4. **Copilot 注意事项** — 专门防止生成质量问题

详见 [Spec 模板说明](templates/spec.md)

### Copilot 使用规则

1. 始终提供文件定义源码路径
2. 使用 FREE 格式 RPGLE
3. 包含完整的错误处理
4. 参考现有代码风格

详见 [Prompt 库](prompts/)

### Review 规则

1. 所有高严重度问题必须修复
2. Copilot 幻觉问题需记录反馈
3. 至少 1 人 Approve 才能合并

详见 [Review 清单](templates/review-checklist.md)

## License

MIT
