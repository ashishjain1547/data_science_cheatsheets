# Scrapy Cheatsheet
### For test
`scrapy shell https://example.com/`

### Run
`scrapy crawl spider_name`

### Output
`scrapy crawl dapps -o data/07-07-dapps.csv`\
`scrapy crawl dapps -t csv -o - >"data/dapp/$DATE-dapp.csv"`

### Creating a project
`scrapy startproject project_name`

### Example
features_spider.py (gets html pages)
```
import scrapy

class FeaturesSpider(scrapy.Spider):
    name = "features"
    start_urls = [
        'https://www.stateofthedapps.com/collections/featured',
    ]

    def parse(self, response):
        for name in response.css('h4.title-4::text').getall():
            yield {
                'name' : name
            }
```

mainpage_promote_spider.py (gets json files)
```
import scrapy
import json

class MainpagePromoteSpider(scrapy.Spider):
    name = "mainpage_promote"
    start_urls = [
        'https://api.stateofthedapps.com/promoted/dapps',
    ]

    def parse(self, response):
        items = json.loads(response.body_as_unicode())
        for item in items:
            yield {
                'name': item['name']
            }
```

