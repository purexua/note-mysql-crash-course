# MySQL Crash Course 练习题解答

《MySQL必知必会》（第2版）练习题解答与学习笔记，基于 `crashcourse` 示例数据库。

## 环境要求

- MySQL 8.0+

## 快速开始

克隆仓库并导入示例数据库：

```bash
git clone https://github.com/purexua/note-mysql-crash-course.git
cd note-mysql-crash-course
mysql -u root -p < schema/mysql-crash-course.sql
```

连接并验证：

```bash
mysql -u root -p crashcourse
```

## 目录结构

```
note-mysql-crash-course/
├── schema/
│   └── mysql-crash-course.sql   # crashcourse 数据库完整 schema 及示例数据
├── exercises/
│   ├── chapter04.md             # 检索数据
│   ├── chapter05.md             # 排序检索数据
│   ├── chapter06.md             # 过滤数据
│   ├── chapter07.md             # 高级数据过滤
│   ├── chapter08.md             # 用通配符进行过滤
│   ├── chapter09.md             # 用正则表达式进行搜索
│   ├── chapter10.md             # 创建计算字段
│   ├── chapter11.md             # 使用数据处理函数（含函数参考表）
│   ├── chapter12.md             # 汇总数据（含聚合函数参考）
│   ├── chapter13.md             # 分组数据
│   ├── chapter14.md             # 使用子查询
│   ├── chapter15.md             # 联结表
│   ├── chapter16.md             # 创建高级联结
│   ├── chapter17.md             # 组合查询
│   ├── chapter18.md             # 全文搜索
│   ├── chapter19.md             # 插入数据
│   ├── chapter20.md             # 更新和删除数据
│   ├── chapter21.md             # 创建和操纵表
│   ├── chapter22.md             # 使用视图
│   └── chapter23.md             # 使用存储过程
└── docs/                        # 备用笔记目录
```

## 数据库结构

`crashcourse` 数据库包含 6 张表：

| 表名 | 说明 | 主键 |
|------|------|------|
| `vendors` | 供应商信息 | `vend_id` |
| `products` | 产品目录，关联 vendors | `prod_id` |
| `customers` | 顾客信息 | `cust_id` |
| `orders` | 订单头，关联 customers | `order_num` |
| `orderitems` | 订单明细，关联 orders 和 products | `order_num` + `order_item` |
| `productnotes` | 产品备注，支持全文搜索（MyISAM） | `note_id` |

## 章节索引

| 章节 | 主题 | 核心知识点 |
|------|------|-----------|
| Ch04 | 检索数据 | `SELECT`、`DISTINCT`、`LIMIT` |
| Ch05 | 排序检索数据 | `ORDER BY`、多列排序、`DESC` |
| Ch06 | 过滤数据 | `WHERE`、比较运算符、`BETWEEN`、`NULL` |
| Ch07 | 高级数据过滤 | `AND`、`OR`、`IN`、`NOT`、运算符优先级 |
| Ch08 | 用通配符进行过滤 | `LIKE`、`%`、`_` |
| Ch09 | 用正则表达式进行搜索 | `REGEXP`、字符类、定位符、`NOT REGEXP` |
| Ch10 | 创建计算字段 | 拼接、算术运算、`AS` 别名 |
| Ch11 | 使用数据处理函数 | 文本函数、日期函数、数值函数 |
| Ch12 | 汇总数据 | `AVG`、`COUNT`、`MAX`、`MIN`、`SUM`、`DISTINCT` |
| Ch13 | 分组数据 | `GROUP BY`、`HAVING`、执行顺序 |
| Ch14 | 使用子查询 | 嵌套子查询、相关子查询 |
| Ch15 | 联结表 | 等值连接、`INNER JOIN` |
| Ch16 | 创建高级联结 | `LEFT/RIGHT OUTER JOIN`、自联结、表别名 |
| Ch17 | 组合查询 | `UNION`、`UNION ALL` |
| Ch18 | 全文搜索 | `MATCH()`、`AGAINST()`、布尔模式 |
| Ch19 | 插入数据 | `INSERT INTO`、`INSERT SELECT` |
| Ch20 | 更新和删除数据 | `UPDATE`、`DELETE`、安全实践 |
| Ch21 | 创建和操纵表 | `CREATE TABLE`、`ALTER TABLE`、`DROP TABLE` |
| Ch22 | 使用视图 | `CREATE VIEW`、视图的作用与限制 |
| Ch23 | 使用存储过程 | `CREATE PROCEDURE`、IN/OUT 参数、`DELIMITER` |

## 练习题格式

每个章节文件遵循统一格式：

```markdown
### 练习 X.N

**题目：** 原题描述（保持原文）

**答案：**
​```sql
-- SQL 语句
​```

**说明：** 关键概念解释
```

## 参考资料

- [《MySQL必知必会》Ben Forta 著，第2版](https://www.amazon.com/gp/product/0138223025/?&tag=benfortascoldfus)
- [MySQL 8.0 官方文档](https://dev.mysql.com/doc/refman/8.0/en/)
