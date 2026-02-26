# Chapter 23 — 使用存储过程

## 练习题

### 练习 23.1

**题目：** 创建一个存储过程，接受一个顾客ID并返回该顾客的所有订单。

**答案：**

```sql
CREATE PROCEDURE customerorders(IN cust_id INT)
BEGIN
    SELECT order_num
    FROM orders
    WHERE orders.cust_id = cust_id
END;
```

**调用：**

```sql
CALL customerorders(10001);
```

**说明：** 存储过程接受 IN 参数 `cust_id`，在过程体内用 WHERE 过滤该顾客的所有订单并返回。注意用表名限定 `orders.cust_id` 以避免与参数名冲突。

---

### 练习 23.2

**题目：** 不同的地方有不同的税率。ordertotal 存储过程会将税率硬编码为6%。更新该存储过程，使其接受要使用的税率（如果需要的话）​。提示：实际上不需要使用另一个参数，而是可以将taxable 替换为接受一个税率，0表示免税（耶！）​。

**答案：**

```sql
DELIMITER //
-- Name: ordertotal
-- Parameters: onumber = order number
--             taxrate = 0 if not taxable, else tax rate
--             ototal  = order total variable

CREATE PROCEDURE ordertotal(
    IN  onumber  INT,
    IN  taxrate  INT,
    OUT ototal   DECIMAL(8,2)
)
BEGIN
    -- Declare variable for total
    DECLARE total DECIMAL(8,2);

    -- Get the total for the order
    SELECT SUM(item_price * quantity)
    FROM orderitems
    WHERE order_num = onumber
    INTO total;

    -- Add tax if taxable
    IF taxrate > 0 THEN
        SELECT total + (total * taxrate / 100) INTO total;
    END IF;

    -- Save to output parameter
    SELECT total INTO ototal;
END//

DELIMITER ;
```

**调用（含税，税率8%）：**

```sql
CALL ordertotal(20005, 8, @total);
SELECT @total;
```

**调用（免税，税率0）：**

```sql
CALL ordertotal(20005, 0, @total);
SELECT @total;
```

**说明：** 将原来的 `taxable BOOLEAN` 替换为 `taxrate INT`，传入 0 表示免税，传入具体数值（如 8）则按该税率计算。这样比布尔值更灵活，可以支持不同地区的税率。

---
