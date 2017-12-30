## Agenda

- A brief thought
- RNN & LSTM
- TL;DR

```python
# -*- coding: utf-8 -*-
import scrapy



class QuizletSpider(scrapy.Spider):
    name = "quizlet"
    allowed_domains = ["quizlet.com"]
    start_urls = ['https://quizlet.com/106562829/vocabulario-noken-4-']

    def parse(self, response):
        item = u''

        for quote in response.css("div.SetPageTerm-contentWrapper"):
            jp = quote.css("span.lang-ja::text").extract_first()
            sp = quote.css("span.lang-es::text").extract_first()

            item += u'{}\n\n--{}\n%\n'.format(jp,sp)

        f = open('vN4', 'w+')
        f.write(item.encode('utf8'))
        f.close()
        print item
```

Note:
