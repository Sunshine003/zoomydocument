# 货态详情文档协议

- [货态追踪文档协议](#货态详情文档协议)
    - [请求信息](#请求信息)
      - [Request 字段信息](#Request对象)
    - [响应信息](#响应信息)
      - [Response 字段信息](#Response对象)
      - [OrderDetail 字段信息](#OrderDetail对象)
      - [成功返回](#成功返回)
      - [失败返回](#失败返回)

### 请求信息

- 请求地址：http(s)://api.flowery-island.com/logistics/api/orders_tracking_detail/list

- 请求类型：POST

- Header参数：
  
  Content-Type - application/json
  
  token - 4c9d491c90fafc1e3bb34db8263116b2

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
|scan_list | string | 货态详情 |
|create_order_time | string | 订单创建时间 |
|order_no | string | 订单号 |
|express_no |   string | 运单号 |
|old_order_no | string | 原始订单号 |
|old_express_no | string | 原始运单号 |

#### 成功返回

- Body Json格式数据

样例：

``` json
{
    "status": "success",
    "sn_str": "1000026",
    "orders_detail": [
        {
            "order_status": "Updating",
            "order_type": "1",
            "scan_list": "[{\"date\":\"05-01-2016 10:41\",\"desc\":\"SHIPMENT RECEIVED BY JNE COUNTER OFFICER AT [JAKARTA]\"}]",
            "create_order_time": "2019-06-25 18:56:03",
            "order_no": "1000025",
            "express_no": "CGKIT00002427416",
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