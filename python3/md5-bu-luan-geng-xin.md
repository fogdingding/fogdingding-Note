# md5不亂更新

```python
import hashlib

# 不加鹽
hashlib.md5("ASD".encode("utf-8")).hexdigest()

# 這樣每次出來的值就都一樣了。

```



