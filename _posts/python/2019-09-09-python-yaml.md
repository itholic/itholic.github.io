---
title: "[python] python에서 yaml 파일 사용하기"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# 파이썬에서 yaml 사용하기

pip으로 PyYAML을 설치해준다.

```
$ pip install PyYAML
```

만약 다음과 같은 yaml 파일이 있다고 하면

```yaml
# info.yaml
language: python
test: pytest
```

이렇게 불러와서 쓰면 된다.

```python
import yaml

with open('info.yaml') as f:
    conf = yaml.load(f)


language = conf['language']
test = conf['pytest']
```

yaml.load를 사용하면 yaml파일의 내용을 딕셔너리로 만들어준다.

따라서 단순히 키를 사용해 값을 가져다가 사용하면 된다.
