# AS400-SDD Framework Lite

> Specification-Driven Development Framework for AS400 RPG Development with AI Assistance

## 概述

这是一套轻量级的 AS400 开发框架，核心理念是：

- **用模板驱动质量** — 规范化的 Spec 文档
- **用流程控制速度** — 简洁的 3 阶段流程
- **用清单保障一致** — Review 检查清单
- **双格式支持** — Fixed Format（旧版 RPG）和 Free Format（现代 RPGLE）

## 适用场景

- 封闭环境（仅有 GitHub Copilot + OpenCode CLI）
- 团队协作开发（5-15 人）
- 新功能开发为主
- 需要支持 Fixed Format（旧系统）和 Free Format（新开发）

## 快速开始

1. 克隆此仓库
2. 阅读 [入门指南](docs/getting-started.md)
3. 使用 [Spec 模板](templates/spec.md) 编写需求，**指定代码格式**
4. 使用 [Prompt 模板](prompts/) 生成代码
5. 按照 [Review 清单](templates/review-checklist.md) 审查代码（按对应格式检查）

## 目录结构

```
as400-sdd-framework-lite/
├── templates/           # 模板文件
│   ├── spec.md         # Spec 文档模板
│   ├── review-checklist.md  # Review 检查清单（支持 Fixed/Free）
│   ├── static-checks.md     # 团队静态检查规则
│   ├── code-format.md       # 代码格式规范（Fixed/Free）
│   └── prompt-library.md   # Prompt 库索引
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
  (指定代码格式)             │                    │
    │                      │                    │
    ├─────────────────────►│                    │
    │   领取任务            │                    │
    │                      │                    │
    │                      ▼                    │
    │                 Copilot 生成代码          │
    │                 (按指定格式)             │
    │                      │                    │
    │                      ├───────────────────►│
    │                      │   提交 PR         │
    │                      │                    │
    │                      │   Review 代码     │
    │                      │   (按对应格式检查)  │
    │                      │◄──────────────────┤
    │                      │   修改问题         │
    │                      │                    │
    ▼                      ▼                    ▼
  合并上线              测试验证            质量守门
```

## 代码格式支持

### Fixed Format（旧版 RPG）

传统 RPG 代码格式，基于列位置：

```rpgle
     C     *ENTRY        PLIST
     C                   PARM                    P_ORDNO      10
     C     P_ORDNO       CHAIN     ORDHDR                      90
     C                   IF        %FOUND
     C                   MOVEL     'A'         W_STATX
     C                   ENDIF
     C                   RETURN
```

**检查重点：**
- 列位置（1-80 列）
- 操作码位置（列 7-21）
- C-spec 格式

### Free Format（现代 RPGLE）

现代自由格式代码：

```rpgle
**FREE

DCL-PI MAIN;
  p_OrderNo CHAR(10);
END-PI;

chain p_OrderNo ORDHDR;
if %found;
  W_STATX = 'A';
endif;

return;
```

**检查重点：**
- `**FREE` 或 `/free` 声明
- 关键字大写
- 结构完整性（IF/ENDIF 配对）
- 缩进 2 空格

### 混用模式

- 主程序使用 Free Format
- 子程序/Factor 可以使用 Fixed Format
- 调用时用 `CALL` 指令

## 核心组件

| 组件 | 位置 | 用途 |
|------|------|------|
| **Spec 模板** | `templates/spec.md` | Team Leader 编写需求文档，**指定代码格式** |
| **代码格式规范** | `templates/code-format.md` | Fixed/Free 格式详细规范 |
| **静态检查规则** | `templates/static-checks.md` | 团队代码规范（可自定义） |
| **Review 清单** | `templates/review-checklist.md` | Review 检查项（按格式区分） |
| **Prompt 库** | `prompts/` | Copilot 生成 Prompt |

## 团队配置

### 角色分工

| 角色 | 职责 |
|------|------|
| Team Leader | 编写 Spec（**指定代码格式**），维护静态检查规则 |
| 开发者 | 按 Spec 指定的格式用 Copilot 生成代码 |
| Reviewer（轮流） | 按 Spec 指定的格式 Review 代码 |

### Spec 中必须指定代码格式

```markdown
## 代码格式
- [ ] Fixed Format（传统 RPG，基于列）
- [ ] Free Format（现代 RPGLE）
- [ ] 混用（主程序 Free，子程序 Fixed）
```

### Review 时按格式检查

| Spec 指定的格式 | Review 检查项 |
|-----------------|---------------|
| Fixed Format | Fixed Format 检查清单 |
| Free Format | Free Format 检查清单 |
| 混用 | 两者都检查 |

## License

MIT
