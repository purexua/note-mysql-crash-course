# Chapter 4 — 检索数据

## 练习题

### 练习 4.1

**题目：** 编写一个 SQL 语句，从 `customers` 表中检索所有的顾客 ID（`cust_id`）。

**答案：**

```sql
SELECT cust_id
FROM customers;
```

**说明：** 最基本的 `SELECT` 用法，指定列名而非 `*`，只取需要的列。

---

### 练习 4.2

**题目：** `orderitems` 表包含了所有已订购的产品（有些已被订购多次）。编写一个 SQL 语句，检索并列出已订购产品（`prod_id`）的清单（不用列出每笔订单，只列出不同产品的清单）。提示：最终应该显示 9 行。

**答案：**

```sql
SELECT DISTINCT prod_id
FROM orderitems;
```

**说明：** `DISTINCT` 关键字作用于其后所有列，去除重复行，确保每种产品只出现一次。

---

### 练习 4.3

**题目：** 编写一个 SQL 语句，检索 `customers` 表中的所有列，再编写另一个 `SELECT` 语句，只检索顾客 ID。使用注释将一个 `SELECT` 语句注释掉，以便运行另一个语句。

**答案：**

```sql
-- 检索所有列
SELECT * FROM customers;

-- 只检索顾客 ID（将上面的语句注释掉后运行此句）
-- SELECT cust_id FROM customers;
```

**说明：** MySQL 支持两种注释风格：`--`（单行）和 `/* */`（多行）。实际开发中应避免 `SELECT *`，明确列出所需字段性能更好。

---
