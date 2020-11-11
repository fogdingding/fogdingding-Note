# import上一層目錄

```python
import sys, os, inspect
currentdir = os.path.dirname(os.path.abspath(inspect.getfile(inspect.currentframe())))
parentdir = os.path.dirname(currentdir)
sys.path.insert(0, parentdir)
```

```python
# 可以直接import了，因為路徑已經寫進去了。
# 小心如果檔案名稱之類的有一樣的話，將會爆炸。
import XXX.XXX
from XXX.XXX import XXX
```

