# Chapter 16 — 创建高级联结

## 练习题

### 练习 16.1

**题目：** 使用INNER JOIN 编写一个SQL语句，检索每个顾客的名称（customers表中的cust_name）以及所有的订单号（orders表中的order_num）​。

**答案：**

```sql
SELECT customers.cust_name, orders.order_num
FROM customers
INNER JOIN orders ON customers.cust_id = orders.cust_id
ORDER BY cust_name;
```

**说明：** INNER JOIN 只返回两张表中有匹配行的记录，即只返回有订单的顾客。

---

### 练习 16.2

**题目：** 修改你刚刚创建的SQL语句以列出所有顾客，包括那些没有下过订单的顾客。

**答案：**

```sql
SELECT customers.cust_name, orders.order_num
FROM customers
LEFT OUTER JOIN orders ON customers.cust_id = orders.cust_id
ORDER BY cust_name;
```

**说明：** 改用 LEFT OUTER JOIN，以 customers 为主表，即使某顾客在 orders 中没有匹配行，也会保留该顾客，order_num 显示为 NULL。

---

### 练习 16.3

**题目：** 使用OUTER JOIN 连接 products表和orderitems表，并返回产品名称(prod_name)和与之相关的订单号(order_num)的列表，然后按产品名称排序。

**答案：**

```sql
SELECT products.prod_name, orderitems.order_num
FROM products
LEFT OUTER JOIN orderitems ON products.prod_id = orderitems.prod_id
ORDER BY prod_name;
```

**说明：** LEFT OUTER JOIN 以 products 为主表，未被订购的产品也会出现在结果中，对应的 order_num 为 NULL。

---

### 练习 16.4

**题目：** 修改上一个挑战题中创建的SQL语句，使其返回每一项产品的总订单数（而不是订单号）​。

**答案：**

```sql
SELECT products.prod_name, COUNT(orderitems.order_num) AS orders
FROM products
LEFT OUTER JOIN orderitems ON products.prod_id = orderitems.prod_id
GROUP BY products.prod_name
ORDER BY prod_name;
```

**说明：** 在 16.3 的基础上用 `COUNT()` 替换 order_num，并加上 `GROUP BY`。`COUNT(orderitems.order_num)` 对 NULL 不计数，因此未被订购的产品计数为 0。

---

### 练习 16.5

**题目：** 编写一个SQL语句，列出供应商（vendors表中的vend_id）及其拥有的产品数量，包括没有产品的供应商。你需要使用OUTER JOIN和聚合函数 Count()来计算 products表中每种产品的数量。注意：vend_id列会出现在多张表中，所以每次引用它时，你都需要对其进行完全限定。

**答案：**

```sql
SELECT vendors.vend_id, COUNT(products.prod_id) AS prod_count
FROM vendors
LEFT OUTER JOIN products ON vendors.vend_id = products.vend_id
GROUP BY vendors.vend_id;
```

**说明：** LEFT OUTER JOIN 以 vendors 为主表，没有产品的供应商也会出现。`COUNT(products.prod_id)` 对 NULL 不计数，无产品的供应商计数为 0。vend_id 在两张表中都存在，必须用表名完全限定以避免歧义。

---
