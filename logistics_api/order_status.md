# 订单状态文档协议

- [货态追踪文档协议](#订单状态文档协议)
    - [请求信息](#请求信息)
      - [Request 字段信息](#Request对象)
    - [响应信息](#响应信息)
      - [Response 字段信息](#Response对象)
      - [OrderDetail 字段信息](#OrderDetail对象)
      - [成功返回](#成功返回)
      - [失败返回](#失败返回)

### 请求信息

- 请求地址：http(s)://api.flowery-island.com/orders

- 请求类型：POST

- Header参数：
  
  Content-Type - application/json
  
  token - 客户已经注册成功的token信息

- Body Json格式数据:

#### Request对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|account_id | string | 客户ID |
|logistics | string | 所选物流 |
|serial_no | string | 客户的订单编号，多个订单编号之间用","分割，英文逗号 |
|command | string | 1:按订单编号查询；2: 按运单编号查询 |

请求头样例：

```html
  Content-Type: application/json
  token :4c9d491c90fafc1e3bb34db8263116b2

```
请求body样例：

``` json
{
    "account_id":"AAA",
    "logistics":"BBB",
    "command":"1",
    "serial_no":"1000025,1000026"
  
}
```
### 响应信息

- 内容格式：JSON format:

#### Response对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|status | string | 响应信息，成功响应默认"success" |
|message | string | 错误响应信息 |
|sn_str |  string | 未找到信息的No 信息 |
|orders_detail | []orderDetail | 订单详细 |

#### OrderDetail对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|order_status | string | 订单状态 |
|order_type | string | 订单类型 |
|order_no | string | 订单号 |
|express_no |   string | 运单号 |
|goods_status | string | 最新货态 |
|goods_status_time | string | 最新货态时间 |
|latest_scan_status | string | 最新扫描状态 |
|goods_name_cn | string | 中文品名,格式“商品名称1_数量&商品名称2_数量” |
|goods_name_en | string | 英文名称,格式“商品名称1_数量&商品名称2_数量” |
|goods_qty | int | 商品汇总数量 |
|weight | string | 订单重量 |
|billing_weight | string | 计费重量 |
|cod_amount | Price | COD代收款金额 |
|insurance_amount | Price | 保险金额 |
|collect_amount | Price | 到付运费金额 |
|service_type | string | 服务类型 |
|sender_order_time | string | 寄件时间 |
|old_order_no | string | 原始订单号 |
|old_express_no | string | 原始运单号 |
|return_reason | string | 退件原因 | 
|return_detail | string | 退件详情 | 
|problem_reason | string | 问题件原因 | 

#### 成功返回

- Body Json格式数据

样例：

``` json
{
    "code": "success",
    "message": "",
    "sn_str": "1000026",
    "orders_detail": [
        {
            "order_status": "退件",
            "order_type": "1",
            "order_no": "1000025",
            "express_no": "CGKIT00002427416",
            "goods_status": "拒收",
            "goods_status_time": "2019-08-26 15:46:53",
            "latest_scan_status": "末端派件",
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
            "goods_name_cn": "AAAA_1&BBBBB_2",
            "goods_name_en": "AAAA_1&BBBBB_2",
            "goods_qty": 3,
            "weight": "100",
            "cod_amount": {"value":1, "uint": "IDR"},
            "insurance_amount": {"value":1, "uint": "IDR"},
            "collect_amount": {"value":1, "uint": "IDR"},
            "service_type": "1",
            "sender_order_time": "2019-6-25 18:56:03",
            "old_order_no": "",
            "old_express_no": ""
        }
    ]
}
```

#### 失败返回

- Body Json格式数据

样例：

``` json
{
    "status": "failure",
    "message": "错误原因",
    "orders_detail": 
}
```