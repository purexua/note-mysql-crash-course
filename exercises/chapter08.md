# Chapter 8 — 用通配符进行过滤

## 练习题

### 练习 8.1

**题目：** 编写一个SQL语句，从products表中检索产品名称(prod_name)和产品描述(prod_desc)，并仅返回产品描述中包含词toy的产品。

**答案：**

```sql
SELECT prod_name, prod_desc
FROM products
WHERE prod_desc LIKE '%toy%';
```

**说明：** `%toy%` 中两侧的 `%` 匹配 toy 前后的任意字符，只要描述中任意位置含有 toy 即可命中。

---

### 练习 8.2

**题目：** 反过来再来一次。编写一个SQL语句，从products表中检索产品名称(prod_name)和产品描述(prod_desc)，并仅返回产品描述中不包含词toy的产品。这次按照产品名称对结果进行排序。

**答案：**

```sql
SELECT prod_name, prod_desc
FROM products
WHERE prod_desc NOT LIKE '%toy%'
ORDER BY prod_name;
```

**说明：** `NOT LIKE` 是 `LIKE` 的取反，排除所有描述中含 toy 的行，再用 `ORDER BY` 按名称升序排列。

---

### 练习 8.3

**题目：** 编写一个SQL语句，从products表中检索产品名称(prod_name)和产品描述(prod_desc)，并仅返回产品描述中同时包含词toy和carrots的产品。有几种方法可以执行此操作，但对于这个挑战题，可以使用一个AND和两个LIKE。

**答案：**

```sql
SELECT prod_name, prod_desc
FROM products
WHERE prod_desc LIKE '%toy%'
  AND prod_desc LIKE '%carrots%';
```

**说明：** 两个 `LIKE` 条件用 `AND` 连接，要求描述中必须同时出现 toy 和 carrots，但不限制两者的先后顺序。

---

### 练习 8.4

**题目：** 来个有点儿棘手的。我没有特别向你展示这种语法，但你可以根据到目前为止学到的知识来看看是否能弄清楚。编写一个SQL语句，从products表中检索产品名称(prod_name)和产品描述(prod_desc)，并仅返回以先后顺序同时出现词toy和carrots的产品。提示：只需用带 3个%的LIKE 即可。

**答案：**

```sql
SELECT prod_name, prod_desc
FROM products
WHERE prod_desc LIKE '%toy%carrots%';
```

**说明：** 模式 `%toy%carrots%` 要求描述中先出现 toy，再出现 carrots，三个 `%` 分别匹配 toy 之前、toy 与 carrots 之间、carrots 之后的任意字符，从而限定了顺序。

---
