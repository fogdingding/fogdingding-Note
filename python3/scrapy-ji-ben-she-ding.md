---
description: 有關於Scrapy的基礎設定，如設定隨機改變的header等
---

# Scrapy基本設定

#### 創建範例

```bash
scrapy startproject ptt
```

```bash
.
├── ptt
│   ├── __init__.py
│   ├── items.py
│   ├── middlewares.py        # 主要操作對象
│   ├── pipelines.py
│   ├── settings.py           # 主要操作對象
│   └── spiders
│       ├── __init__.py
│       └── first_spider.py   # 主要操作對象
└── scrapy.cfg
```

#### 新增middleware的函數

於middlewares.py內新增以下程式碼

```python
from fake_useragent import UserAgent


class UserAgentMiddleware(object):
    def process_request(self, request, spider):
        ua = UserAgent()
        user_agent = ua.chrome
        request.headers.setdefault(b'User-Agent', user_agent)
```

#### 新增settings.py的設定

善用Ctrl+F來進行查詢 DOWNLOADER\_MIDDLEWARES 的位址，尊重原先的設計



```python
DOWNLOADER_MIDDLEWARES = {
     'ptt.middlewares.UserAgentMiddleware': 400, # 主要設定該專案的middlewares為...
     'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None, # 把預設的UserAgentMiddleware給關掉
}
```

#### 新增爬蟲主體

```bash
.
├── ptt2
│   ├── __init__.py
│   ├── items.py
│   ├── middlewares.py
│   ├── pipelines.py
│   ├── settings.py
│   └── spiders
│       ├── __init__.py
│       └── ptt.py        # 新增檔案
└── scrapy.cfg
```

於spiders/ptt.py 新增檔案後，加入以下程式碼。

```python
import scrapy


class QuotesSpider(scrapy.Spider):
    name = "quotes"

    # 寫入logging.log檔案
    def write_to_file(self, words):
        with open("logging.log", "a") as f:
            f.write(words)
            f.write('\n')

    # 主體爬蟲的進入點。
    def start_requests(self):
        urls = [
            'http://quotes.toscrape.com/page/1/',
            'http://quotes.toscrape.com/page/2/',
        ]
        for url in urls:
            request = scrapy.Request(url=url, callback=self.parse)
            yield request

    # 爬蟲順利獲得資料後，進行解析的地方。
    def parse(self, response):

        # 爬取的網站html等。
        page = response.url.split("/")[-2]
        filename = 'quotes-{}.html'.format(page)
        with open(filename, 'wb') as f:
            f.write(response.body)
        
        # 寫入logging file
        # self.log('Saved file {}'.format(filename))
        self.write_to_file("*" * 40)
        self.write_to_file("response text: {}".format(response.text))
        self.write_to_file("response headers: {}".format(response.headers))
        self.write_to_file("response meta: {}".format(response.meta))
        self.write_to_file("request headers: {}".format(response.request.headers))
        self.write_to_file("request cookies: {}".format(response.request.cookies))
        self.write_to_file("request meta: {}".format(response.request.meta))
```

在於有scrapy.cfg的檔案路徑進行以下指令，這邊備註一下，為何是quotes而不是ptt呢。主要因為在主體的ptt.py檔案內，我們寫的時候是把name以及ClassName取名為Quotes哦～

```python
scrapy crawl quotes
```

將會產生出以下三個檔案

```bash
.
├── logging.log
├── quotes-1.html
├── quotes-2.html
└── scrapy.cfg
```

* loggin.log
  * 紀錄爬蟲的log
