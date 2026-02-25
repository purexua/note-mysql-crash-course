# Chapter 15 — 联结表

## 练习题

### 练习 15.1

**题目：** 编写一个SQL语句，分别从customers表中返回顾客名称(cust_name)，从orders表中返回相关订单号(order_num)，然后按顾客名称和订单号对结果进行排序。实际上，请尝试两次：一次使用简单的等值连接语法，一次使用INNER JOIN。

**答案（等值连接）：**

```sql
SELECT customers.cust_name, orders.order_num
FROM customers, orders
WHERE customers.cust_id = orders.cust_id
ORDER BY cust_name, order_num;
```

**答案（INNER JOIN）：**

```sql
SELECT customers.cust_name, orders.order_num
FROM customers INNER JOIN orders
ON customers.cust_id = orders.cust_id
ORDER BY cust_name, order_num;
```

**说明：** 两种写法结果相同。等值连接在 WHERE 中指定连接条件，INNER JOIN 使用 ON 子句，后者语义更清晰，是推荐写法。

---

### 练习 15.2

**题目：** 我们来让上一个挑战题变得更有用些。除了返回顾客名称和订单号，再添加一个名为ordertotal的第三列，其中包含每笔订单的总价。有两种方法可以执行此操作：一种是使用orderitems表的子查询来创建ordertotal列，另一种是将orderitems表连接到现有表并使用聚合函数。提示：注意需要使用完全限定列名的地方。

**答案（子查询）：**

```sql
SELECT customers.cust_name,
       orders.order_num,
       (SELECT SUM(item_price * quantity)
        FROM orderitems
        WHERE orderitems.order_num = orders.order_num) AS ordertotal
FROM customers INNER JOIN orders
ON customers.cust_id = orders.cust_id
ORDER BY cust_name, order_num;
```

**答案（JOIN + 聚合）：**

```sql
SELECT customers.cust_name,
       orders.order_num,
       SUM(orderitems.item_price * orderitems.quantity) AS ordertotal
FROM customers
INNER JOIN orders ON customers.cust_id = orders.cust_id
INNER JOIN orderitems ON orders.order_num = orderitems.order_num
GROUP BY customers.cust_name, orders.order_num
ORDER BY cust_name, order_num;
```

**说明：** 子查询写法逐行计算，JOIN + 聚合写法将三张表连接后用 GROUP BY 分组汇总，两者结果相同，后者通常性能更好。

---

### 练习 15.3

**题目：** 让我们重温一下第14章的挑战题(2)。编写一个SQL语句，检索产品BR01的订购日期，但这次使用连接和简单的等值连接语法。输出应该与第14章相同。

**答案：**

```sql
SELECT orders.cust_id, orders.order_date
FROM orders, orderitems
WHERE orders.order_num = orderitems.order_num
  AND orderitems.prod_id = 'BR01'
ORDER BY order_date;
```

**说明：** 用等值连接替代子查询，在 WHERE 中同时指定连接条件和过滤条件，结果与第 14 章相同。

---

### 练习 15.4

**题目：** 非常有趣，让我们再试一次。重新创建你在第14章的挑战题(3)中编写的SQL，但这次使用ANSI的INNER JOIN 语法。在之前编写的代码中你使用了两个嵌套的子查询。要重新创建它，需要两个INNER JOIN语句，每个语句的格式与本章前面的INNER JOIN 示例类似。不要忘记使用WHERE子句来按 prod_id 进行过滤。

**答案：**

```sql
SELECT customers.cust_email
FROM customers
INNER JOIN orders ON customers.cust_id = orders.cust_id
INNER JOIN orderitems ON orders.order_num = orderitems.order_num
WHERE orderitems.prod_id = 'BR01';
```

**说明：** 两个 INNER JOIN 将三张表串联起来，用 WHERE 过滤产品 ID，替代了第 14 章中的两层嵌套子查询，逻辑更直观。

---

### 练习 15.5

**题目：** 再来一次，为了让事情变得更有趣，我们将混合使用连接、聚合函数和分组。准备好了吗？回到第13章，当时的挑战是要求找出总计订单价格至少为1000的所有订单的订单号。这些结果是有用的，但更有用的是下了至少这个金额的订单的顾客名称。因此，编写一个SQL语句，使用连接从customers表中返回顾客名称(cust_name)，从orderitems表中返回所有订单的总价。提示：为了连接这些表，还需要包括 orders表（因为customers表与orderitems表没有直接关系，但customers表与orders表有关，而orders表与orderitems表有关）​。别忘了GROUP BY和HAVING，并确保按顾客名称对结果进行排序。你可以使用简单的等值连接或ANSI的INNER JOIN语法。或者也可以两种方法都试一下。

**答案（等值连接）：**

```sql
SELECT customers.cust_name,
       SUM(orderitems.item_price * orderitems.quantity) AS ordertotal
FROM customers, orders, orderitems
WHERE customers.cust_id = orders.cust_id
  AND orders.order_num = orderitems.order_num
GROUP BY customers.cust_name
HAVING SUM(item_price*quantity) >= 1000
ORDER BY cust_name;
```

**答案（INNER JOIN）：**

```sql
SELECT customers.cust_name,
       SUM(orderitems.item_price * orderitems.quantity) AS ordertotal
FROM customers
INNER JOIN orders ON customers.cust_id = orders.cust_id
INNER JOIN orderitems ON orders.order_num = orderitems.order_num
GROUP BY customers.cust_name
HAVING SUM(item_price*quantity) >= 1000
ORDER BY cust_name;
```

**说明：** 三表连接后按顾客名称分组，`HAVING` 过滤总价不低于 1000 的顾客，最后按名称排序。连接是子查询的更优替代方案，性能通常更好。

---
