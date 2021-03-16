# 更新json

```sql


update 表名 set 列名 = (jsonb_set(列名::jsonb,'{key}','"value"'::jsonb)) where 条件 

UPDATA "test" SET "test_json" = (jsonb_set("test_json"::jsonb, '{name}', '"test1234"')) where id=3;
 
```

