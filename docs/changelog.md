# 变更记录

所有框架相关的变更都记录在此文件。

格式：
- 版本号
- 日期
- 变更内容
- 变更人

---

## v1.0.0 - 2026-03-24

### 初始版本

#### 新增文件
- `README.md` — 项目介绍
- `templates/spec.md` — Spec 文档模板
- `templates/review-checklist.md` — Code Review 清单
- `templates/prompt-library.md` — Prompt 库索引
- `prompts/pgm/basic-read.md` — 读取文件程序 Prompt
- `prompts/pgm/basic-write.md` — 写入文件程序 Prompt
- `prompts/pgm/batch-process.md` — 批量处理程序 Prompt
- `prompts/spec/new-feature.md` — 新功能 Spec 辅助 Prompt
- `prompts/review/code-review.md` — 代码 Review 辅助 Prompt
- `docs/getting-started.md` — 入门指南
- `docs/faq.md` — 常见问题
- `examples/good/` — 好的示例（待补充）
- `examples/bad/common-errors.md` — 常见错误案例

#### 框架设计
- 确定 3 阶段流程：Spec → Copilot 生成 → Review
- 确定角色分工：Team Leader / 开发者 / Reviewer
- 确定基于 GitHub PR 的协作方式

---

## 变更记录模板

```markdown
## vX.Y.Z - YYYY-MM-DD

### 新增
- [文件/功能描述]

### 修改
- [文件/功能描述]

### 修复
- [问题描述]

### 废弃
- [功能/文件描述]
```
