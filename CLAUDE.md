# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

Practice solutions and notes for *MySQL Crash Course* (2nd Edition). Contains the sample database schema, chapter exercises, and documentation notes.

## Database Setup

Load the sample database into a local MySQL 8.0+ instance:

```bash
mysql -u root -p < schema/mysql-crash-course.sql
```

This creates and populates the `crashcourse` database. To connect and verify:

```bash
mysql -u root -p crashcourse
```

## Schema Overview

The `crashcourse` database has 6 tables with the following relationships:

- `vendors` — supplier info (PK: `vend_id`)
- `products` — product catalog, references `vendors` (PK: `prod_id`)
- `customers` — customer info (PK: `cust_id`)
- `orders` — order headers, references `customers` (PK: `order_num`)
- `orderitems` — order line items, references `orders` and `products` (composite PK: `order_num` + `order_item`)
- `productnotes` — full-text searchable notes per product, uses MyISAM engine for FULLTEXT support

## Repository Structure

- `schema/` — SQL dump to recreate the `crashcourse` database with sample data
- `exercises/` — Chapter exercise answers, one file per chapter (`chapter01.md`, `chapter02.md`, ...)
- `docs/` — Notes and reference documentation

## Exercise File Convention

Each `exercises/chapterXX.md` follows this template:

```markdown
# Chapter X — [Chapter Title]

## 练习题

### 练习 X.1

**题目：** [question]

**答案：**

​```sql
-- SQL query
​```

**说明：** [explanation of approach or key concept]

---
```

When the user provides exercise questions, write answers using this format. Keep **说明** concise — focus on the key MySQL concept demonstrated by the query.
