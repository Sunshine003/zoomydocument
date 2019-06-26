# Channel&Token注册

- [Channel&Token注册](#Channel&Token注册)
    - [请求信息](#请求信息)
        - [Request 字段信息](#Request对象)
    - [响应信息](#响应信息)
        - [Response 字段信息](#Response对象)
            - [Data 对象信息](#Data对象)


### 请求信息

当新增一个物流channel时，需要注册信息的channel和token信息

- 请求地址：咨询HQD平台

- 请求类型：POST

- Header参数：
  
  Content-Type - application/json

- Body Json格式数据:

#### Request对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
| account_id | string;required | 客户ID，由HQD物流客服提供 |
| channel | string;required | 所物流标识，由HQD物流客服提供 |
| random | string;required | 随机字符串 |
| key_string | string;required | 加密Key, 由HQD物流客服提供，不同channel，key_string不同 |

样例：
  
  ``` json
  {
    "account_id" : "AAA"
    "channel": "ABCD",
    "random": "43dssowcw",
    "key_string": "4c9d491c90fafc1e3bb34db8263116b2" 
  }
  ```

### 响应信息

#### 成功返回

- HTTP响应码: 200

- Body Json格式数据:

##### Response对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|code  | int       | 响应编码| 
|message |  string  | 响应信息，成功响应默认"success"| 
|data    | object   | 响应数据，不同请求响应返回不同数据| 


##### Data对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|channel | string | 渠道编号|
|token   | string|  注册成功的token|

样例：
  
``` json
{
  "code": 200,
  "message":  "success",
  "data": {
    "logistics_sn": "ABCD",
    "token": "4c9d491c90fafc1e3bb34db8263116b2"  
  }
}
```

#### 失败返回

- HTTP响应码： 404

- Body Json格式数据：

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|code  |   int   |   响应编码|
|message | string|  响应信息，返回失败原因|
|data  |  object |  响应数据，默认为空|


样例：

``` json
{
  "code": 404,
  "message": "失败原因",
  "data":
}
```