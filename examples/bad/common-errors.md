# Copilot 生成常见错误案例

本文档收集 Copilot 生成 RPG 代码时的常见错误，供团队学习和预防。

---

## 1. 字段幻觉

### 问题描述
Copilot 生成引用不存在字段的代码。

### 错误示例
```rpgle
// ❌ 错误：OHCUSTN 是幻觉字段，实际是 OHCUST
CHAIN (OHORD#: OHCUSTN) ORDHDR;
IF %FOUND;
  DSPLY OHCUSTN;  // 编译失败！
ENDIF;
```

### 正确写法
```rpgle
// ✅ 正确：使用文件定义中实际存在的字段
CHAIN (OHORD#: OHCUST) ORDHDR;
IF %FOUND;
  DSPLY OHCUST;
ENDIF;
```

### 预防措施
- Spec 必须提供文件定义源码路径
- 生成后对照文件定义检查所有字段引用
- 在 Copilot Prompt 中明确禁止"创造"字段

---

## 2. 缺少错误处理

### 问题描述
文件操作前不判断状态，异常时无感知。

### 错误示例
```rpgle
// ❌ 错误：直接 CHAIN，不判断文件状态
CHAIN KEYFIELD FILEA;
IF %FOUND;
  // 处理
ENDIF;
```

### 正确写法
```rpgle
// ✅ 正确：先判断文件状态，再操作
/free
  chain keyfield FILEA;
  if %found;
    // 处理
  else;
    // 处理不存在
    except ERRLOG;
  endif;
```

### 预防措施
- 在 Spec 的 Copilot 生成规则中明确要求
- Review 时重点检查 INFSPC 错误处理

---

## 3. 事务控制缺失

### 问题描述
多文件操作时不使用 COMMIT/ROLLBACK，导致数据不一致。

### 错误示例
```rpgle
// ❌ 错误：多个文件更新，但没有事务控制
UPDATE ORDHDRR;  // 可能成功
UPDATE ORDDETR;  // 可能失败，导致数据不一致
```

### 正确写法
```rpgle
// ✅ 正确：使用事务控制
/copy qsysinc,sqlrc
EXEC SQL SET TRANSACTION ISOLATION LEVEL UR;
EXEC SQL UPDATE ORDHDR SET ...;
if sqlState = '00000';
  EXEC SQL UPDATE ORDDET SET ...;
  if sqlState = '00000';
    EXEC SQL COMMIT;
  else;
    EXEC SQL ROLLBACK;
  endif;
endif;
```

### 预防措施
- 在 Spec 的"事务规则"中明确是否需要事务控制
- 涉及多文件更新时必须开启 COMMIT

---

## 4. 死循环

### 问题描述
READE 循环没有推进记录位置，导致死循环。

### 错误示例
```rpgle
// ❌ 错误：READE 在循环内，但没有推进
read(e) key field FILEA;
dow not %eof;
  // 处理
  // 忘记 READE 或 LEAVE
enddo;
```

### 正确写法
```rpgle
// ✅ 正确：循环内读取下一条
setll *loval FILEA;
reade *loval FILEA;
dow not %eof;
  // 处理
  reade FILEA;
enddo;
```

### 预防措施
- 在 Prompt 中强调使用 SETGT + READE 模式
- Review 时检查所有循环是否有退出条件

---

## 5. 字符处理不当

### 问题描述
字符字段比较时未去除空格，导致逻辑错误。

### 错误示例
```rpgle
// ❌ 错误：直接比较，可能因空格导致判断错误
if OHSTAT = 'A';
  // 处理
endif;
```

### 正确写法
```rpgle
// ✅ 正确：使用 %trim 处理空格
if %trim(OHSTAT) = 'A';
  // 处理
endif;

// 或者在比较前处理
OHSTAT_T = %trim(OHSTAT);
if OHSTAT_T = 'A';
```

### 预防措施
- 在 Spec 中说明哪些字段可能包含前后空格
- Review 时检查字符比较是否有 TRIM 处理

---

## 6. 日期格式混淆

### 问题描述
YYYYMMDD 和 YYYY-MM-DD 格式混用，或日期计算错误。

### 错误示例
```rpgle
// ❌ 错误：日期格式混用
if OHDATE = '2026-03-24';  // OHDATE 是 8 位数值，不是这种格式
```

### 正确写法
```rpgle
// ✅ 正确：使用正确的日期格式
if OHDATE = 20260324;  // 数值比较
// 或者
if %char(OHDATE: *ISO0) = '20260324';
```

### 预防措施
- 在 Spec 中明确日期字段的格式（数值还是字符）
- 说明日期计算规则（%DATE, %DIFF, etc）

---

## 7. 参数传递错误

### 问题描述
调用程序时参数类型或长度不匹配。

### 错误示例
```rpgle
// ❌ 错误：参数长度不匹配
DCL-PRC P1;
  p_code CHAR(5);  // 定义为 5 位
END-PRC;

DCL-PRC P2;
  p_code CHAR(10);  // 但传入 10 位
END-PRC;
```

### 正确写法
```rpgle
// ✅ 正确：确保参数定义一致
// 调用方
DCL-PRC P1;
  p_code CHAR(10);
END-PRC;

// 被调用方
DCL-PRC P1;
  p_code CHAR(10);
END-PRC;
```

### 预防措施
- Spec 中完整列出参数定义
- Review 时核对调用方和被调用方的参数定义

---

## 8. 数组越界

### 问题描述
数组操作时索引超出范围。

### 错误示例
```rpgle
// ❌ 错误：循环读取到超出数组范围
for i = 1 to 100;
  if i > %elem(arr);  // 可能已经越界
    leave;
  endif;
  arr(i) = field;
endfor;
```

### 正确写法
```rpgle
// ✅ 正确：使用 %lookuplt 或检查边界
for i = 1 to %elem(arr);
  if %eof(FILEA);
    leave;
  endif;
  arr(i) = field;
  read FILEA;
endfor;
```

### 预防措施
- 涉及数组操作时在 Spec 中说明大小限制
- Review 时检查数组边界处理

---

## 如何贡献

发现新的错误案例时：
1. 记录到本文档
2. 更新 [Spec 模板](../templates/spec.md) 的 Copilot 生成规则
3. 更新 [Review 清单](../templates/review-checklist.md) 的专项检查
