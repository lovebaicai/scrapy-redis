#### 自用scrapy-redis，修改源代码，适合自己项目需求
- fork [scrapy-redis](https://github.com/rmax/scrapy-redis)
- 原项目会持续读取redis数据，不会自动停止。修改源代码，实现读取固定source:start_urls完成后，自动结束爬虫
- 目前测试可使用20个进程同时抓取30余个平台，读取redis结束后，可自动结束
- 部署环境：CentOS release 6.9 (Final) + Python3.5
- 具体实现代码：
```Python
# filename: spiders
# linenumber：82
while found < self.redis_batch_size:
    data = fetch_one(self.redis_key)
    if not data:
        # Queue empty.
        #self.crawler.engine.close_spider(self.name, 'finished')
        self.crawler.engine.close_spider(spider=self, reason='queue is empty, the spider close')
        break
```
