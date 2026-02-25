# Chapter 18 — 全文搜索

## 练习题

### 练习 18.1

**题目：** 编写一个SQL语句，使用全文搜索返回包含词safe 但不包含词handsaw的所有行。

**答案：**

```sql
SELECT note_text
FROM productnotes
WHERE MATCH(note_text) AGAINST('+safe -handsaw' IN BOOLEAN MODE);
```

**说明：** 布尔模式下，`+` 表示必须包含，`-` 表示必须排除。`+safe -handsaw` 即返回含 safe 且不含 handsaw 的行。

---

### 练习 18.2

**题目：** 编写一个SQL语句，使用全文搜索返回包含词drop、dropped、dropping以及任何以drop 开头的其他词的所有行。

**答案：**

```sql
SELECT note_text
FROM productnotes
WHERE MATCH(note_text) AGAINST('+drop*' IN BOOLEAN MODE);
```

**说明：** 布尔模式下，`+` 表示必须包含，`*` 是截断通配符，`+drop*` 即返回含 drop、dropped、dropping 等所有以 drop 开头的词。

---
