# Prompt 库索引

## 目录结构

```
prompts/
├── pgm/           # 程序生成 Prompt
│   ├── basic-read.md       # 读取文件程序
│   ├── basic-write.md      # 写入文件程序
│   └── batch-process.md    # 批量处理程序
├── spec/          # Spec 编写 Prompt
│   └── new-feature.md      # 新功能 Spec
└── review/        # Review Prompt
    └── code-review.md      # 代码 Review
```

## 程序生成 Prompt

### basic-read.md
用于生成读取文件/查询类的程序。
- 适用场景：查询、报表数据读取
- 输入：文件名、查询条件、输出格式
- 输出：RPGLE 程序代码

### basic-write.md
用于生成写入文件/更新类的程序。
- 适用场景：新增记录、修改记录、删除记录
- 输入：文件名、操作类型、业务规则
- 输出：RPGLE 程序代码

### batch-process.md
用于生成批量处理类的程序。
- 适用场景：批量更新、迁移、夜间批处理
- 输入：源文件、目标文件、处理逻辑
- 输出：RPGLE 程序代码

## Spec 编写 Prompt

### new-feature.md
用于辅助编写 Spec 文档。
- 适用场景：从需求描述生成规范 Spec
- 输入：原始需求
- 输出：结构化 Spec 草稿

## Review Prompt

### code-review.md
用于 Copilot 辅助代码 Review。
- 适用场景：PR Review、代码自查
- 输入：代码 + Spec 摘要
- 输出：问题列表 + 建议

---

## 使用方法

### 方式 1：直接复制使用

1. 打开对应的 Prompt 文件
2. 复制内容到 Copilot Chat
3. 根据实际情况修改 [] 部分的内容
4. 发送并生成结果

### 方式 2：作为模板参考

1. 阅读 Prompt 了解结构和要求
2. 根据项目实际情况调整 Prompt 内容
3. 保存为项目专属的 Prompt 变体

---

## Prompt 编写原则

| 原则 | 说明 |
|------|------|
| 提供上下文 | 始终提供文件定义、参考代码路径 |
| 明确格式要求 | 指定 FREE/传统、命名规范 |
| 列出禁止事项 | 说明 Copilot 容易出错的地方 |
| 分步骤描述 | 用编号描述执行顺序 |

---

## 常见问题

**Q: Copilot 生成的结果不理想怎么办？**
A: 1) 检查是否提供了足够的上下文 2) 明确禁止事项 3) 分步骤发送而不是一次生成

**Q: 如何生成项目专属的 Prompt？**
A: 基于现有模板，根据团队代码风格修改"禁止代码模式"和"格式要求"部分

**Q: Prompt 需要经常更新吗？**
A: 根据 Review 反馈更新。当发现 Copilot 反复出现同一类错误时，在 Prompt 中明确禁止