* quotes-1.html
  * [目標爬蟲網址](http://quotes.toscrape.com/page/1/)
* quotes-2.html
  * [目標爬蟲網址](http://quotes.toscrape.com/page/2/)

#### loggin.log的記錄狀況

觀看下列紀錄的headers

```bash
****************************************
response headers: {b'Server': [b'nginx/1.14.0 (Ubuntu)'], b'Date': [b'Fri, 21 Aug 2020 05:57:36 GMT'], b'Content-Type': [b'text/html; charset=utf-8'], b'X-Upstream': [b'spidyquotes-master_web']}
response meta: {'download_timeout': 180.0, 'download_slot': 'quotes.toscrape.com', 'download_latency': 0.3361520767211914}
request headers: {b'Accept': [b'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8'], b'Accept-Language': [b'en'], b'User-Agent': [b'Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/28.0.1468.0 Safari/537.36'], b'Accept-Encoding': [b'gzip, deflate']}
request cookies: {}
request meta: {'download_timeout': 180.0, 'download_slot': 'quotes.toscrape.com', 'download_latency': 0.3361520767211914}
****************************************
response headers: {b'Server': [b'nginx/1.14.0 (Ubuntu)'], b'Date': [b'Fri, 21 Aug 2020 05:57:37 GMT'], b'Content-Type': [b'text/html; charset=utf-8'], b'X-Upstream': [b'spidyquotes-master_web']}
response meta: {'download_timeout': 180.0, 'download_slot': 'quotes.toscrape.com', 'download_latency': 0.7438931465148926}
request headers: {b'Accept': [b'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8'], b'Accept-Language': [b'en'], b'User-Agent': [b'Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36'], b'Accept-Encoding': [b'gzip, deflate']}
request cookies: {}
request meta: {'download_timeout': 180.0, 'download_slot': 'quotes.toscrape.com', 'download_latency': 0.7438931465148926}

```

#### setting 設定

* ROBOTSTXT\_OBEY
  * 預設True，主要是為了符合robots.txt的規範。（就關掉吧，都要當爬蟲了XD\)
* DOWNLOAD\_DELAY
  * 預設為0，主要是爬蟲的間格為何（單位/秒）。從同一網站下載連續頁面之前，下載程序應等待的時間（以秒為單位）。這可以用來限制爬網速度，以避免對服務器造成太大的衝擊。支持小數。
* DOWNLOADER\_MIDDLEWARES
  * 主要進行爬蟲的MIDDLEWARES指派等。包含您的項目中啟用的下載器中間件及其命令的字典。
* RETRY\_TIMES
  * 除了首次下載外，最大重試次數。
* RETRY\_ENABLED
  * 是否啟用“重試”中間件。
* COOKIES\_ENABLES
  * 預設為True，關閉將可以把Cookie給隱藏起來，避免被反爬蟲偵測到。

```bash
ROBOTSTXT_OBEY = False
DOWNLOAD_DELAY = 1
RETRY_TIMES = 3
RETRY_ENABLED: True
COOKIES_ENABLES = False
```

#### 參數傳遞\(meta\)

```python
import scrapy


class QuotesSpider(scrapy.Spider):
    name = "quotes"

    # 寫入logging.log檔案
    def write_to_file(self, words):
        with open("logging.log", "a") as f:
            f.write(words)
            f.write('\n')

    # 主體爬蟲的進入點。
    def start_requests(self):
        urls = [
            'http://quotes.toscrape.com/page/1/',
            'http://quotes.toscrape.com/page/2/',
        ]
        test = {'test':'hello'}
        for url in urls:
            request = scrapy.Request(url=url, callback=self.parse)
            request.meta['item'] = test
            yield request

    # 爬蟲順利獲得資料後，進行解析的地方。
    def parse(self, response):
        # 爬取的網站html等。
        page = response.url.split("/")[-2]
        filename = 'quotes-{}.html'.format(page)
        with open(filename, 'wb') as f:
            f.write(response.body)
        
        # 寫入logging file
        # self.log('Saved file {}'.format(filename))
        self.write_to_file("*" * 40)
        # self.write_to_file("response text: {}".format(response.text))
        self.write_to_file("response headers: {}".format(response.headers))
        self.write_to_file("response meta: {}".format(response.meta))
        self.write_to_file("request headers: {}".format(response.request.headers))
        self.write_to_file("request cookies: {}".format(response.request.cookies))
        self.write_to_file("request meta: {}".format(response.request.meta))
        self.write_to_file("request parameter: {}".format(response.request.meta['test']))
```

logging.log檔案內即可看到

```bash
****************************************
response headers: {b'Server': [b'nginx/1.14.0 (Ubuntu)'], b'Date': [b'Fri, 21 Aug 2020 06:29:32 GMT'], b'Content-Type': [b'text/html; charset=utf-8'], b'X-Upstream': [b'spidyquotes-master_web']}
response meta: {'test': {'test': 'hello'}, 'download_timeout': 180.0, 'download_slot': 'quotes.toscrape.com', 'download_latency': 0.39804697036743164}
request headers: {b'Accept': [b'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8'], b'Accept-Language': [b'en'], b'User-Agent': [b'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.17 (KHTML, like Gecko) Chrome/24.0.1312.60 Safari/537.17'], b'Accept-Encoding': [b'gzip, deflate']}
request cookies: {}
request meta: {'test': {'test': 'hello'}, 'download_timeout': 180.0, 'download_slot': 'quotes.toscrape.com', 'download_latency': 0.39804697036743164}
request parameter: {'test': 'hello'}
****************************************
response headers: {b'Server': [b'nginx/1.14.0 (Ubuntu)'], b'Date': [b'Fri, 21 Aug 2020 06:29:32 GMT'], b'Content-Type': [b'text/html; charset=utf-8'], b'X-Upstream': [b'spidyquotes-master_web']}
response meta: {'test': {'test': 'hello'}, 'download_timeout': 180.0, 'download_slot': 'quotes.toscrape.com', 'download_latency': 0.685413122177124}
request headers: {b'Accept': [b'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8'], b'Accept-Language': [b'en'], b'User-Agent': [b'Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.67 Safari/537.36'], b'Accept-Encoding': [b'gzip, deflate']}
request cookies: {}
request meta: {'test': {'test': 'hello'}, 'download_timeout': 180.0, 'download_slot': 'quotes.toscrape.com', 'download_latency': 0.685413122177124}
request parameter: {'test': 'hello'}
```

#### 資料來源

* [settings文件](https://docs.scrapy.org/en/latest/topics/settings.html)
* [scrapy對於meta、headers、cookies的解說](https://blog.csdn.net/mouday/article/details/81159416)

