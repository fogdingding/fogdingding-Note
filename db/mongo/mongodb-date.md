---
description: 使用python3或其他語言再存入mongo的時候需要注意的有...
---

# mongoDB-date

```python
from dateutil.parser import parse
from datetime import date
import datetime
parse(date.today().strftime("%Y-%m-%d"))
parse(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
```

```python
import datetime
import time
publishAt = 1585064773
date = datetime.datetime.fromtimestamp(publishAt)
```

```python
from dateutil.parser import parse
from datetime import date
import datetime

def connect_MongoDB():
    try:
        return MongoClient(host=mongo_host,
                           username=mongo_userName, password=mongo_password, port=int(mongo_port))
    except Exception as e:
        print(f'connect fail! {e}')
        exit()
    else:
        print('connect successful!')

cli = connect_MongoDB()
db = cli["test"]
col = db["test"]

if __name__=='__main__':
    tmp = {
        "newsId": '1234',
        "newsTime": parse(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
    }
    col.update_one({"newsId": tmp["newsId"]}, {"$set": tmp}, upsert=True)
    tmp = col.find({'newsId':'1234'})
    for i in tmp:
        print(i)
        print(i['newsTime'].strftime("%Y-%m-%d %H:%M:%S"))
```



