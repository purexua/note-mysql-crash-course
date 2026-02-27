# Chapter 19 — 插入数据

## 练习题

### 练习 19.1

**题目：** 使用INSERT和指定的列，将你自己添加到 customers表中。明确列出要添加哪几列，并且仅需列出你需要的列。

**答案：**

```sql
INSERT INTO customers (cust_name, cust_address, cust_city, cust_state, cust_zip, cust_country)
VALUES ('Xu Bai', '123 Main St', 'Shenzhen', 'GD', '518000', 'CN');
```

**说明：** 明确列出需要插入的列名，未列出的列（如 cust_id、cust_email 等）将使用默认值或 NULL。这种写法比省略列名更安全，不受表结构变化影响。

---

### 练习 19.2

**题目：** 使用INSERT SELECT语句，为你的orders表和orderitems表创建备份副本。

**答案：**

```sql
CREATE TABLE orders_backup LIKE orders;

INSERT INTO orders_backup
SELECT * FROM orders;
```

```sql
CREATE TABLE orderitems_backup LIKE orderitems;

INSERT INTO orderitems_backup
SELECT * FROM orderitems;
```

**说明：** 先用 `CREATE TABLE ... LIKE` 复制表结构，再用 `INSERT INTO ... SELECT` 复制数据，避免重复插入。若使用 `CREATE TABLE ... AS SELECT`，通常可一步完成建表和数据复制。

---
