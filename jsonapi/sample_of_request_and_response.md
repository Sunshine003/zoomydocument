# 广告请求和返回json示例

- [广告请求和返回json示例](#广告请求和返回json示例)
    - [Banner](#横幅)
        - [Banner请求示例](#Banner广告请求示例（Site）)
        - [Banner请求示例](#Banner广告请求示例（Mobile）)
        - [Banner返回示例（HTML）](#横幅|插屏|全屏广告返回示例(HTML))
    - [原生](#原生)
        - [Native请求示例](#Native请求示例)
        - [Native广告返回示例](#Native广告返回示例)

> - 使用测试参数获取的广告，仅供查看效果使用，正式上线后请切换为正式的id，否则将不会产生任何请求，展示，点击，收益等数据。

## Banner

> 开屏、插屏和横幅广告的请求、返回结构类似，不另外举例

### Banner广告请求示例（Site）

```json

{ 
    "id": "80ce30c53c16e6ede735f123ef6e32361bfc7b22", 
    "at": 1, "cur": [ "USD" ], 
    "imp": [ 
            { 
              "id": "1", 
              "banner": { "h": 250, "w": 300, "pos": 0 } 
             } 
          ], 
      "site": { 
        "id": "102855", 
        "cat": [ "IAB3-1" ], 
        "domain": "www.foobar.com", 
        "page": "http://www.foobar.com/1234.html ", 
        "publisher": { 
          "id": "8953", "name": "foobar.com", 
          "cat": [ "IAB3-1" ], "domain": "foobar.com" 
          } 
         },   
      "device": {
      "ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_6_8) AppleWebKit/537.13 (KHTML, like Gecko) Version/5.1.7 Safari/534.57.2", 
      "ip": "123.145.167.10" }, 
      "user": { 
        "id": "55816b39711f9b5acf3b90e313ed29e51665623f" 
        } 
 }

```

### Banner广告请求示例（Mobile）

```json
{ 
  "id": "IxexyLDIIk", 
  "at": 2, 
  "bcat": [ "IAB25", "IAB7-39", "IAB8-18", "IAB8-5", "IAB9-9" ], 
  "badv": [ "apple.com", "go-text.me", "heywire.com" ], 
  "imp": [ 
          { 
            "id": "1", 
            "instl": 0, 
            "tagid": "agltb3B1Yi1pbmNyDQsSBFNpdGUY7fD0FAw", 
            "banner": { 
                "w": 728, "h": 90, "pos": 1, 
                "btype": [ 4 ], 
                "battr": [ 14 ], 
                "api": [ 3 ] 
                }
            } 
         ],    
  "app": {
           "id": "agltb3B1Yi1pbmNyDAsSA0FwcBiJkfIUDA", 
           "name": "Yahoo Weather", 
           "cat": [ "IAB15", "IAB15-10" ], 
           "ver": "1.0.2", 
           "bundle": "com.yahoo.wxapp", 
           "storeurl": "https://itunes.apple.com/id628677149", 
           "publisher": { 
                "id": "agltb3B1Yi1pbmNyDAsSA0FwcBiJkfTUCV", 
                "name": "yahoo", 
                "domain": "www.yahoo.com" 
                }
         },  
  "device": { 
           "dnt": 0, 
           "ua": "Mozilla/5.0 (iPhone; CPU iPhone OS 6_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9A334 Safari/7534.48.3",  
           "ip": "123.145.167.189", 
           "ifa": "AA000DFE74168477C70D291f574D344790E0BB11", 
           "carrier": "VERIZON", 
           "language": "en", 
           "make": "Apple", 
           "model": "iPhone", 
           "os": "iOS", 
           "osv": "6.1", 
           "js": 1, 
           "connectiontype": 3, 
           "devicetype": 1,
           "geo": { 
                "lat": 35.012345, 
                "lon": -115.12345, 
                "country": "USA", 
                "metro": "803", 
                "region": "CA", 
                "city": "Los Angeles", 
                "zip": "90049" 
           },
           "ext" : {
           
           }
  }, 
  "user": { 
      "id": "ffffffd5135596709273b3a1a07e466ea2bf4fff", 
      "yob": 1984, 
      "gender": "M" 
  } 
}

```

### 横幅|插屏|全屏广告返回示例(HTML)

```json
{
    "id": "req_id",
    "seatbid": [
        {
            "bid": [
                {
                    "id": "1", 
                    "impid": "102", 
                    "nurl": "https://adserver.com/winnotice?impid=102",
                    "iurl": "https://creativeUrl.png",
                    "adm": "<a href=https://clickurl><img src=https://creativeUrl.png/> img src=https://impUrl style=display:none/>",
                    "adomain": [ "advertiserdomain.com" ],
                    "cid": "campaignId",
                    "crid": "creativeId",
                    "h": 50,
                    "w": 320
                }
            ]
        }
    ]
}
```

### 横幅|插屏|全屏广告返回示例（JSON）

```json
{
    "id": "req_id",
    "seatbid": [
        {
            "bid": [
                {
                    "adm": "{\"url\":\"http:\\/\\/mammut.vlion.cn\\/ui\\/assets\\/img\\/advimg\\/300_300.png\",\"ldp\":\"http:\\/\\/baidu.com\"}",
                    "cid": "23449_d",
                    "ext": {
                        "ad_icon": "http://c.vlion.cn/ms/tj/dsp/cornermark/arrow-ll-ad.png",
                        "ad_logo": "http://c.vlion.cn/ms/tj/dsp/cornermark/bule/arrow-max-up-a.png",
                        "clk_t": [
                            "http://test.vlion.cn:8045/sc?downx=__CLICK_DOWN_X__&downy=__CLICK_DOWN_Y__&upx=__CLICK_UP_X__&upy=__CLICK_UP_Y__&m=0&e=MTU1NjEwMDQ5NwkzMDA4NwkyMzQ0OQkJCXJlcV9pZAkwCQkxCTAJODY1NzM2MDMzNzE3MDI5CQkJCWI5OTllZDQ5ZDFkNjQ2NjQJCQkJCQ==&t=23449&f=0&g="
                        ],
                        "ctype": 2,
                        "imp_t": [
                            "http://test.vlion.cn:8045/se?e=MTU1NjEwMDQ5NwkzMDA4NwkyMzQ0OQkJCXJlcV9pZAkwCQkxCTAJODY1NzM2MDMzNzE3MDI5CQkJCWI5OTllZDQ5ZDFkNjQ2NjQJCQkJCQ==&t=23449"
                        ],
                        "instl": 0,
                        "interact_type": 0
                    },
                    "h": 50,
                    "impid": "imp_id",
                    "w": 320
                }
            ]
        }
    ]
}
```

## 原生

### Native请求示例

```json

{ 
  "id": "IxexyLDIIk", 
  "at": 2, 
  "bcat": [ "IAB25", "IAB7-39", "IAB8-18", "IAB8-5", "IAB9-9" ], 
  "badv": [ "apple.com", "go-text.me", "heywire.com" ], 
  "imp": [ 
          { 
            "id": "1", 
            "instl": 0, 
            "tagid": "agltb3B1Yi1pbmNyDQsSBFNpdGUY7fD0FAw", 
            "native": { 
                "request": "{\"ver\":\"1.0\",\"assets\":[ ... ]}", 
                "ver": "1.0", 
                "api": [ 1 ]   
             }
            } 
         ],    
  "app": {
           "id": "agltb3B1Yi1pbmNyDAsSA0FwcBiJkfIUDA", 
           "name": "Yahoo Weather", 
           "cat": [ "IAB15", "IAB15-10" ], 
           "ver": "1.0.2", 
           "bundle": "com.yahoo.wxapp", 
           "storeurl": "https://itunes.apple.com/id628677149", 
           "publisher": { 
                "id": "agltb3B1Yi1pbmNyDAsSA0FwcBiJkfTUCV", 
                "name": "yahoo", 
                "domain": "www.yahoo.com" 
                }
         },  
  "device": { 
           "dnt": 0, 
           "ua": "Mozilla/5.0 (iPhone; CPU iPhone OS 6_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9A334 Safari/7534.48.3",  
           "ip": "123.145.167.189", 
           "ifa": "AA000DFE74168477C70D291f574D344790E0BB11", 
           "carrier": "VERIZON", 
           "language": "en", 
           "make": "Apple", 
           "model": "iPhone", 
           "os": "iOS", 
           "osv": "6.1", 
           "js": 1, 
           "connectiontype": 3, 
           "devicetype": 1,
           "geo": { 
                "lat": 35.012345, 
                "lon": -115.12345, 
                "country": "USA", 
                "metro": "803", 
                "region": "CA", 
                "city": "Los Angeles", 
                "zip": "90049" 
           }
  }, 
  "user": { 
      "id": "ffffffd5135596709273b3a1a07e466ea2bf4fff", 
      "yob": 1984, 
      "gender": "M" 
  } 
  }

```
#### 原生广告BidRequest中native对象特别说明
```html

"native":{
          "ver":"1.1",
          "request":{
                "ver":"1.0",
                "layout":6,
                "plcmtcnt":1,
                "assets":[
                      {"id":0,"required":1,"title":{"len":90}},
                      {"id":1,"img":{"type":1,"wmin":50,"hmin":50}},
                      {"id":3,"data":{"type":12,"len":0}},
                      {"id":4,"data":{"type":2,"len":100}},
                      {"id":5,"img":{"type":3,"wmin":320,"hmin":320}},
                      {"id":6,"img":{"type":3,"wmin":480,"hmin":480}},
                      {"id":7,"img":{"type":3,"wmin":300,"hmin":250}},
                      {"id":8,"img":{"type":3,"wmin":320,"hmin":480}},
                      {"id":9,"img":{"type":3,"wmin":480,"hmin":320}},
                      {"id":10,"img":{"type":3,"wmin":320,"hmin":50}}
                ]
               }
     }
```

### Native广告返回示例

```json

{
    "id": "req_id",
    "seatbid": [
        {
            "bid": [
                {
                    "id": "1", 
                    "impid": "102", 
                    "nurl": "https://adserver.com/winnotice?impid=102",
                    "iurl": "https://creativeUrl.png",
                    "adm": "{\"native\":{\"ver\":\"1.0\",\"link\":{ ... }, \"imptrackers\":[ ... ],\"assets\":[ ... ]}}",
                    "adomain": [ "advertiserdomain.com" ],
                    "cid": "campaignId",
                    "crid": "creativeId",
                    "h": 50,
                    "w": 320
                }
            ]
        }
    ]
}
```

#### 原生广告BidResponse中native对象特别说明
```html

"native":
      {"link":
        {"url":"http: //i.am.a/URL"},
        "imptrackers":[
            "https://tracking.meetadver.com/tracking/imp?"
            ],
            "assets":[
                {"id":0,"title":{"text":"native test"}},
                {"id":1,"img":{"url":"https://creatives.meetadscdn.com/images/50x50.jpg"}},
                {"id":3,"data":{}},
                {"id":4,"data":{"value":"123"}},
                {"id":5,"img":{"url":"https://images/320x320.jpg"}},
                {"id":6,"img":{"url":"https://images/480x480.jpg"}},
                {"id":7,"img":{"url":"https:///300x250.jpg"}},
                {"id":8,"img":{"url":"https://images/320x480.jpg"}},
                {"id":9,"img":{"url":"https://images/480x320.jpg"}},
                {"id":10,"img":{"url":"https://images/320x50.jpg"}}
            ]
   }
```
