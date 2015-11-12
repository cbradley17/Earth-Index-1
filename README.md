# Earth-Index-1
Scrapy Tabular Data Web Crawler

import scrapy

from govdata.items import GovdataItem                                #import from item path

class GovdataSpider(scrapy.Spider):                                
    name = "EIA2"
    allowed_domains = ["EIA.gov"]
    start_urls = [
        "http://www.eia.gov/forecasts/steo/report/us_oil.cfm",
    ]                                                                #target url

    def parse(self, response):
        log.msg('parse(%s)' % response.url, level = log.DEBUG)  
        rows = response.xpath('//table')                             #data location
        for row in rows:
            item = PopulationItem()
            item['CrudeOil'] = row.xpath('th/text()').extract()
            item['Dollars'] = row.xpath('td[2]/text()').extract()
            item['AllVals'] = row.xpath ('//table').extract()
            item['AllVal'] = row.xpath ('//table').extract()
            yield item

// This is a comment
