# Logistics&Token注册

- [Channel&Token注册](#LogisticsSn&Token注册)
    - [请求信息](#请求信息)
        - [Request 字段信息](#Request对象)
    - [响应信息](#响应信息)
        - [Response 字段信息](#Response对象)
            - [Data 对象信息](#Data对象)


### 请求信息

- 请求地址：http(s)://api.flowery-island.com/logistics/api/token

- 请求类型：POST

- Header参数：
  
  Content-Type - application/json

- Body Json格式数据:

#### Request对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
| account_id | string;required | 客户ID，由HQD物流客服提供 |
| logistics | string;required | 所物流标识，由HQD物流客服提供 |
| random | string;required | 随机字符串 |
| secret_key | string;required | 加密Key, 由HQD物流客服提供，不同logistics，需要注册不同的token信息 |

样例：
  
  ``` json
  {
    "account_id" : "AAA"
    "logistics": "ABCD",
    "random": "43dssowcw",
    "secret_key": "4c9d491c90fafc1e3bb34db8263116b2" 
  }
  ```

### 响应信息

#### 成功返回

- Body Json格式数据:

##### Response对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|status |  string  | 响应信息，成功响应默认"success"| 
|data    | object  | 响应数据，不同请求响应返回不同数据| 


##### Data对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|logistics | string | 物流信息|
|token   | string|  注册成功的token|

样例：
  
``` json
{
  "status":  "success",
  "data": {
    "logistics": "ABCD",
    "token": "4c9d491c90fafc1e3bb34db8263116b2"  
  }
}
```

#### 失败返回

- Body Json格式数据：

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
|status |  string  | 响应信息，失败响应默认"failure"| 
|message | string|  响应信息，返回失败原因|
|data  |  object |  响应数据，默认为空|


样例：

``` json
{
  "status": "failure",
  "message": "失败原因",
  "data":
}
```