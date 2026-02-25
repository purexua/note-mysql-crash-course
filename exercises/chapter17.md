# Chapter 17 — 组合查询

## 练习题

### 练习 17.1

**题目：** 编写一个SQL语句，将两个SELECT语句结合起来，以便从order-items表中检索产品ID(prod_id)和quantity，其中，一个SELECT语句用于过滤数量恰好为100的行，另一个SELECT语句用于过滤 ID以BNBG 开头的产品。按产品ID对结果进行排序。

**答案：**

```sql
SELECT prod_id, quantity
FROM orderitems
WHERE quantity = 100
UNION
SELECT prod_id, quantity
FROM orderitems
WHERE prod_id LIKE 'BNBG%'
ORDER BY prod_id;
```

**说明：** UNION 将两个 SELECT 的结果合并，`ORDER BY` 只写在最后一个 SELECT 之后，对整个合并结果排序。

---

### 练习 17.2

**题目：** 重写你刚刚创建的SQL语句，仅使用单个SELECT语句。

**答案：**

```sql
SELECT prod_id, quantity
FROM orderitems
WHERE quantity = 100 OR prod_id LIKE 'BNBG%'
ORDER BY prod_id;
```

**说明：** 对同一张表的 UNION 通常可以用 OR 条件替代，两者结果相同，单个 SELECT 写法更简洁。

---

### 练习 17.3

**题目：** 虽然这个挑战题有点儿荒谬，但它确实做了你在本章中学到的事情。编写一个SQL语句，返回并组合 products表中的产品名称(prod_name)和customers表中的顾客名称(cust_name)，然后按产品名称对结果进行排序。

**答案：**

```sql
SELECT prod_name AS name
FROM products
UNION
SELECT cust_name
FROM customers
ORDER BY name;
```

**说明：** UNION 可以合并来自不同表的查询结果，但要求列数和数据类型兼容。结果列名以第一个 SELECT 为准，这里用别名 `name` 统一命名，再按其排序。

---

### 练习 17.4

**题目：** 以下SQL语句有什么问题？​（尝试在不运行的情况下指出。​）

```sql
SELECT cust_name, cust_contact, cust_email
FROM customers
WHERE cust_state = 'MI'
ORDER BY cust_name;
UNION
SELECT cust_name, cust_contact, cust_email
FROM customers
WHERE cust_state = 'IL'
ORDER BY cust_name;
```

**答案：** `ORDER BY cust_name;` 后面的分号将第一个 SELECT 变成了独立的完整语句，导致 UNION 成为语法错误。`ORDER BY` 只能出现在整个 UNION 的最末尾，用于对合并后的结果排序。

正确写法：

```sql
SELECT cust_name, cust_contact, cust_email
FROM customers
WHERE cust_state = 'MI'
UNION
SELECT cust_name, cust_contact, cust_email
FROM customers
WHERE cust_state = 'IL'
ORDER BY cust_name;
```

**说明：** UNION 中间不能有分号，`ORDER BY` 只写一次，放在最后一个 SELECT 之后。

---
