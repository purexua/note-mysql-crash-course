# Chapter 22 — 使用视图

## 练习题

### 练习 22.1

**题目：** 创建一个名为vendorproducts的视图，将vendors表和products表连接起来。使用SELECT语句确保你拥有正确的数据。

**答案：**

```sql
CREATE VIEW vendorproducts AS
SELECT vendors.vend_id, vend_name, prod_id, prod_name, prod_price
FROM vendors
INNER JOIN products ON vendors.vend_id = products.vend_id;
```

**验证：**

```sql
SELECT * FROM vendorproducts;
```

**说明：** 视图将两张表的连接封装起来，后续查询直接使用视图名即可，无需重复编写 JOIN 逻辑。

---

### 练习 22.2

**题目：** 创建一个名为customerswithorders的视图，其中包含 customers表中的所有列，但仅仅是那些已下订单的列。提示：可以在orders表中使用JOIN来仅仅过滤所需的顾客。然后使用SELECT语句确保拥有正确的数据。

**答案：**

```sql
CREATE VIEW customerswithorders AS
SELECT customers.*
FROM customers
INNER JOIN orders ON customers.cust_id = orders.cust_id;
```

**验证：**

```sql
SELECT * FROM customerswithorders;
```

**说明：** INNER JOIN 只保留在 orders 表中有匹配记录的顾客，即只返回已下过订单的顾客。视图将这一过滤逻辑封装起来，使用时无需关心底层实现。

---
