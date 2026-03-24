# 入门指南

## 前提条件

- GitHub Copilot 可用（IDE 内或 CLI）
- Git 仓库已创建
- 团队成员了解 AS400/RPG 开发基础

## 快速开始（5 分钟）

### Step 1: 克隆项目

```bash
git clone <your-repo-url>
cd as400-sdd-framework
```

### Step 2: 了解项目结构

```
as400-sdd-framework/
├── templates/           # 模板文件
│   ├── spec.md         # Spec 文档模板
│   └── review-checklist.md  # Review 检查清单
├── prompts/            # Prompt 模板库
│   ├── pgm/           # 程序生成 Prompt
│   ├── spec/          # Spec 编写 Prompt
│   └── review/        # Review Prompt
└── docs/               # 文档（本文件）
```

### Step 3: 阅读核心文档

1. [Spec 模板](../templates/spec.md) — 了解 Spec 文档结构
2. [Review 清单](../templates/review-checklist.md) — 了解代码检查项
3. [Prompt 库索引](../templates/prompt-library.md) — 了解可用 Prompt

### Step 4: 开始使用

#### 编写 Spec

1. Team Leader 创建新文件：`specs/YYYYMMDD-feature-name.md`
2. 基于 `templates/spec.md` 填写
3. 确保包含 Copilot 生成规则

#### 生成代码

1. 开发者阅读 Spec
2. 从 `prompts/pgm/` 选择合适的 Prompt
3. 复制 Prompt 到 Copilot，填入实际参数
4. 根据输出生成代码

#### Code Review

1. 开发者提交 PR
2. Reviewer 打开 `templates/review-checklist.md`
3. 逐项检查
4. 在 PR Comment 中反馈问题

---

## 角色指南

### Team Leader

**职责：**
- 编写规范化的 Spec 文档
- 把控需求质量和优先级
- 维护 Copilot 生成规则

**开始步骤：**
1. 阅读 [Spec 模板说明](../templates/spec.md)
2. 用 [Spec 辅助 Prompt](../prompts/spec/new-feature.md) 生成第一个 Spec
3. 根据实际项目调整 Copilot 生成规则

### 开发者

**职责：**
- 理解 Spec 文档
- 使用 Copilot 生成代码
- 根据 Review 反馈修复问题

**开始步骤：**
1. 阅读 [Prompt 库索引](../templates/prompt-library.md)
2. 选择合适的 Prompt 模板
3. 在 Copilot 中使用模板生成代码
4. 提交 PR 前自查代码

### Reviewer

**职责：**
- 按 Review 清单检查代码
- 记录 Copilot 幻觉问题
- 反馈给 Team Leader

**开始步骤：**
1. 阅读 [Review 清单](../templates/review-checklist.md)
2. 打印或保存清单到本地
3. PR Review 时逐项检查

---

## 常见问题

### Q: Team Leader 不熟悉新流程怎么办？

A: 建议进行 30 分钟培训，内容包括：
- Spec 模板讲解（15 分钟）
- 演示用模板写一个 Spec（10 分钟）
- Q&A（5 分钟）

### Q: 开发者不熟悉 Copilot 怎么办？

A: 建议进行 30 分钟培训，内容包括：
- 新流程介绍（5 分钟）
- Copilot 生成演示（10 分钟）
- Review 清单讲解（10 分钟）
- Q&A（5 分钟）

### Q: Copilot 生成质量不好怎么办？

A: 按以下步骤排查：
1. 检查 Spec 是否提供了足够的上下文
2. 检查 Prompt 是否明确禁止事项
3. 是否提供了文件定义源码路径
4. 收集具体问题，反馈给 Team Leader 更新 Spec

### Q: 如何处理 Copilot 幻觉问题？

A: 记录到 Review 反馈表，反馈给 Team Leader：
- 问题描述
- 猜测原因（哪个上下文缺失）
- 建议改进（更新 Spec / 更新 Prompt）

### Q: 现有项目如何接入？

A: 建议分阶段：
1. 新功能开始使用新流程
2. 重要修改可以回退到新流程重写
3. 维护性修改暂不强制，等有精力再迁移

---

## 下一步

- 查看 [常见错误案例](../examples/bad/common-errors.md)
- 查看 [好的示例](../examples/good/)
- 加入团队日常开发实践
