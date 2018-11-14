---
title: "[python] 파이썬에서 switch-case를 사용하려면?"
layout: post
tag:
- python
category: python
author: itholic
sitemap:
  changefreq: daily
  priority: 1.0
---

# switch-case on python

파이썬에는 switch-case문이 없다.

따라서 다음과 같이 딕셔너리에 값을 지정해놓고 반환하는 식으로 비슷하게 사용이 가능하다.

```python
def switch_day_of_the_week(idx):
    dict_day_of_the_week = {
        1:'monday',
        2:'tuesday',
        3:'wednesday',
        4:'thursday',
        5:'friday',
        6:'saturday',
        7:'sunday'
    }
    return dict_day_of_the_week.get(idx, '{} is invalid index (1-7)'.format(idx))

switch_day_of_the_week(0)  # '0 is invalid index (1-7)'
switch_day_of_the_week(1)  # 'monday'
switch_day_of_the_week(2)  # 'tuesday'
switch_day_of_the_week(3)  # 'wednesday'
switch_day_of_the_week(4)  # 'thursday'
switch_day_of_the_week(5)  # 'friday'
switch_day_of_the_week(6)  # 'saturday'
switch_day_of_the_week(7)  # 'sunday'
switch_day_of_the_week(8)  # '8 is invalid index (1-7)'
```

보통 딕셔너리의 값을 가져올 때에는 `dict[key]` 와 같은 형태로 가져오지만,

get 메소드를 사용하면 key가 없을시 두 번쨰 인자로 등록한 값을 가져오게 된다.

```
dict_color = {"r":"red", "g":"green", "b":"blue"}

dict_color["r"]  # 'red'
dict_color["g"]  # 'green'
dict_color["b"]  # 'blue'
# dict_color["y"]  # KeyError: 'y' 

dict_color.get("r", 0)  # 'red'
dict_color.get("g", 0)  # 'green'
dict_color.get("b", 0)  # 'blue'
dict_color.get("y", 0)  # 0
```
