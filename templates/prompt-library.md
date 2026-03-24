# Prompt 库索引 v2.0

## 目录结构

```
prompts/
├── pgm/           # 程序生成 Prompt
│   ├── basic-read.md       # 读取文件程序
│   ├── basic-write.md      # 写入文件程序
│   └── batch-process.md    # 批量处理程序
├── spec/          # Spec 编写 Prompt
│   └── new-feature.md      # 新功能 Spec
├── review/        # Review Prompt
│   ├── code-review.md      # 代码 Review（检查模式）
│   └── fix-format.md       # 代码格式修复（修复模式）
```

---

## 两种模式

### 检查模式（Review）
- 使用 `review/code-review.md`
- 目的：发现问题、记录问题
- 输出：问题列表 + 修复建议

### 修复模式（Fix Format）
- 使用 `review/fix-format.md`
- 目的：自动修复格式问题
- 输出：修复后的代码

---

## 使用流程

### 场景 1：PR Review（先检查后修复）

```
1. 使用 code-review.md 检查代码
   ↓
2. 发现格式问题 → 使用 fix-format.md 生成修复
   ↓
3. 开发者确认修复
   ↓
4. Reviewer 最终 Approve
```

### 场景 2：快速格式修复

```
开发者：发现代码格式不规范
   ↓
使用 fix-format.md 生成修复建议
   ↓
确认修复结果
   ↓
提交更新
```

---

## Review Prompt 文档

### code-review.md
用于 Review 的检查模式。

**适用场景：**
- PR Review（主要用途）
- 代码自查
- 上线前检查

**检查内容：**
1. 正确性（字段引用、逻辑判断）
2. 安全性（硬编码、SQL 注入）
3. 性能（循环内查询、大数据量）
4. 代码质量（命名、注释）
5. Copilot 幻觉专项

### fix-format.md
用于 Review 的修复模式。

**适用场景：**
- 格式不规范但逻辑正确
- 缩进/空格/大小写问题
- 结构不完整（缺少 END）

**修复内容：**
- 缩进统一为 2 空格
- 关键字大写
- 字符串引号统一
- 结构完整性
- 空格规范

**不修复内容：**
- ❌ 业务逻辑
- ❌ 变量名/字段名
- ❌ 代码顺序
- ❌ 功能逻辑

---

## 选择指南

| 场景 | 推荐 Prompt |
|------|------------|
| PR Review | code-review.md |
| 发现格式问题 | fix-format.md |
| 代码自查 | code-review.md |
| 批量格式修复 | fix-format.md |
| 新功能开发 | code-review.md（开发后检查） |

---

## 常见问题

**Q: Fix Format 会改变代码逻辑吗？**
A: 不会。Fix Format 只修复格式，不修改任何逻辑。但建议修复后重新 Review 确认。

**Q: 什么时候用检查模式，什么时候用修复模式？**
A: 建议先用 code-review.md 检查全部问题，发现格式问题后再用 fix-format.md 修复。也可以只使用 code-review.md，让开发者手动修复格式问题。

**Q: Fix Format 能修复所有格式问题吗？**
A: 不能。只能修复：缩进、关键字大小写、引号、结构完整性、空格规范。其他问题（如命名不规范）需要手动修复。

**Q: 如何区分格式问题和逻辑问题？**
A: 格式问题不影响程序运行结果，只影响代码可读性。逻辑问题会影响程序运行结果。如果不确定，先用 code-review.md 检查。
