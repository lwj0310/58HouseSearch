[![License: LGPL v3](https://img.shields.io/badge/License-LGPL%20v3-blue.svg)](http://www.gnu.org/licenses/lgpl-3.0)

# [地图搜租房(woyaozufang.live)](https://woyaozufang.live/)

## 这是什么?爬虫+高德地图驱动的找租房平台

- 爬虫全天不间断获取公开租房信息,汇总处理分析后落地到数据库中.

- 使用高德地图API直接在地图上展示房源位置,方便查看租房地理位置,同时提供住址到公司的路线计算（公交+地图 or 步行导航）以及预估耗时.

- 已接入【豆瓣租房小组】、【Zuber合租平台】、【蘑菇租房】、【CCB建融家园】、【58同城品牌公寓】、【58同城诚信租房】、【上海互助租房】数据展示，部分房源价格支持筛选功能,累计数据过百万,同时支持手动添加豆瓣房源爬虫任务.

- 支持个人收藏房源信息,以便筛选自己合适的房子.

## [使用教程](/使用教程.md)

## [日常更新](/日常更新.md)

## 项目代码介绍

### [HouseCrawler.Core(当前维护版本)](/HouseCrawler.Core)

- 基于dotnet core 2.0,使用了 dapper, TimeJob ,RestSharp , Jieba.net...

- 数据库使用 MySQL, 缓存使用redis

- Core项目为爬虫逻辑,Web项目为网站项目,逻辑分离

- CI自动化发布使用Jenkins +Docker(这部分有兴趣可以看下:[手把手教你用Jenkins做Docker自动化发布](https://zhuanlan.zhihu.com/p/36509817))

- appsetting.json配置和初始化MySQL脚本
  appsetting.json配置如下:

    ```json
    {
        "ConnectionStrings": {
            "MySQLConnectionString": "server=mysql地址;port=端口号;database=数据库名字;uid=账号;pwd=密码;charset='utf-8';Allow User Variables=True;Connection Timeout=30;",
            "RedisConnectionString": "redis数据库地址:端口,name=名字,keepAlive=1800,syncTimeout=10000,connectTimeout=360000,password=访问密码,ssl=False,abortConnect=False,responseTimeout=360000,defaultDatabase=1"
        },
        "CCBHomeAPIKey": "建融家园APIKey,抓包可得",
        "EncryptionConfig": {
            "CIV": "加密向量,16个16进制数字",
            "CKEY": "加密秘钥,16个16进制数字"
        },
        "EmailConfig": {
            "Account": "QQ邮箱账号",
            "Password": "QQ邮箱密码"
        }
    }
    ```
    数据库初始化脚本:[HouseCrawler.Core/Dump20180512-House-Structure.sql](/HouseCrawler.Core/Dump20180512-House-Structure.sql)

    数据库爬虫配置数据:[HouseCrawler.Core/Dump20180512-House-Config.sql](HouseCrawler.Core/Dump20180512-House-Config.sql)

### [58HouseSearch.Core(停止维护)](/58HouseSearch.Core)

- dotnet core mvc + 实时爬虫 + 地图定位展示

### [58HouseSearch(停止维护)](58HouseSearch)

- dotnet MVC 4 + 实时爬虫 + 地图定位展示
