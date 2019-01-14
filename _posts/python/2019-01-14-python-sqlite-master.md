---
title: "[python] sqlite3 테이블 목록 가져오기(sqlite\_master)"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# sqlite3 테이블 목록 가져오기

파이썬에서는 자체적으로 sqlite3 라이브러리를 지원하므로, 이를 이용한 개발을 자주 하게된다.

특정 DB파일에서 테이블 목록을 가져와 처리해야할 경우는 어떻게 해야할까?

```python
import sqlite3

conn = sqlite3.connect(':memory:')
cursor = conn.cursor()

cursor.execute("CREATE TABLE TEST_TABLE_1 (A TEXT)")
cursor.execute("CREATE TABLE TEST_TABLE_2 (A TEXT)")
cursor.execute("CREATE TABLE TEST_TABLE_3 (A TEXT)")
cursor.execute("SELECT name FROM sqlite_master WHERE type='table';")

# print(cursor.fetchall())  # [('TEST_TABLE_1',), ('TEST_TABLE_2',), ('TEST_TABLE_3',)]
for row in cursor:
    print(row[0])
```

위 스크립트 실행 결과는 다음과 같다.

```
TEST_TABLE_1
TEST_TABLE_2
TEST_TABLE_3
```

생성한 테이블 목록을 잘 출력하고있다.

<br/>

간단하게 동작 원리를 설명하자면,

우선 메모리에서 DB를 오픈하고 TEST\_TABLE 세 개를 만들었다.

connection을 할 때 DB경로에 실제 파일 경로대신 :memory: 라고 주게되면, 

파일을 생성하지 않고 메모리상에서만 작업하게된다.

스크립트를 실행한 이후 :memory: 라는 이름의 파일이 남지 않는다는 의미이다.

<br/>

어쨌든 이렇게 만들어진 테이블 정보는 sqlite\_master라는 시스템 테이블에서 관리한다.

다음은 sqlite\_master 테이블의 스키마이다.

```sql
CREATE TABLE sqlite_master(
  type        TEXT,
  name        TEXT,
  tbl_name    TEXT,
  rootpage    INTEGER,
  sql         TEXT
);
```

type은 해당 데이터가 테이블 관련 정보인지 인덱스 관련 정보인지 등을 나타낸다.

테이블을 생성하게되면 'table' 이라는 데이터가 삽입된다.

name은 말그대로 해당 오브젝트의 이름을 의미한다.

TEST\_TABLE\_1 을 만들었다면, 이 내용이 그대로 삽입된다.

그래서 위 스크립트에서 

```sql
SELECT name FROM sqlite_master WHERE type='table';
```

라는 쿼리를 사용해 테이블명을 가져온 것이다.

tbl\_name은 말그대로 table이름이다.

테이블의 경우에는 name, tbl\_name이 같다.

인덱스나 트리거의 경우에는 해당 인덱스나 트리거가 어떤 테이블을 대상으로 적용되었는지 나타낸다.

예를들어 TEST\_IDX\_1 이라는 인덱스를 TEST\_TABLE\_1 에 걸어주었을 경우,

name에는 TEST\_IDX\_1, tbl\_name에는 TEST\_TABLE\_1 이 저장된다.

rootpage는 루트 b-tree 페이지의 번호를 나타낸다.

sql은 해당 오브젝트를 생성할때 실제 실행한 sql 스크립트가 저장된다.

이 스크립트를 조회 후 정규식 등을 사용해 적절히 파싱하게되면,

테이블명 뿐 아니라 컬럼명, 컬럼타입 등 여러 정보를 가져와 사용할 수 있다.
