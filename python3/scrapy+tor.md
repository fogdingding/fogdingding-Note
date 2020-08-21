---
description: 當爬蟲長時間對於一個網站進行抓取，將會有機率性的被阻擋。因此我們可以透過更改proxy的方法來避免被阻擋（反爬蟲）。
---

# Scrapy+Tor

Tor是實現匿名通信的自由軟體。其名源於「The Onion Router」（洋蔥路由器）的英語縮寫Tor。用戶可透過Tor接達由全球志願者免費提供，包含6000+個中繼的覆蓋網路，從而達至隱藏用戶真實位址、避免網路監控及流量分析的目的。Tor用戶的網際網路活動（包括瀏覽線上網站、貼文以及即時訊息等通訊形式）相對較難追蹤。Tor的設計原意在於保障用戶的個人隱私，以及不受監控地進行秘密通信的自由和能力。[資料來源](https://zh.wikipedia.org/wiki/Tor)

#### 安裝\(mac\)

* tor
* polipo

```bash
brew install tor
brew install polipo
```

安裝完畢後將進行新增檔案

```bash
mkdir /etc/polipo
cd /etc/polipo
touch config
```

在config 檔案內新增以下程式碼

```bash
# config file
socksParentProxy = localhost:9050
diskCacheRoot=""
disableLocalInterface=""
```

重起服務，polipo應該會預設背景執行，我們只需重啟服務即可。

```bash
brew services restart polipo
```

執行tor服務

```bash
tor
```

#### 設定Scrapy + Tor

一樣先行建立專案並創建爬蟲主體檔案api.py

```python
scrapy startproject api
```

檔案結構

```python
.
├── api
│   ├── __init__.py
│   ├── items.py
│   ├── middlewares.py
│   ├── pipelines.py
│   ├── settings.py
│   └── spiders
│       ├── __init__.py
│       └── api.py        # 自行建立
└── scrapy.cfg
```

在middlewares.py 新增以下程式碼

```python
from scrapy.utils.project import get_project_settings
settings = get_project_settings()
from fake_useragent import UserAgent

class UserAgentMiddleware(object):
    def process_request(self, request, spider):
        ua = UserAgent()
        user_agent = ua.chrome
        request.headers.setdefault(b'User-Agent', user_agent)

class ProxyMiddleware(object):
    def process_request(self, request, spider):
        request.meta['proxy'] = settings.get('HTTP_PROXY')
```

在settings.py新增以下程式碼

```python
ROBOTSTXT_OBEY = False
DOWNLOAD_DELAY = 1
HTTP_PROXY = 'http://127.0.0.1:8123'
DOWNLOADER_MIDDLEWARES = {
     'api.middlewares.UserAgentMiddleware': 400,
     'api.middlewares.ProxyMiddleware': 410,
     'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None,
}
RETRY_TIMES = 3
RETRY_ENABLED: False
COOKIES_ENABLES = False
```

#### 新增爬蟲主體

```python
import scrapy


class ApiSpider(scrapy.Spider):
    name = "api"

    def write_to_file(self, words):
        with open("logging.log", "a") as f:
            f.write(words)
            f.write('\n')

    def start_requests(self):
        urls = [
            'https://api.ipify.org',
        ]
        for url in urls:
            request = scrapy.Request(url=url, callback=self.parse)
            yield request

    def parse(self, response):
        self.write_to_file("*" * 40)
        self.write_to_file("response text: %s" % response.text)
        self.write_to_file("response headers: %s" % response.headers)
        self.write_to_file("response meta: %s" % response.meta)
        self.write_to_file("request headers: %s" % response.request.headers)
        self.write_to_file("request cookies: %s" % response.request.cookies)
        self.write_to_file("request meta: %s" % response.request.meta)
```

執行爬蟲

```bash
scrapy cawle api
```

logging.log檔案將會看出目前的ip為51.75.52.118這即是透過tor來進行替換proxy的部分。  
透過瀏覽器進行api查詢訪問（[連結網址](https://api.ipify.org/)）即可知道目前localhost的IP位址

```bash
****************************************
response text: 51.75.52.118
response headers: {b'Server': [b'Cowboy'], b'Content-Type': [b'text/plain'], b'Vary': [b'Origin'], b'Date': [b'Fri, 21 Aug 2020 07:00:28 GMT'], b'Via': [b'1.1 vegur']}
response meta: {'download_timeout': 180.0, 'proxy': 'http://127.0.0.1:8123', 'download_slot': 'api.ipify.org', 'download_latency': 5.826346158981323}
request headers: {b'Accept': [b'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8'], b'Accept-Language': [b'en'], b'User-Agent': [b'Mozilla/5.0 (Windows NT 6.3; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2049.0 Safari/537.36'], b'Accept-Encoding': [b'gzip, deflate']}
request cookies: {}
request meta: {'download_timeout': 180.0, 'proxy': 'http://127.0.0.1:8123', 'download_slot': 'api.ipify.org', 'download_latency': 5.826346158981323}

```

#### 新增並測試當爬蟲中斷的處理

更改爬蟲主體

```python
import scrapy


class ApiSpider(scrapy.Spider):
    name = "api"

    def write_to_file(self, words):
        with open("logging.log", "a") as f:
            f.write(words)
            f.write('\n')

    def start_requests(self):
        urls = []
        for i in range(10):
            urls.append('https://api.ipify.org')
        for url in urls:
            request = scrapy.Request(url=url, callback=self.parse,dont_filter = True)
            yield request

    def parse(self, response):
        self.write_to_file("*" * 40)
        self.write_to_file("response text: %s" % response.text)
        self.write_to_file("response headers: %s" % response.headers)
        self.write_to_file("response meta: %s" % response.meta)
        self.write_to_file("request headers: %s" % response.request.headers)
        self.write_to_file("request cookies: %s" % response.request.cookies)
        self.write_to_file("request meta: %s" % response.request.meta)
```

更改settings.py

```python
ROBOTSTXT_OBEY = True
DOWNLOAD_DELAY = 0
HTTP_PROXY = 'http://127.0.0.1:8123'
DOWNLOADER_MIDDLEWARES = {
     'api.middlewares.UserAgentMiddleware': 400,
     'api.middlewares.ProxyMiddleware': 410,
     'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None,
     'api.middlewares.Process_Proxies': 120,
}
RETRY_TIMES = 3
RETRY_ENABLED: True
COOKIES_ENABLES = False
DUPEFILTER_DEBUG = True
```

新增middlewares.py

```python
import logging
from scrapy.downloadermiddlewares.retry import RetryMiddleware
from scrapy.utils.response import response_status_message
from stem import Signal
from stem.control import Controller
import time
import random
class Process_Proxies(RetryMiddleware):
    logger = logging.getLogger(__name__)

    def dele_proxy(self,proxy,res=None):
        print('刪除代理')
        with Controller.from_port(port=9051) as c:
            c.authenticate()
            c.signal(Signal.NEWNYM)
    def process_response(self, request, response, spider):
        if response.status == 200:
            return response
        elif response.status != 200:
            print('狀態碼異常')
            print(response.status)
            reason = response_status_message(response.status)
            self.dele_proxy(request.meta['proxy'],False)
            time.sleep(random.randint(1,3))
            return self._retry(request,reason,spider) or response

    def process_exception(self, request, exception, spider):
        if isinstance(exception,self.EXCEPTIONS_TO_RETRY) and not request.meta.get('dont_retry',False):
            self.dele_proxy(request.meta.get('proxy',False))
            time.sleep(random.randint(1,3))
            self.logger.warning('連線異常,進行重試......')

            return self._retry(request,exception,spider)
```

即可看到，中間會進行IP替換

```bash
****************************************
response text: 185.220.102.250
response headers: {b'Server': [b'Cowboy'], b'Content-Type': [b'text/plain'], b'Vary': [b'Origin'], b'Date': [b'Fri, 21 Aug 2020 07:29:56 GMT'], b'Via': [b'1.1 vegur']}
response meta: {'download_timeout': 180.0, 'proxy': 'http://127.0.0.1:8123', 'download_slot': 'api.ipify.org', 'download_latency': 0.5960571765899658}
request headers: {b'Accept': [b'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8'], b'Accept-Language': [b'en'], b'User-Agent': [b'Scrapy/2.3.0 (+https://scrapy.org)'], b'Accept-Encoding': [b'gzip, deflate']}
request cookies: {}
request meta: {'download_timeout': 180.0, 'proxy': 'http://127.0.0.1:8123', 'download_slot': 'api.ipify.org', 'download_latency': 0.5960571765899658}
****************************************
response text: 162.247.74.27
response headers: {b'Server': [b'Cowboy'], b'Content-Type': [b'text/plain'], b'Vary': [b'Origin'], b'Date': [b'Fri, 21 Aug 2020 07:29:56 GMT'], b'Via': [b'1.1 vegur']}
response meta: {'download_timeout': 180.0, 'proxy': 'http://127.0.0.1:8123', 'download_slot': 'api.ipify.org', 'download_latency': 2.55774188041687}
request headers: {b'Accept': [b'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8'], b'Accept-Language': [b'en'], b'User-Agent': [b'Scrapy/2.3.0 (+https://scrapy.org)'], b'Accept-Encoding': [b'gzip, deflate']}
request cookies: {}
request meta: {'download_timeout': 180.0, 'proxy': 'http://127.0.0.1:8123', 'download_slot': 'api.ipify.org', 'download_latency': 2.55774188041687}
```

#### 總結

在前半段的部分，我們進行第一次的嘗試，確保IP已經被修正了。  
在後半段的部分，為了強迫產生異常處理，我們將ROBOTSTXT\_OBEY = True來讓爬蟲特別抓取robots.txt的部分（造成404回應）。因此我們才有後續的更改ip的動作。  
並且避免重複一直執行，RETRY\_TIMES = 3進行設定（最多跑三次）。



#### 資料來源

* [作者為Erik van de Ven所撰寫的範例文](https://www.kaggle.com/getting-started/45130)
* 
