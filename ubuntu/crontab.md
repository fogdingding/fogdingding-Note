---
description: 一個好用的排程工具
---

# crontab

```text
sudo apt-get update
sudo apt-get install cron
```

```text
.---------------- minute (0 - 59) 
|  .------------- hour (0 - 23)
|  |  .---------- day of month (1 - 31)
|  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ... 
|  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7)  OR sun,mon,tue,wed,thu,fri,sat 
|  |  |  |  |
*  *  *  *  *  command to be executed
```

### 資料來源

* [鳥哥的私房](http://linux.vbird.org/linux_basic/0430cron.php)





