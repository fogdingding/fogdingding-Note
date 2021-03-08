# run shell

如果在 `docker-compose` 上想執行 `test.sh` 則需要注意以下事情

* 權限問題：因此需要使用`Dockerfile` 來進行複製檔案以及權限更動`chmod` 
* 路徑問題：有時如果想要拿取上一層的資料，需要在`docker-compose.yml` 內部填寫`context: ../` \(第五行\) 

### docker/test/Dockerfile

```bash
...

# add test.sh
COPY docker/test.sh /root/
RUN chmod +x /root/test.sh 

CMD ["/bin/bash"]
```

### docker/docker-compose.yml

```bash
version: "3.7"
services:
  test:
    build:
      context: ../
      dockerfile: docker/test/Dockerfile
    stdin_open: true
    tty: true
    command: /bin/sh -c "/root/test.sh"
    working_dir: /root
```

