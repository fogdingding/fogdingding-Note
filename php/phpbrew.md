# phpbrew



```text
sudo apt-get update
sudo apt-get upgrade

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
apt-get install postgresql postgresql-client postgresql-contrib


# 假設是root user
curl -L -O https://github.com/phpbrew/phpbrew/raw/master/phpbrew
chmod +x phpbrew
# Move phpbrew to somewhere can be found by your $PATH
mv phpbrew /usr/local/bin/phpbrew

vim ~/.bashrc
add source $HOME/.phpbrew/bashrc


# 初始化PHPBrew
phpbrew init
# 重新載入設定檔.bashrc
source ~/.bashrc

phpbrew known
phpbrew known --old
phpbrew install 7.1.10
phpbrew use 7.1.10
php --version
phpbrew off
php --version
```

