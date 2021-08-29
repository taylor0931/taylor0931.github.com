---
title: "阿布量化周报爬虫"
date: 2021-08-29T22:41:35+08:00
tags: ["爬虫","金融"]
categories: ["数据分析"]
draft: false
---

阿布量化（）每周日会发布下一周的股票价格预测。我们基于chrome 插件 [webscraper](https://www.webscraper.io/) 做一个简单的web页面爬虫，即可拿到每周的全部股票预测数据。

<!--more-->

## 一、阿布量化

阿布量化是一个基于Python的开源的量化交易系统。

- Github开源地址：[https://github.com/bbfamily/abu](https://github.com/bbfamily/abu)

- 官网地址：[www.abuquant.com/](http://www.abuquant.com/)

- 阿布沪深周榜网页地址：[https://www.abuquant.com/rankDetail/final_score_rank](https://www.abuquant.com/rankDetail/final_score_rank)

## 二、web scraper

Web Scraper 是一个可视化的 web 爬虫配置工具，主要通过 Chrome 插件的形式来运行爬虫。

- 官网地址：[https://www.webscraper.io/](https://www.webscraper.io/)

- Chrome插件安装地址：[chrome webstore web-scraper](https://chrome.google.com/webstore/detail/web-scraper/jnhgnonknehpejjnehehllkliplmbmhn)

- 使用指南：[https://www.webscraper.io/documentation](https://www.webscraper.io/documentation)


## 二、配置导入

在 Chrome 浏览器中打开【开发者工具】（`Option + Command + I`，或者 `F12`），在 【Web Scraper】中点击 【Create new sitemap】 => 【Import Sitemap】，将上述配置信息贴在【Sitemap JSON】文本框中，然后点击 【Import Sitemap】按钮即可。

具体操作如下图：

![image-20210829230554066](https://raw.githubusercontent.com/taylor0931/pics-repo/master/img/image-20210829230554066.png)

### 2.1 配置内容

```json
{
    "_id":"abu_week",
    "startUrl":[
        "https://www.abuquant.com/rankDetail/final_score_rank/cn/week/[1-55:1]#selectExchange"
    ],
    "selectors":[
        {
            "id":"week_link",
            "type":"SelectorLink",
            "parentSelectors":[
                "_root"
            ],
            "selector":".layui-col-xs12 div:nth-of-type(1) .layui-col-xs4 a",
            "multiple":true,
            "delay":0
        },
        {
            "id":"week_price",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":"font[size='10']",
            "multiple":false,
            "regex":"[0-9,.]+",
            "delay":0
        },
        {
            "id":"delta_price",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":".module_card font[size='3']",
            "multiple":false,
            "regex":"[\\+,\\-,0-9,.,%]+",
            "delay":0
        },
        {
            "id":"percentage_price",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":".module_card font[size='3']",
            "multiple":false,
            "regex":"[0-9,.,\\+,\\-]+%",
            "delay":0
        },
        {
            "id":"mon_flag",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":".module_card:nth-of-type(4) .layui-card-header font font:nth-of-type(1)",
            "multiple":false,
            "regex":"",
            "delay":0
        },
        {
            "id":"tues_flag",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":".module_card:nth-of-type(4) .layui-card-header font font:nth-of-type(2)",
            "multiple":false,
            "regex":"",
            "delay":0
        },
        {
            "id":"wed_flag",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":".module_card:nth-of-type(4) .layui-card-header font font:nth-of-type(3)",
            "multiple":false,
            "regex":"",
            "delay":0
        },
        {
            "id":"thu_flag",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":".module_card:nth-of-type(4) .layui-card-header font font:nth-of-type(4)",
            "multiple":false,
            "regex":"",
            "delay":0
        },
        {
            "id":"fri_flag",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":".module_card:nth-of-type(4) .layui-card-header font font:nth-of-type(5)",
            "multiple":false,
            "regex":"",
            "delay":0
        },
        {
            "id":"mon_percentage",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":"span:nth-of-type(1) font",
            "multiple":false,
            "regex":"[\\+,\\-,0-9,.]+%",
            "delay":0
        },
        {
            "id":"tues_percentage",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":"span:nth-of-type(2) font",
            "multiple":false,
            "regex":"[\\+,\\-,0-9,.]+%",
            "delay":0
        },
        {
            "id":"wed_percentage",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":"span:nth-of-type(3) font",
            "multiple":false,
            "regex":"[\\+,\\-,0-9,.]+%",
            "delay":0
        },
        {
            "id":"thu_percentage",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":"span:nth-of-type(4) font",
            "multiple":false,
            "regex":"[\\+,\\-,0-9,.]+%",
            "delay":0
        },
        {
            "id":"fri_percentage",
            "type":"SelectorText",
            "parentSelectors":[
                "week_link"
            ],
            "selector":"span:nth-of-type(5) font",
            "multiple":false,
            "regex":"[\\+,\\-,0-9,.]+%",
            "delay":0
        }
    ]
}
```



