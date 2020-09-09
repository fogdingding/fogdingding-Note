# laradock

### 套件需求

* git
* docker
* laradock

### 安裝開始

先建立一個資料夾來存放，之後下載laradock以及自己的專案

```text
mkdir -p ~/services/<projectName>
cd ~/services/test

git clone https://github.com/laradock/laradock.git
git clone <GitProjectName>
```

laradock進入資料夾，複製設置檔案，再進行相關設定。

```text
cd ~/services/<projectName>/laradock
cp env-example .env
```

#### 編輯設定檔案\(主要為volume\_path、nginx、php-fpm、mysql\)

1.volume\_path

```bash
#修正地方連結我的git下來的專案路徑
#APP_CODE_PATH_HOST=../project-z/

APP_CODE_PATH_HOST=../GitProjectName
```

2.nginx

```bash
#修正地方，需要對外的port為何
#NGINX_HOST_HTTP_PORT=80
#NGINX_HOST_HTTPS_PORT=443

NGINX_HOST_HTTP_PORT=1180
NGINX_HOST_HTTPS_PORT=11443
NGINX_HOST_LOG_PATH=./logs/nginx/
NGINX_SITES_PATH=./nginx/sites/
NGINX_PHP_UPSTREAM_CONTAINER=php-fpm
NGINX_PHP_UPSTREAM_PORT=9000
NGINX_SSL_PATH=./nginx/ssl/
```

其餘的可以先不用動。

### 啟動docekr

```bash
docker-compose up -d --build nginx php-fpm mysql
# docker-compose up -d nginx php-fpm mysql
# 第一次才需要build喔
# 第一次可能會需要一點時間…
# 可能要10G左右硬體容量喔…


docker ps
# 查看服務是否啟動

docker-compose exec --user=laradock workspace bash
# 進入docker
# 然後就可以開始設定專案了，設定完成後。
```

### 驗證

網頁輸入localhost:11080，  
剛剛nginx設定的部分。  
如果有出現自己設定的laravel的專案頁面就成功了～～～～





### 資料來源

* [github](https://github.com/laradock/laradock)

