# Chapter 13 — 分组数据

## 练习题

### 练习 13.1

**题目：** orderitems表包含每笔订单的每项物品。编写一个SQL语句，返回每个订单号(order_num)的行数(order_lines)，并按 order_lines对结果进行排序。

**答案：**

```sql
SELECT order_num, COUNT(*) AS order_lines
FROM orderitems
GROUP BY order_num
ORDER BY order_lines;
```

**说明：** `GROUP BY order_num` 将每笔订单的所有行归为一组，`COUNT(*)` 统计每组的行数，再按行数升序排列。

---

### 练习 13.2

**题目：** 编写一个SQL语句，返回名为cheapest_item的字段，该字段中包含每个供应商成本最低的物品（使用products表中的prod_price）​，然后按成本从低到高的顺序对结果进行排序。

**答案：**

```sql
SELECT vend_id, MIN(prod_price) AS cheapest_item
FROM products
GROUP BY vend_id
ORDER BY cheapest_item;
```

**说明：** `GROUP BY vend_id` 按供应商分组，`MIN(prod_price)` 取每组中的最低价，再按最低价升序排列。

---

### 练习 13.3

**题目：** 确定最佳顾客非常重要。编写一个SQL语句，返回至少包含 100件物品的每笔订单的订单号（orderitems表中的order_num）​。

**答案：**

```sql
SELECT order_num
FROM orderitems
GROUP BY order_num
HAVING SUM(quantity) >= 100;
ORDER BY order_num;
```

**说明：** 先按订单分组，再用 `HAVING` 过滤出物品总数量不低于 100 的订单。`HAVING` 用于对聚合结果进行过滤，`WHERE` 无法做到这一点。

---

### 练习 13.4

**题目：** 确定最佳顾客的另一种方法是统计他们的消费金额。编写一个SQL语句，返回订单总价至少为1000的所有订单的订单号（orderitems表中的order_num）​。提示：对于这个问题，需要计算并求和总价（item_price 乘以quantity）​。按订单号对结果进行排序。

**答案：**

```sql
SELECT order_num, SUM(item_price * quantity) AS order_total
FROM orderitems
GROUP BY order_num
HAVING SUM(item_price*quantity) >= 1000
ORDER BY order_num;
```

**说明：** `item_price * quantity` 计算每行的小计，`SUM()` 汇总为订单总价，`HAVING` 过滤出总价不低于 1000 的订单，最后按订单号排序。

---

### 练习 13.5

**题目：** 以下SQL语句有什么问题？​（尝试在不运行的情况下指出。​）

```sql
SELECT order_num, COUNT(*) AS items
FROM orderitems
GROUP BY items
HAVING COUNT(*) >= 3
ORDER BY items, order_num;
```

**答案：** `GROUP BY items` 有误。`items` 是 `SELECT` 中定义的别名，`GROUP BY` 子句在 `SELECT` 之前执行，此时别名尚未生效，因此无法按别名分组。应改为按实际列名分组：

```sql
SELECT order_num, COUNT(*) AS items
FROM orderitems
GROUP BY order_num
HAVING COUNT() >= 3
ORDER BY items, order_num;
```

**说明：** SQL 子句执行顺序为 `FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY`，`GROUP BY` 不能引用 `SELECT` 中定义的别名，`ORDER BY` 则可以。

---
