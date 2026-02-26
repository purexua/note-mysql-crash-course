# Chapter 21 — 创建和操纵表

## 练习题

### 练习 21.1

**题目：** 在vendors表中添加名为vend_web的网站列。你需要一个足够大的文本字段来容纳 URL。

**答案：**

```sql
ALTER TABLE vendors
ADD vend_web VARCHAR(255);
```

**说明：** `ALTER TABLE` 用于修改已有表结构，`ADD` 添加新列。URL 通常不超过 255 个字符，`VARCHAR(255)` 是合适的选择，未填写时默认为 NULL。

---

### 练习 21.2

**题目：** 使用UPDATE语句更新 vendors表记录，以便加入网站（你可以编造任何地址）​。

**答案：**

```sql
UPDATE vendors SET vend_web = 'https://www.anvils.com'    WHERE vend_id = 1001;
UPDATE vendors SET vend_web = 'https://www.ltsupplies.com' WHERE vend_id = 1002;
UPDATE vendors SET vend_web = 'https://www.acme.com'       WHERE vend_id = 1003;
UPDATE vendors SET vend_web = 'https://www.furball.com'    WHERE vend_id = 1004;
UPDATE vendors SET vend_web = 'https://www.jetset.com'     WHERE vend_id = 1005;
UPDATE vendors SET vend_web = 'https://www.jouets.com'     WHERE vend_id = 1006;
```

**说明：** 每条 UPDATE 语句通过 WHERE 精确定位到单个供应商，逐一更新 vend_web 字段。务必使用 WHERE 子句，否则会将所有供应商的网址更新为同一个值。

---
