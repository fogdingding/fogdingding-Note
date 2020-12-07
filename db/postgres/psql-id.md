---
description: 有時候我們在搬移資料的時候，PK id 不一定會更新
---

# psql-id

再進行資料庫搬移或複製數據後，容易出現的錯誤，就是資料庫內部的ID會沒有改變。

```sql
//error log
// DETAIL:  Key (id)=(1) already exists.
```

```sql
-- 查詢目前的id、跟目前追蹤的id
SELECT MAX(id) FROM "table_name";
SELECT nextval('"table_name_sql"'::regclass);
-- 修正id
SELECT setval('"Announcement_id_seq"'::regclass, (SELECT max(id) FROM "Announcement"));
```

