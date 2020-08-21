---
description: 使用Scrapy來進行一個簡單的爬蟲範例，主要爬取的目標網站為Ptt
---

# Scrapy-Ptt範例

批踢踢實業坊，簡稱批踢踢、PTT，是一個臺灣電子布告欄（BBS），採用Telnet BBS技術運作，建立在台灣學術網路的資源之上，以學術性質為原始目的，提供線上言論空間。目前由國立臺灣大學電子布告欄系統研究社管理，大部份的系統原始碼由國立臺灣大學資訊工程學系的學生與校友進行維護，並且邀請法律專業人士擔任法律顧問。[資料來源](https://zh.wikipedia.org/wiki/%E6%89%B9%E8%B8%A2%E8%B8%A2)

#### 建立專案

```bash
scrapy startproject ptt
```

專案-檔案結構

```bash
.
├── ptt
│   ├── __init__.py
│   ├── items.py               # 資料欄位定義
│   ├── middlewares.py
│   ├── pipelines.py
│   ├── settings.py
│   └── spiders                # 爬蟲主體放置位子
│       └── __init__.py
└── scrapy.cfg
```

#### 設置資料欄位定義

於items.py內進行編輯撰寫

```python
import scrapy

class PttItem(scrapy.Item):
    title = scrapy.Field()
    author = scrapy.Field()
    date = scrapy.Field()
    push = scrapy.Field()
    url = scrapy.Field()
```

#### 撰寫爬蟲主體

於spiders資料夾內創立一個新的檔案為ptt.py

```bash
.
├── ptt
│   ├── __init__.py
│   ├── items.py
│   ├── middlewares.py
│   ├── pipelines.py
│   ├── settings.py
│   └── spiders
│       ├── __init__.py
│       └── ptt.py            # 新增爬蟲主體
└── scrapy.cfg
```

```python
from ptt.items import PttItem
import scrapy
import time

class PTTSpider(scrapy.Spider):
    name = 'ptt'
    allowed_domains = ['ptt.cc']
    start_urls = ['https://www.ptt.cc/bbs/Gossiping/index.html']
    
    def parse(self, response):
        for i in range(100):
            time.sleep(1)
            url = "https://www.ptt.cc/bbs/Gossiping/index" + str(39164 - i) + ".html"
            yield scrapy.Request (url, cookies={'over18': '1'}, callback=self.parse_article)
    def parse_article(self, response):
        item = PttItem()
        target = response.css("div.r-ent")


        for tag in target:
            try:
                item['title'] = tag.css("div.title a::text")[0].extract()
                item['author'] = tag.css('div.author::text')[0].extract()
                item['date'] = tag.css('div.date::text')[0].extract()
                item['push'] = tag.css('span::text')[0].extract()
                item['url'] = tag.css('div.title a::attr(href)')[0].extract()

                yield item

            except IndexError:
                pass
            continue
```

#### 開始執行爬蟲

於含有scrapy.cfg的路徑下執行下列程式碼。

```bash
.
├── ptt
│   ├── __init__.py
│   ├── items.py
│   ├── middlewares.py
│   ├── pipelines.py
│   ├── settings.py
│   └── spiders
│       ├── __init__.py
│       └── ptt.py
└── scrapy.cfg             # 於此檔案的位址來執行下列程式碼的指令
```

```bash
scrapy crawl ptt
```

如果要將檔案進行存擋的話，只需增加以下參數

```bash
scrapy crawl ptt -o output.json # 輸出為JSON文件
scrapy crawl ptt -o output.csv # 輸出為CSV文件
```

#### 資料來源

* [作者為Max的教學文](https://www.maxlist.xyz/2018/08/25/python_scrapy_ptt/)
* [作者為Yong-Siang Shih的教學文](https://city.shaform.com/zh/2016/02/28/scrapy/)（進階）

