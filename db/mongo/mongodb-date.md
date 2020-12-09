---
description: 使用python3或其他語言再存入mongo的時候需要注意的有...
---

# mongoDB-date

```python
from dateutil.parser import parse
from datetime import date
parse(date.today().strftime("%Y-%m-%d"))
```

```python
import datetime
import time
publishAt = 1585064773
date = datetime.datetime.fromtimestamp(publishAt)
```

