# Chapter 11 — 使用数据处理函数

## 练习题

### 练习 11.1

**题目：** 我们的商店已经上线了，正在创建顾客账户。所有用户都需要登录名，默认的登录名由用户姓名和所在城市组成。编写一个SQL语句，返回顾客ID(cust_id)、顾客名称(customer_name)以及登录名(user_login)，其中登录名全部为大写字母，且由顾客联系人(cust_contact)的前两个字符和顾客所在城市(cust_city)的前3个字符组成。例如，我的登录名是BEOAK（Ben Forta，居住在Oak Park）​。提示：对于这个例子，需要使用函数、拼接和别名。

**答案：**

```sql
SELECT cust_id,
       cust_name AS customer_name,
       CONCAT(UPPER(LEFT(cust_contact, 2)), UPPER(LEFT(cust_city, 3))) AS user_login
FROM customers;
```

**说明：** `LEFT(str, n)` 取字符串前 n 个字符，`CONCAT` 拼接两段，`UPPER` 转为大写，最后用 `AS` 命名为 `user_login`。

---

### 练习 11.2

**题目：** 编写一个SQL语句，返回2023 年 10 月的所有订单的订单号(order_num)和订单日期(order_date)，并按订单日期排序。

**答案：**

```sql
SELECT order_num, order_date
FROM orders
WHERE YEAR(order_date) = 2023 AND MONTH(order_date) = 10
ORDER BY order_date;
```

**说明：** `YEAR()` 和 `MONTH()` 分别提取日期中的年份和月份，用 `AND` 组合过滤出 2023 年 10 月的订单，再按日期升序排列。

---
