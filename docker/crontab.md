# crontab

### 範例程式碼

```text
* * * * * docker exec -t {containerID} {command} >> /dev/null 2>&1
* * * * * docker exec -t $(docker ps -qf "name=dockerphp1") python3 hello.py >> /dev/null 2>&1
```

### 來源資料

* [部落客教學](https://blog.longwin.com.tw/2020/07/docker-crontab-how-to-set-2020/)

