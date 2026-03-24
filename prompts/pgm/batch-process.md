# Prompt: 批量处理程序

## 任务
生成一个 RPGLE 批量处理程序。

## 处理逻辑
1. 从 [源文件] 读取待处理记录（条件：STAT = 'P'）
2. 对每条记录调用 [处理程序]
3. 成功后更新 STAT = 'C'，失败更新 STAT = 'E' + 错误原因
4. 每 [1000] 条记录 COMMIT 一次

## 上下文
- 源文件：/inc/[源文件]_D.rpgle
- 错误文件：/inc/ERRLOG_D.rpgle
- 处理程序：PGM[XXX]
- 错误处理：写 ERRLOG 表

## 程序结构
```
BATCH001
├── 01. 初始化
│   ├── 获取批次号（BTHSEQ）
│   ├── 读取处理参数
│   └── 设置 COMMIT=*YES
│
├── 02. 主循环（SETGT + READE）
│   ├── 读取待处理记录
│   ├── 调用处理程序
│   ├── 更新状态
│   └── 每1000条 COMMIT
│
├── 03. 异常处理
│   ├── 捕获异常
│   ├── ROLLBACK
│   ├── 记录错误表 ERRLOG
│   └── 继续下一条
│
└── 04. 结束
    ├── 打印处理报告
    └── 更新批次状态
```

## 要求
1. 使用递归读取（SETGT + READE）
2. 包含批次号和进度日志
3. 异常时 ROLLBACK 并继续
4. 结束时打印处理报告（成功数/失败数/耗时）

## Copilot 注意事项 ⚠️
- [ ] 使用 SETGT + READE 避免重复读取
- [ ] 每N条 COMMIT 防止长事务锁表
- [ ] 错误记录包含批次号、记录键值、错误原因
- [ ] 失败后记录错误表，然后 CONTINUE 不要 ABORT

## 禁止代码模式
```rpgle
// ❌ 错误：处理失败就停止
READE KEY FIELD;
DOW NOT %EOF;
  GOTO C10;  // 不要用 GOTO
ENDDO;

// ✅ 正确：失败继续处理
READE KEY FIELD;
DOW NOT %EOF;
  MONITOR;
    CALL 'PGMX' PARM(p1: p2);
    UPDATE REPTFR;
  ON-ERROR;
    EVAL RTERR = 'Y';
    UPDATE REPTFR;
  ENDMON;
  READE KEY FIELD;
ENDDO;
```

## 输出格式
直接输出完整代码。
