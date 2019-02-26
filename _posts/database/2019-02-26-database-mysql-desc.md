---
title: "[database] mysql 테이블 스키마 확인"
layout: post
tag:
- database
category: database
author: itholic
sitemap:
  changefreq: weekly
  priority: 1.0
---

# mysql 테이블 스키마 확인

mysql의 테이블 스키마를 확인하려면 다음과 같이 DESC 명령을 사용하면 된다.

```sql
DESC [TABLE_NAME];
```

다음 예제를 보면 좀 더 구체적으로 이해가 될 것이다.

```sql
mysql> CREATE TABLE test_table (
    name VARCHAR(32) NOT NULL,
    country VARCHAR(32) NOT NULL,
    phone INT(11) NOT NULL
);
```

```
mysql> DESC dept;
+-----------+------------------+------+-----+---------+-------+
| Field     | Type             | Null | Key | Default | Extra |
+-----------+------------------+------+-----+---------+-------+
| name      | varchar(32)      | NO   |     | NULL    |       |
| country   | varchar(32)      | NO   |     | NULL    |       |
| phone     | int(11)          | NO   |     | NULL    |       |
+-----------+------------------+------+-----+---------+-------+
```
