# Chapter 20 — 更新和删除数据

## 练习题

### 练习 20.1

**题目：** 美国各州的缩写应该始终是大写。编写一个SQL语句来更新所有美国地址，包括供应商所在州（vendors表中的vend_state）和顾客所在州（customers表中的cust_state）​，使它们均为大写。为此，你需要使用一个将文本转换为大写的函数（如果需要，请参阅第11章）​，并使用WHERE子句仅过滤美国地址。

**答案：**

```sql
UPDATE vendors
SET vend_state = UPPER(vend_state)
WHERE vend_country = 'USA';

UPDATE customers
SET cust_state = UPPER(cust_state)
WHERE cust_country = 'USA';
```

**说明：** `UPPER()` 将字段值转为大写后写回原列，`WHERE` 限定只更新美国地址，避免影响其他国家的数据。

---

### 练习 20.2

**题目：** 第19章中的挑战题(1)要求你将自己添加到 customers表中。现在请删除你自己。确保使用WHERE子句（并在使用DELETE语句之前用SELECT语句进行测试）​，否则你将删除所有顾客。

**答案（先用 SELECT 验证）：**

```sql
SELECT * FROM customers WHERE cust_id = 10006;
```

**答案（确认无误后执行删除）：**

```sql
DELETE FROM customers WHERE cust_id = 10006;
```

**说明：** 执行 DELETE 前先用 SELECT 确认目标行，避免误删。WHERE 子句是 DELETE 语句的安全保障，省略 WHERE 将删除表中所有数据。

---
