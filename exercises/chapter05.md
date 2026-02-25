# Chapter 5 — 排序检索数据

## 练习题

### 练习 5.1

**题目：** 编写一个 SQL 语句，从 `customers` 表中检索所有的顾客名称（`cust_name`），并按从 Z 到 A 的顺序显示结果。

**答案：**

```sql
SELECT cust_name
FROM customers
ORDER BY cust_name DESC;
```

**说明：** `ORDER BY` 默认升序（`ASC`），加 `DESC` 改为降序，即 Z→A。

---

### 练习 5.2

**题目：** 编写一个 SQL 语句，从 `orders` 表中检索顾客 ID（`cust_id`）和订单号（`order_num`），先按顾客 ID 对结果进行排序，再按订单日期降序排序。

**答案：**

```sql
SELECT cust_id, order_num
FROM orders
ORDER BY cust_id, order_date DESC;
```

**说明：** 多列排序时，`ORDER BY` 按列的书写顺序依次生效。`DESC` 只作用于紧跟其前的那一列，`cust_id` 仍为默认升序。

---

### 练习 5.3

**题目：** 编写一个 SQL 语句，显示 `orderitems` 表中的数量（`quantity`）和价格（`item_price`），并按数量由多到少、价格由高到低排序。

**答案：**

```sql
SELECT quantity, item_price
FROM orderitems
ORDER BY quantity DESC, item_price DESC;
```

**说明：** 两列都需要降序，每列后面都要单独加 `DESC`。

---

### 练习 5.4

**题目：** 以下 SQL 语句有什么问题？（尝试在不运行的情况下指出。）

```sql
SELECT vend_name,
FROM vendors
ORDER vend_name DESC;
```

**答案：** 有两处错误：

1. `SELECT vend_name,` — 列名后面多了一个逗号 `,`，语法错误。
2. `ORDER vend_name DESC` — 缺少 `BY` 关键字，应为 `ORDER BY vend_name DESC`。

**说明：** 正确写法：

```sql
SELECT vend_name
FROM vendors
ORDER BY vend_name DESC;
```

---
