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

## 函数参考

### 文本处理函数

| 函数 | 说明 |
|------|------|
| `Left(str, n)` | 返回字符串左边的 n 个字符 |
| `Length(str)` | 返回字符串的长度 |
| `Locate(substr, str)` | 找出字符串中一个子串的位置 |
| `Lower(str)` | 将字符串转换为小写 |
| `LTrim(str)` | 去掉字符串左边的空格 |
| `Right(str, n)` | 返回字符串右边的 n 个字符 |
| `RTrim(str)` | 去掉字符串右边的空格 |
| `Soundex(str)` | 返回字符串的 SOUNDEX 值 |
| `SubString(str, pos, len)` | 返回子字符串 |
| `Upper(str)` | 将字符串转换为大写 |

### 日期和时间处理函数

| 函数 | 说明 |
|------|------|
| `AddDate(date, INTERVAL n unit)` | 增加一个日期（天、周等） |
| `AddTime(time, interval)` | 增加一个时间（时、分等） |
| `CurDate()` | 返回当前日期 |
| `CurTime()` | 返回当前时间 |
| `Date(datetime)` | 返回日期时间的日期部分 |
| `DateDiff(date1, date2)` | 计算两个日期之差 |
| `Date_Add(date, INTERVAL n unit)` | 日期运算 |
| `Date_Format(date, format)` | 返回一个格式化的日期或时间字符串 |
| `Day(date)` | 返回一个日期的天数部分 |
| `DayOfWeek(date)` | 返回对应的星期几 |
| `Hour(time)` | 返回一个时间的小时部分 |
| `Minute(time)` | 返回一个时间的分钟部分 |
| `Month(date)` | 返回一个日期的月份部分 |
| `Now()` | 返回当前日期和时间 |
| `Second(time)` | 返回一个时间的秒部分 |
| `Time(datetime)` | 返回一个日期时间的时间部分 |
| `Year(date)` | 返回一个日期的年份部分 |

### 数值处理函数

| 函数 | 说明 |
|------|------|
| `Abs(n)` | 返回一个数的绝对值 |
| `Cos(n)` | 返回一个角度的余弦值 |
| `Exp(n)` | 返回一个数的指数值 |
| `Mod(n, m)` | 返回除法运算的余数 |
| `Pi()` | 返回圆周率 |
| `Rand()` | 返回一个随机数 |
| `Sin(n)` | 返回一个角度的正弦值 |
| `Sqrt(n)` | 返回一个数的平方根 |
| `Tan(n)` | 返回一个角度的正切值 |
