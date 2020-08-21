---
description: >-
  Scrapy是一個Python編寫的開源網絡爬蟲框架。它是一個被設計用於爬取網絡數據、提取結構性數據的程序框架。該框架主要由Scrapinghub
  公司進行維護。
---

# Scrapy

### 安裝方法

使用python3的pip3套件即可順利安裝

```text
pip3 install scrapy
```

### 初步認識架構

#### 創立爬蟲專案

```bash
scrapy startproject tutorial
```

執行以上程式碼在command line後，即可獲得以下的資料樹狀圖。  
備註：其中 tutorial 是指專案名稱，是可以自行編輯的哦～

#### 專案的資料夾內部檔案結構

```text
.
├── scrapy.cfg              # deploy configuration file
└── tutorial                # project's Python module, you'll import your code from here
    ├── __init__.py
    ├── items.py            # project items definition file
    ├── middlewares.py      # project middlewares file
    ├── pipelines.py        # project pipelines file
    ├── settings.py         # project settings file
    └── spiders             # a directory where you'll later put your spiders
        └── __init__.py
```

#### 各個檔案主要處理的項目

* items.py
  * 主要處理於爬蟲完成（解析完成）後，需要對於資料進行封裝的時候所用的欄位定義。
* middlewares.py
  * 主要處理於爬蟲跟目標網站的時候，介入到Scrapy的spider處理機制。也就是說，在爬取網站的時候，會附上一些 headers、cookie 的資料以及當爬蟲中斷 404、500等狀況的時候應該如何處理的部分。
* pipelines.py
  * 把爬取到的欄位透過 items.py 所定義好的欄位，來進行資料的封裝。也就是說把title 、url 、data 等進行資料封裝成dictionary的地方。
* setting.py
  * 主要處理Scrapy運作時候的設定，如middlewares是否執行等。
* spiders
  * 主要放入自己撰寫的爬蟲程式碼。

#### 資料來源

* [Scrapy-中文官方文件](https://scrapy-chs.readthedocs.io/zh_CN/0.24/index.html)
* [Scrapy-英文官方文件](https://docs.scrapy.org/en/latest/)



