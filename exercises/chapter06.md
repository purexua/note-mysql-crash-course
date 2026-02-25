# Chapter 6 — 过滤数据

## 练习题

### 练习 6.1

**题目：** 编写一个 SQL 语句，从 `products` 表中检索产品 ID（`prod_id`）和产品名称（`prod_name`），并仅返回价格为 9.49 美元的产品。

**答案：**

```sql
SELECT prod_id, prod_name
FROM products
WHERE prod_price = 9.49;
```

**说明：** `WHERE` 子句用于过滤行，`=` 是精确匹配操作符。

---

### 练习 6.2

**题目：** 编写一个 SQL 语句，从 `products` 表中检索产品 ID（`prod_id`）和产品名称（`prod_name`），并仅返回价格大于或等于 9 美元的产品。

**答案：**

```sql
SELECT prod_id, prod_name
FROM products
WHERE prod_price >= 9;
```

**说明：** `>=` 表示大于或等于，常用比较操作符还有 `>`、`<`、`<=`、`<>`、`!=`（不等于）。

---

### 练习 6.3

**题目：** 编写一个 SQL 语句，从 `orderitems` 表中检索出物品数量达到 100 或以上的订单的唯一订单号（`order_num`）列表。

**答案：**

```sql
SELECT DISTINCT order_num
FROM orderitems
WHERE quantity >= 100;
```

**说明：** 结合第 4 章的 `DISTINCT` 去重和本章的 `WHERE` 过滤，同一订单可能有多个行，`DISTINCT` 确保每个订单号只出现一次。

---

### 练习 6.4

**题目：** 编写一个 SQL 语句，返回 `products` 表中所有价格在 3 美元和 6 美元之间产品的名称（`prod_name`）和价格（`prod_price`），然后按价格排序。

**答案：**

```sql
SELECT prod_name, prod_price
FROM products
WHERE prod_price >= 3 AND prod_price <= 6
ORDER BY prod_price;
```

**说明：** 用 `AND` 连接两个条件实现范围过滤。第 7 章会介绍等价的 `BETWEEN 3 AND 6` 写法，两者结果相同。

---
