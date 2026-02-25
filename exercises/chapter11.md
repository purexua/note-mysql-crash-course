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

| 函数 | 说明 | 示例 |
|------|------|------|
| `Left()` | 返回字符串左边的 n 个字符 | `Left(str, n)` |
| `Length()` | 返回字符串的长度 | `Length(str)` |
| `Locate()` | 找出子串在字符串中的位置 | `Locate(substr, str)` |
| `Lower()` | 将字符串转换为小写 | `Lower(str)` |
| `LTrim()` | 去掉字符串左边的空格 | `LTrim(str)` |
| `Right()` | 返回字符串右边的 n 个字符 | `Right(str, n)` |
| `RTrim()` | 去掉字符串右边的空格 | `RTrim(str)` |
| `Soundex()` | 返回字符串的 SOUNDEX 值 | `Soundex(str)` |
| `SubString()` | 返回子字符串 | `SubString(str, pos, len)` |
| `Upper()` | 将字符串转换为大写 | `Upper(str)` |

### 日期和时间处理函数

| 函数 | 说明 | 示例 |
|------|------|------|
| `AddDate()` | 增加一个日期（天、周等） | `AddDate(date, INTERVAL n unit)` |
| `AddTime()` | 增加一个时间（时、分等） | `AddTime(time, interval)` |
| `CurDate()` | 返回当前日期 | `CurDate()` |
| `CurTime()` | 返回当前时间 | `CurTime()` |
| `Date()` | 返回日期时间的日期部分 | `Date(datetime)` |
| `DateDiff()` | 计算两个日期之差 | `DateDiff(date1, date2)` |
| `Date_Add()` | 日期运算 | `Date_Add(date, INTERVAL n unit)` |
| `Date_Format()` | 返回格式化的日期或时间字符串 | `Date_Format(date, format)` |
| `Day()` | 返回一个日期的天数部分 | `Day(date)` |
| `DayOfWeek()` | 返回对应的星期几 | `DayOfWeek(date)` |
| `Hour()` | 返回一个时间的小时部分 | `Hour(time)` |
| `Minute()` | 返回一个时间的分钟部分 | `Minute(time)` |
| `Month()` | 返回一个日期的月份部分 | `Month(date)` |
| `Now()` | 返回当前日期和时间 | `Now()` |
| `Second()` | 返回一个时间的秒部分 | `Second(time)` |
| `Time()` | 返回日期时间的时间部分 | `Time(datetime)` |
| `Year()` | 返回一个日期的年份部分 | `Year(date)` |

### 数值处理函数

| 函数 | 说明 | 示例 |
|------|------|------|
| `Abs()` | 返回一个数的绝对值 | `Abs(n)` |
| `Cos()` | 返回一个角度的余弦值 | `Cos(n)` |
| `Exp()` | 返回一个数的指数值 | `Exp(n)` |
| `Mod()` | 返回除法运算的余数 | `Mod(n, m)` |
| `Pi()` | 返回圆周率 | `Pi()` |
| `Rand()` | 返回一个随机数 | `Rand()` |
| `Sin()` | 返回一个角度的正弦值 | `Sin(n)` |
| `Sqrt()` | 返回一个数的平方根 | `Sqrt(n)` |
| `Tan()` | 返回一个角度的正切值 | `Tan(n)` |
