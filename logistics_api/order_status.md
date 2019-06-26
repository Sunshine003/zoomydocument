# 货态追踪文档协议

- [货态追踪文档协议](#货态追踪文档协议)
    - [请求信息](#请求信息)
      - [Request 字段信息](#Request对象)
    - [响应信息](#响应信息)
      - [Response 字段信息](#Response对象)
      - [OrderDetail 字段信息](#OrderDetail对象)

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
|account_id | string | 客户ID |
|channel | string | 所选物流渠道 |
|searial_no | string | 客户的订单编号，多个订单编号之间用","分割，英文逗号 |
|command | string | 1:按订单编号查询；2: 按运单编号查询 |

样例：

``` json
{
    "account_id":"AAA",
    "channel":"BBB",
    "command":"1",
    "serial_no":"1000025,1000026"
  
}
```
### 响应信息

- 内容格式：JSON format:

#### Response对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|code | string | 响应编码 |
|message | string | 响应信息，成功响应默认"success" |
|sn_str |  string | 未找到信息的No 信息 |
|orders_detail | []orderDetail | 订单详细 |

#### OrderDetail对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|order_status | string | 订单状态 |
|account_id |   string | 客户ID |
|order_no | string | 订单号 |
|express_no |   string | 运单号 |
|goods_type |   string | 货物类型,GC (General Cargo普货)/ SC (Special Cargo特货) |
|goods_name_cn | string | 中文品名,格式“商品名称1_数量&商品名称2_数量” |
|goods_name_en | string | 英文名称,格式“商品名称1_数量&商品名称2_数量” |
|goods_qty | int | 商品汇总数量 |
|weight | float64 | 订单总重量 |
|cod_amount |   float64 | COD代收款金额 |
|insurance_amount | float64 | 保险金额 |
|collect_amount | float64 | 到付运费金额 |
|price_currency | string | 币种, 三字母币种 |
|pay_type | string | 运费付款方式PP(月结)/CA(票结)/CC(到付) |
|service_type | string | 服务类型 |
|scan_list | string | 货态详情 |
|remark | string | 订单备注 |
|package_pcs |  string | 商品包裹数量，系统默认是 "1" |
|create_order_time | string | 订单创建时间 |
|old_order_no | string | 原始订单号 |
|old_express_no | string | 原始运单号 |

#### 成功返回

- HTTP响应码:200

- Body Json格式数据

样例：

``` json
{
    "code": "true",
    "message": "",
    "sn_str": "1000026",
    "orders_detail": [
        {
            "order_status": "Updating",
            "account_id": "SH",
            "order_type": "1",
            "order_no": "1000025",
            "express_no": "CGKIT00002427416",
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
            "goods_type": "GC",
            "goods_name_cn": "AAAA+BBBBB",
            "goods_name_en": "AAAA+CCCCC",
            "goods_qty": 1,
            "weight": "100",
            "cod_amount": 1,
            "insurance_price": 1,
            "price_currency": "IDR",
            "pay_type": "PP",
            "service_type": "2",
            "scan_list": "[{\"date\":\"05-01-2016 10:41\",\"desc\":\"SHIPMENT RECEIVED BY JNE COUNTER OFFICER AT [JAKARTA]\"}]",
            "remark": "",
            "create_order_time": "2019-06-25 18:56:03",
            "send_start_time": "",
            "send_end_time": "",
            "old_order_no": "",
            "old_express_no": ""
        }
    ]
}
```