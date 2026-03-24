# 代码格式规范

> 本文件定义 RPG 代码的格式标准，支持 Fixed Format 和 Free Format 两种模式。

---

## 格式选择

在 Spec 中指定代码格式：

```markdown
## 代码格式
- [ ] Fixed Format（传统 RPG，基于列）
- [ ] Free Format（现代 RPGLE）
- [ ] 混用（主程序 Free，子程序 Fixed）
```

---

## Fixed Format（传统 RPG）

### 特征
- 代码写在特定列位置（6-80 列）
- 使用 C-spec 描述逻辑
- 关键字在列 7-21
- 操作符在列 26-35
-  continuation 字符在列 6

### 列定义

| 列 | 用途 | 说明 |
|-----|------|------|
| 1-5 | 顺序号 | 可选 |
| 6 | Continuation / 注释 | * = 继续，/ = 注释 |
| 7-21 | 关键字 | 操作说明 |
| 22-25 | 描述符 | Factor 1 |
| 26-35 | 操作符 | 操作码 |
| 36-50 | 操作数1 | Factor 2 |
| 51-80 | 操作数2 | Result |

### Fixed Format 示例

```rpgle
     DSPF  ORDMAIN                 E             WORKSTN
     E                    1   1   RECD
     E                    1   2   FIELDS
     E                    1   1   SFLCTL
     E                    1   2   SFL
     E                    1   2   SFLEND
     E                    1   1   SUBFILE
     E                    1   2   SUBFILE1
     E                    1   2   SUBFILE2
     E                    1   2   SUBFILE3
     E                    1   2   SUBFILE4
     E                    1   2   SUBFILE5
     E                    1   2   SUBFILE6
     E                    1   2   SUBFILE7
     E                    1   2   SUBFILE8
     E                    1   2   SUBFILE9
     E                    1   2   SUBFILE10
     E                    1   2   SUBFILE11
     E                    1   2   SUBFILE12
     E                    1   2   SUBFILE13
     E                    1   2   SUBFILE14
     E                    1   2   SUBFILE15
     E                    1   2   SUBFILE16
     E                    1   2   SUBFILE17
     E                    1   2   SUBFILE18
     E                    1   2   SUBFILE19
     E                    1   2   SUBFILE20
     E                    1   2   SUBFILE21
     E                    1   2   SUBFILE22
     E                    1   2   SUBFILE23
     E                    1   2   SUBFILE24
     E                    1   2   SUBFILE25
     E                    1   2   SUBFILE26
     E                    1   2   SUBFILE27
     E                    1   2   SUBFILE28
     E                    1   2   SUBFILE29
     E                    1   2   SUBFILE30
     E                    1   2   SUBFILE31
     E                    1   2   SUBFILE32
     E                    1   2   SUBFILE33
     E                    1   2   SUBFILE34
     E                    1   2   SUBFILE35
     E                    1   2   SUBFILE36
     E                    1   2   SUBFILE37
     E                    1   2   SUBFILE38
     E                    1   2   SUBFILE39
     E                    1   2   SUBFILE40
     E                    1   2   SUBFILE41
     E                    1   2   SUBFILE42
     E                    1   2   SUBFILE43
     E                    1   2   SUBFILE44
     E                    1   2   SUBFILE45
     E                    1   2   SUBFILE46
     E                    1   2   SUBFILE47
     E                    1   2   SUBFILE48
     E                    1   2   SUBFILE49
     E                    1   2   SUBFILE50
     E                    1   2   SUBFILE51
     E                    1   2   SUBFILE52
     E                    1   2   SUBFILE53
     E                    1   2   SUBFILE54
     E                    1   2   SUBFILE55
     E                    1   2   SUBFILE56
     E                    1   2   SUBFILE57
     E                    1   2   SUBFILE58
     E                    1   2   SUBFILE59
     E                    1   2   SUBFILE60
     E                    1   2   SUBFILE61
     E                    1   2   SUBFILE62
     E                    1   2   SUBFILE63
     E                    1   2   SUBFILE64
     E                    1   2   SUBFILE65
     E                    1   2   SUBFILE66
     E                    1   2   SUBFILE67
     E                    1   2   SUBFILE68
     E                    1   2   SUBFILE69
     E                    1   2   SUBFILE70
     E                    1   2   SUBFILE71
     E                    1   2   SUBFILE72
     E                    1   2   SUBFILE73
     E                    1   2   SUBFILE74
     E                    1   2   SUBFILE75
     E                    1   2   SUBFILE76
     E                    1   2   SUBFILE77
     E                    1   2   SUBFILE78
     E                    1   2   SUBFILE79
     E                    1   2   SUBFILE80
     E                    1   2   SUBFILE81
     E                    1   2   SUBFILE82
     E                    1   2   SUBFILE83
     E                    1   2   SUBFILE84
     E                    1   2   SUBFILE85
     E                    1   2   SUBFILE86
     E                    1   2   SUBFILE87
     E                    1   2   SUBFILE88
     E                    1   2   SUBFILE89
     E                    1   2   SUBFILE90
     E                    1   2   SUBFILE91
     E                    1   2   SUBFILE92
     E                    1   2   SUBFILE93
     E                    1   2   SUBFILE94
     E                    1   2   SUBFILE95
     E                    1   2   SUBFILE96
     E                    1   2   SUBFILE97
     E                    1   2   SUBFILE98
     E                    1   2   SUBFILE99
     E                    1   2   SUBFILE100
```

