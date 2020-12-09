---
description: 找尋時間
---

# mongo-date

```python
start = datetime.datetime(2020, 3, 24)
end = datetime.datetime(2020, 4, 24)
tmp = col.find({'newsTime': {'$lt': end, '$gte': start}})
```



