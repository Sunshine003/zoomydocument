# 订单创建对接协议

- [订单创建对接协议](#订单创建对接协议)
    - [请求信息](#请求信息)
      - [Request 字段信息](#Request对象)
      - [Shipper 字段信息](#Shipper对象)
      - [Receiver 字段信息](#Receiver对象)
    - [响应信息](#响应信息)
      - [Response 字段信息](#Response对象)
      - [Detail 字段信息](#Detail对象)
      - [成功返回](#成功返回)
      - [失败返回](#失败返回)
            
### 请求信息

- 请求地址：咨询HQD平台

- 请求类型：POST

- Header参数：
  
  Content-Type - application/json
  
  token - 4c9d491c90fafc1e3bb34db8263116b2

- Body Json格式数据:

#### Request对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|account_id | string,必填 |   客户Id，由花千岛平台提供|
|channel_sn | string,必填 |  物流公司编号，由花千岛平台提供|
|order_no   | string,必填 | 订单编号|
|order_type | string,必填 | 订单类型，默认“1” |
|shipper | object,必填 | 订单发件人信息 |
|receiver | object,必填 | 订单收件人信息 |
|goods_type | string | 货物类型,GC (General Cargo普货)/ SC (Special Cargo特货) |
|goods_name_cn | string | 中文品名,格式“商品名称1_SKU_数量|商品名称2_SKU_数量” |
|goods_name_en | string | 英文名称,格式“商品名称1_SKU_数量|商品名称2_SKU_数量” |
|goods_qty | int | 商品汇总数量 |
|weight | double,必填 | 订单总重量 |
|cod_amount | float64,必填 | COD代收款金额 |
|insurance_amount | float64 |  保险金额 |
|collect_amount | float64 |  到付运费金额 |
|price_currency | string | 币种, 三字母币种 |
|pay_type |  string | 运费付款方式PP(月结)/CA(票结)/CC(到付) |
|service_type | string | 服务类型，默认"1",国际件 |
|remark | string | 订单备注 |
|package_pcs |  string,必填 | 商品包裹数量，系统默认是 "1" |
|old_order_no | string | 转运订单，旧订单号 |
|old_express_no|  string | 转运订单，旧运单号 | 

#### Shipper对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|name | string,必填 | 发件人姓名 |
|mobile | string,必填 | 发件人手机 |
|phone | string | 发件人电话号码 |
|email | string | 发件人邮箱 |
|postcode | string,必填 | 发件人邮政编码 |
|country_code | string | 发件人国家 |
|prov | string,必填 | 发件人省 |
|city | string,必填 | 发件人城市 |
|area | string,必填 | 发件人地区 |
|address | string,必填 | 发件人地址 |

#### Receiver对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|name | string,必填 | 收件人姓名 |
|mobile | string,必填 | 收件人手机 |
|phone | string | 收件人电话号码 |
|email | string | 收件人邮箱 |
|postcode | string,必填 | 收件人邮政编码 |
|country_code | string | 收件人国家 |
|prov | string,必填 | 收件人省 |
|city | string,必填 | 收件人城市 |
|area | string,必填 | 收件人地区 |
|address | string,必填 | 收件人地址 |

样例：

``` json
{
   "ad_channel_sn":"flowery-island",
   "order_sn":"C2019010508073000003",
   "user_name":"CarrierS",
   "order_type":1,
   "goods":[
      {
         "sn":"ZY1901XMSF00P",
         "price":{
            "value":395000.00,
            "unit":"IDR"
         },
         "num":2,
         "amount":{
            "value":790000.00,
            "unit":"IDR"
         }
      }
   ],
   "amount":{
      "value":790000.00,
      "unit":"IDR"
   },
   "receiver":{
      "name":"Muhdi",
      "email":"",
      "postcode":"92776",
      "mobile":"XXXXXXXXXXXX",
      "phone":"",
      "country_code":"IDN",
      "prov":"SULAWESI SELATAN",
      "city":"BONE",
      "area":"KAJUARA",
      "address":"XXXXXXXXXXX"
   },
   "insurance_price":{
      "num":0,
      "unit":""
   },
   "adchannel_cost":{
      "num":0,
      "unit":"USD"
   },
   "ad_pay_type":"货到付款",
   "remark":"",
   "logistic_sn":"YL",
   "ad_url":"",
   "order_time":1551753805
}
```

### 响应信息

- 内容格式：JSON format:

#### Response对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|error | string | 成功为200 失败为404 |
|msg | string | 提示信息, Success/Wrong/Token错误等信息 |
|detail |  Detail | 订单明细内容 |

#### Detail对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|logistics_sn |  string | 物流公司标识 |
|order_no | string | 订单编号 |
|express_no | string | 物流编号，成功返回值 |
|order_type | string | 订单类型 |
|shipper | Shipper | 订单发件人信息 |
|receiver | Receiver | 订单收件人信息 |
|goods_type | string | 货物类型,GC (General Cargo普货)/ SC (Special Cargo特货) |
|goods_name_cn | string | 中文品名,格式“商品名称1_数量&商品名称2_数量” |
|goods_name_en | string | 英文名称,格式“商品名称1_数量&商品名称2_数量” |
|goods_qty | int | 商品汇总数量 |
|weight |  float64 | 订单总重量 |
|cod_amount | float64 | COD代收款金额 |
|insurance_amount| float64 | 保险金额 |
|collect_amount | float64 | 到付运费金额 |
|price_currency | string | 币种, 三字母币种 |
|pay_type | string | 运费付款方式PP(月结)/CA(票结)/CC(到付) |
|service_type |  string | 服务类型 |
|remark |  string | 订单备注 |
|package_pcs | string | 商品包裹数量，系统默认是 "1" |
|error_info | string | 错误明细，失败返回值 |

#### 成功返回

- HTTP响应码: 200

- Body Json格式数据:

样例：
  
``` json
{
    "error": "200",
    "msg": "success",
    "detail": {
        "logistics_sn": "JNE",
        "order_no": "1000023",
        "order_type": "1",
        "shipper": {
            "name": "TEST PENGIRIM",
            "email": "892818700@qq.com",
            "postcode": "80552",
            "mobile": " 6281276497866",
            "phone": " 6281111111111",
            "country": "CHN",
            "prov": "DKI JAKARTA",
            "city": "JAKARTA",
            "area": "JAKARTA",
            "address": "TEST ALAMAT PENGIRIM"
        },
        "receiver": {
            "name": "TEST PENGIRIM",
            "email": "892818700@qq.com",
            "postcode": "80552",
            "mobile": " 6281276497866",
            "phone": " 6281111111111",
            "country": "CHN",
            "prov": "DKI JAKARTA",
            "city": "JAKARTA",
            "area": "JAKARTA",
            "address": "TEST ALAMAT PENGIRIM"
        },
        "goods_type": "",
        "goods_name_cn": "AAAA+BBBBB",
        "goods_name_en": "AAAA+CCCCC",
        "goods_qty": 1,
        "weight": 100,
        "cod_amount": 1,
        "insurance_price": 1,
        "price_currency": "IDR",
        "pay_type": "PP",
        "package_pcs": "1",
        "remark": "TESTING, JANGAN DILANJUT!!!",
        "express_no": "0109401900020306"
    }
}
```

#### 失败返回

- HTTP响应码： 404

- Body Json格式数据：

样例：

``` json
{
    "error": "404",
    "msg": "Transaction no. already exists, please try with another",
    "detail": {
        "express_no": "0109401900020306",
        "error_info": "Transaction no. already exists, please try with another"
    }
}
```