### Fixed Format 检查项

| 检查项 | 规范 | 必须修复 |
|--------|------|----------|
| 列位置 | 代码必须在 1-80 列内 | [ ] |
| 关键字位置 | 操作码必须在列 7-21 | [ ] |
| 续行符 | 超过 80 列用 * 续行 | [ ] |
| 注释列 | 列 1 用 / 或 * | [ ] |
| C-spec | 逻辑行必须以 C 开头 | [ ] |

---

## Free Format（现代 RPGLE）

### 特征
- 类似 Java/Python 的写法
- 不需要列位置限制
- 使用 `/free` 或 `**FREE` 声明
- END-xxx 结构替代 C-spec

### Free Format 示例

```rpgle
**FREE

DCL-F ORDHDR keyed;
DCL-F ORDDET keyed;

DCL-PI MAIN;
  p_OrderNo CHAR(10);
END-PI;

chain p_OrderNo ORDHDR;
if %found;
  dsply ('Order found: ' + p_OrderNo);
else;
  dsply ('Order not found: ' + p_OrderNo);
endif;

*inlr = *on;
return;
```

### Free Format 检查项

| 检查项 | 规范 | 必须修复 |
|--------|------|----------|
| 声明 | 必须有 `**FREE` 或 `/free` | [ ] |
| 关键字 | 大写（IF/ELSE/ENDIF/DCL/etc） | [ ] |
| 结构 | IF 必须有 ENDIF，DO 必须有 ENDDO | [ ] |
| 缩进 | 2 空格缩进 | [ ] |
| 引号 | 单引号 | [ ] |

---

## 混用模式

### 规则
- 主程序使用 Free Format
- 子程序/Factor 可以使用 Fixed Format
- 禁止混合在同一行

### 示例

```rpgle
**FREE

// 主程序逻辑 - Free Format
DCL-PI MAIN;
END-PI;

call 'S_PROC1';  // 调用 Fixed Format 子程序

*inlr = *on;
return;

// S_PROC1 - Fixed Format
     S_PROC1    B

     C                   MOVE      *ON           *INLR

     C                   SETON                                        LR
```

---

## 选择指南

| 场景 | 推荐格式 |
|------|----------|
| 新开发功能 | Free Format |
| 维护旧系统 | Fixed Format 或混用 |
| 新子程序被旧程序调用 | Fixed Format |
| 独立新模块 | Free Format |
| 团队统一规范 | Free Format（推荐） |

---

## 更新记录

| 版本 | 日期 | 修改内容 |
|------|------|----------|
| v1.0 | ___ | 初始版本 |
