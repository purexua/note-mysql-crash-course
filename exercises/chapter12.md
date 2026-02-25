# Chapter 12 — 汇总数据

## 练习题

### 练习 12.1

**题目：** 编写一个SQL语句，确定已售出的所有物品的总数量（使用order-items表中的quantity列）​。

**答案：**

```sql
SELECT SUM(quantity) AS total_quantity
FROM orderitems;
```

**说明：** `SUM()` 对指定列的所有值求和，返回 orderitems 表中所有订单行的数量总计。

---

### 练习 12.2

**题目：** 修改你刚刚编写的语句，确定prod_item 为BR01的物品已售出的总数量。

**答案：**

```sql
SELECT SUM(quantity) AS total_quantity
FROM orderitems
WHERE prod_id = 'BR01';
```

**说明：** 在 12.1 的基础上加 `WHERE prod_id = 'BR01'`，将聚合范围限定为特定产品。

---

### 练习 12.3

**题目：** 这是一个有点儿愚蠢的问题，但想象一下，一个顾客想要购买 products表中的每一件产品。编写一个SQL语句来计算总价。

**答案：**

```sql
SELECT SUM(prod_price) AS total_price
FROM products;
```

**说明：** 每件产品各买一件，总价即为所有产品单价之和，用 `SUM(prod_price)` 直接汇总即可。

---

### 练习 12.4

**题目：** 编写一个SQL语句，确定products表中价格(prod_price)不超过 10美元的产品的最贵价格。将计算出的字段命名为max_price。

**答案：**

```sql
SELECT MAX(prod_price) AS max_price
FROM products
WHERE prod_price <= 10;
```

**说明：** `MAX()` 返回满足条件的行中的最大值，`WHERE prod_price <= 10` 先过滤出价格不超过 10 美元的产品，再从中取最高价。

---

## 函数参考

### SQL 聚合函数

| 函数 | 说明 | 示例 |
|------|------|------|
| `AVG()` | 返回某列的平均值 | `AVG(col_name)` |
| `COUNT()` | 返回某列的行数 | `COUNT(col_name)` / `COUNT(*)`|
| `MAX()` | 返回某列的最大值 | `MAX(col_name)` |
| `MIN()` | 返回某列的最小值 | `MIN(col_name)` |
| `SUM()` | 返回某列值之和 | `SUM(col_name)` |

### 聚合不同值（DISTINCT）

在聚合函数中加入 `DISTINCT` 关键字，可以只对不重复的值进行计算：

```sql
SELECT AVG(DISTINCT prod_price) AS avg_price
FROM products;
```

- 默认行为（`ALL`）：对所有行计算，包含重复值
- 指定 `DISTINCT`：先去重，再聚合，重复值只计算一次
- `DISTINCT` 可用于 `AVG()`、`SUM()`、`COUNT()` 等，但不能用于 `MAX()` 和 `MIN()`（对它们无意义）


