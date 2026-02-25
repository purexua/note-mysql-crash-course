# Chapter 7 — 高级数据过滤

## 练习题

### 练习 7.1

**题目：** 从 vendors 表中检索供应商名称（vend_name），仅返回加利福尼亚州（CA）且国家为 USA 的供应商。

**答案：**

```sql
SELECT vend_name
FROM vendors
WHERE vend_country = 'USA' AND vend_state = 'CA';
```

**说明：** 用 AND 连接两个条件，同时满足国家为 USA 且州为 CA，避免其他国家同名州的干扰。

---

### 练习 7.2

**题目：** 查找 orderitems 表中至少订购了 100 件 BR01、BR02 或 BR03 的订单，返回 order_num、prod_id 和 quantity。

**答案：**

```sql
SELECT order_num, prod_id, quantity
FROM orderitems
WHERE (prod_id = 'BR01' OR prod_id = 'BR02' OR prod_id = 'BR03')
  AND quantity >= 100;
```

**说明：** OR 条件需用括号括起来，确保先对产品 ID 求值，再与 AND 的数量条件组合。若不加括号，AND 优先级高于 OR，会导致逻辑错误。

---

### 练习 7.3

**题目：** 返回 products 表中价格在 3 美元到 6 美元之间的所有产品名称（prod_name）和价格（prod_price），使用 AND 运算符，并按价格排序。

**答案：**

```sql
SELECT prod_name, prod_price
FROM products
WHERE prod_price >= 3 AND prod_price <= 6
ORDER BY prod_price;
```

**说明：** 用 AND 连接上下界条件实现范围过滤，等价于 BETWEEN 3 AND 6，但更直观地体现 AND 的用法。

---

### 练习 7.4

**题目：** 以下 SQL 语句有什么问题？

```sql
SELECT vend_name
FROM vendors
ORDER BY vend_name
WHERE vend_country = 'USA' AND vend_state = 'CA';
```

**答案：** `ORDER BY` 子句必须放在 `WHERE` 子句**之后**，当前语句将 `ORDER BY` 写在了 `WHERE` 前面，违反了 SQL 子句的书写顺序，执行时会报语法错误。

正确写法：

```sql
SELECT vend_name
FROM vendors
WHERE vend_country = 'USA' AND vend_state = 'CA'
ORDER BY vend_name;
```

**说明：** SQL 子句的固定顺序为 `SELECT → FROM → WHERE → ORDER BY`，顺序不可颠倒。

---
