---
description: A Dependency Manager for PHP
---

# composer

### 安裝介紹

#### mac

一行指令即可安裝

```bash
# install
brew install composer
# check
composer --version

# output
# Composer version 1.10.10 2020-08-03 11:35:19
```

#### liunx

```bash
# install
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"

#local use
php composer.phar
# check
php composer.phar --version

#golbal use
mv composer.phar /usr/local/bin/composer
# check
composer --version

# check output
# Composer version 1.10.10 2020-08-03 11:35:19
```

### 資料來源

* [官方連結](https://getcomposer.org/)

