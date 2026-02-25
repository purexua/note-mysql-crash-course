# Chapter 10 — 创建计算字段

## 练习题

### 练习 10.1

**题目：** 别名的常见用法是在检索出的结果中重命名表列字段（可能是为了满足特定的报告要求或顾客需求）​。编写一个SQL语句，从vendors表中检索vend_id、vend_name、vend_address和vend_city，并将vend_name 重命名为vname，将vend_city 重命名为vcity，将vend_address 重命名为vaddress。按供应商名称对结果进行排序，为此，可以使用原始名称或新名称。

**答案：**

```sql
SELECT vend_id,
       vend_name AS vname,
       vend_address AS vaddress,
       vend_city AS vcity
FROM vendors
ORDER BY vname;
```

**说明：** 用 `AS` 关键字为列指定别名，`ORDER BY` 可以直接引用别名 `vname`，也可以用原始列名 `vend_name`，两者等效。

---

### 练习 10.2

**题目：** 我们的示例商店正在进行打折促销，所有产品均降价 10%。编写一个SQL语句，从products表中返回prod_id、prod_price和sale_price。sale_price是一个包含促销价格的计算字段。提示：可以乘以0.9，这样得到的值就是原价的90%（因此是10%的折扣）​。

**答案：**

```sql
SELECT prod_id,
       prod_price,
       prod_price * 0.9 AS sale_price
FROM products;
```

**说明：** `prod_price * 0.9` 是一个计算字段，表示原价的 90%，即打九折后的促销价，用 `AS sale_price` 为其命名。

---
