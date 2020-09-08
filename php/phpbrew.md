---
description: PHPBrew 是由 C9S 大神產出來的神作，一直以來都用它維護伺服器上的 PHP 版本
---

# phpbrew

### on ubuntu-18.04 install

先行更新套件管理

```text
sudo apt-get update
sudo apt-get upgrade
```

安裝相關套件\(php7.2-預設\)

```bash
sudo apt-get install curl
sudo apt-get install php7.2 \
  php7.2-curl \
  php7.2-json \
  php7.2-cgi \
  php7.2-fpm \
  php7.2-bz2 \
  autoconf \
  automake \
  libxml2-dev \
  libcurl4-openssl-dev \
  libssl-dev \
  openssl \
  gettext \
  libicu-dev \
  libmcrypt-dev \
  libmcrypt4 \
  libbz2-dev \
  libreadline-dev \
  build-essential \
  libmhash-dev \
  libmhash2 \
  libxslt1-dev
  
# 如果想要有額外的MySQL支援還需要安裝下列的套件
apt-get install mysql-server mysql-client libmysqlclient-dev libmysqld-devZ
# 如果想要有額外的PostgreSQL支援還需要安裝下列的套件
apt-get install postgresql postgresql-client postgresql-contri

```

下載使用，搬移檔案變成全域使用

```bash
sudo curl -L -O https://github.com/phpbrew/phpbrew/raw/master/phpbrew
sudo chmod +x phpbrew
# Move phpbrew to somewhere can be found by your $PATH
sudo mv phpbrew /usr/local/bin/phpbrew

sudo vim ~/.bashrc
sudo add source $HOME/.phpbrew/bashrc
```

接下來就能在終端機上打入指令，如果出現版本資訊就表示成功了

```bash
phpbrew known
# 更老的版本
phpbrew known --old
```

```bash
# 安裝，需要編譯，所以會很久喔。
phpbrew install 7.1.10
# 切換版本
phpbrew use 7.1.10
# 確認版本資訊
php --version
# 關掉phpbrew
phpbrew off
# 再次確認
php --version

```



