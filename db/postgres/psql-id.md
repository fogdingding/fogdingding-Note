---
description: 有時候我們在搬移資料的時候，PK id 不一定會更新
---

# psql-id

```sql
SELECT MAX(id) FROM "table_name";
SELECT nextval('"table_name_sql"'::regclass);
--方案一
BEGIN;
LOCK TABLE "table_name" IN EXCLUSIVE MODE;
SELECT setval('"table_id_seq"'::regclass, COALESCE((SELECT MAX(id)+1 FROM table_name), 1), false);
COMMIT;
--方案二
SELECT setval('"goodInfoAnnouncement_id_seq"'::regclass, (SELECT max(id) FROM "goodInfoAnnouncement"));
```

