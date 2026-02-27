# Chapter 14 — 使用子查询

## 练习题

### 练习 14.1

**题目：** 使用子查询，返回购买了价格为10美元（含）以上物品的顾客列表。你需要使用orderitems表查找匹配的订单号(order_num)，然后使用orders表检索每个匹配订单的顾客ID(cust_id)。

**答案：**

```sql
SELECT DISTINCT cust_id
FROM orders
WHERE order_num IN (
    SELECT order_num
    FROM orderitems
    WHERE item_price >= 10
);
```

**说明：** 最内层子查询从 orderitems 中找出单价不低于 10 美元的订单号，外层查询再从 orders 中返回对应的顾客 ID。

---

### 练习 14.2

**题目：** 你想知道物品 BR01的订购日期。编写一个SQL语句，使用子查询来确定orderitems表中的哪些订单购买了prod_id 为BR01的物品，然后从orders表中返回每件物品对应的顾客ID(cust_id)和订单日期(order_date)。按订购日期对结果进行排序。

**答案：**

```sql
SELECT cust_id, order_date
FROM orders
WHERE order_num IN (
    SELECT order_num
    FROM orderitems
    WHERE prod_id = 'BR01'
)
ORDER BY order_date;
```

**说明：** 子查询从 orderitems 中找出购买了 BR01 的订单号，外层查询返回这些订单的顾客 ID 和订单日期，并按日期排序。

---

### 练习 14.3

**题目：** 现在让我们令这个挑战更有难度。更新上一个挑战题，为购买了prod_id 为BR01的物品的所有顾客返回电子邮件（customers表中的cust_email）​。提示：这涉及 SELECT语句，最内层的查询会从orderitems表返回order_num，中间的查询会从customers表返回cust_id。

**答案：**

```sql
SELECT DISTINCT cust_email
FROM customers
WHERE cust_id IN (
    SELECT cust_id
    FROM orders
    WHERE order_num IN (
        SELECT order_num
        FROM orderitems
        WHERE prod_id = 'BR01'
    )
);
```

**说明：** 三层嵌套子查询：最内层找出购买了 BR01 的订单号，中间层找出对应的顾客 ID，最外层从 customers 表返回这些顾客的邮箱。

---

### 练习 14.4

**题目：** 你需要一个列出每个顾客ID及其总订单金额的列表。编写一个SQL语句，返回顾客ID（orders表中的cust_id）和total_ordered，并使用子查询返回每个顾客的订单总额。按消费金额从高到低对结果进行排序。提示：我们之前使用Sum() 计算过订单总额。

**答案：**

```sql
SELECT cust_id,
       (SELECT SUM(item_price * quantity)
        FROM orderitems
        WHERE orderitems.order_num IN (
            SELECT order_num FROM orders WHERE orders.cust_id = customers.cust_id
        )) AS total_ordered
FROM customers
ORDER BY total_ordered DESC;
```

**说明：** 相关子查询为每个顾客计算其所有订单的总金额，外层按顾客 ID 分组并按总金额降序排列。

---

### 练习 14.5

**题目：** 编写一个SQL语句，从products表中检索所有的产品名称(prod_name)，以及名为quant_sold的计算列，该列包含此产品的销售总数（使用子查询和Sum(quantity)在orderitems表中检索）​。

**答案：**

```sql
SELECT prod_name,
       (SELECT SUM(quantity)
        FROM orderitems
        WHERE orderitems.prod_id = products.prod_id) AS quant_sold
FROM products;
```

**说明：** 相关子查询对 products 表中的每一行，到 orderitems 中匹配相同 prod_id 并求销售总数，结果作为计算列 quant_sold 返回。

---
