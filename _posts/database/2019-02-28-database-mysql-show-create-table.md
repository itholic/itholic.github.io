---
title: "[database] mysql 테이블 생성 쿼리 확인"
layout: post
tag:
- database
category: database
author: itholic
sitemap:
  changefreq: weekly
  priority: 1.0
---

# mysql 테이블 생성 쿼리 확인

mysql을 사용하다보면,

특정 테이블의 데이터를 조회하거나 스키마를 확인하는 것 외에도,

특정 테이블의 CREATE TABLE 당시 사용했던 SQL문이 보고싶을 수 있다.

그럴땐 다음과 같은 쿼리를 사용하면 특정 테이블의 CREATE TABLE 쿼리를 확인할 수 있다.

```
SHOW CREATE TABLE [TABLE_NAME];
```
