# Prompt: 写入文件程序

## 任务
生成一个 RPGLE 程序，向 [文件名] 写入记录。

## 输入参数
| 参数 | 类型 | 方向 | 说明 |
|------|------|------|------|
| p_FieldA | CHAR(10) | IN | 字段A |
| p_FieldB | PACKED(15:2) | IN | 字段B |

## 业务规则
1. 写入前校验必填字段（FieldA 不能为空）
2. 写入前检查是否重复（CHAIN 检查键值）
3. 写入后更新相关统计
4. 需要事务控制（COMMIT）

## 上下文
- 文件定义：见 /inc/[文件名]_D.rpgle
- 错误处理参考：/src/ERRHDL.rpgle
- 代码风格参考：/src/PGM[参考程序].rpgle

## 要求
1. 使用 FREE 格式
2. 包含完整的错误处理（INFSPC）
3. 写入操作使用 COMMIT
4. 如果是新记录用 WRITE，如果是更新用 UPDATE
5. 使用 DCL-PRC 定义过程接口

## Copilot 注意事项 ⚠️
- [ ] 先 CHAIN 检查是否存在
- [ ] 不存在用 WRITE，存在用 UPDATE
- [ ] 操作前后判断文件状态
- [ ] 错误时 ROLLBACK
- [ ] 记录操作日志

## 禁止代码模式
```rpgle
// ❌ 错误：直接 WRITE 不检查
WRITE REFORMAT;

// ✅ 正确：先检查再决定
CHAIN KEYFIELD FILEA;
IF %FOUND;
  UPDATE FIELDR;
ELSE;
  WRITE FIELDR;
ENDIF;
```

## 输出格式
直接输出完整代码。
