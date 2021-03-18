# nginx

監聽80後轉發封包，並依照server\_name

```text
server {
  listen 80;
  server_name b.taiwin.tw;
  location / {
    proxy_pass http://127.0.0.1:8002/;
  }
}
```

