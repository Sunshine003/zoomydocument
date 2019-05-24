# SSP 对接文档协议

- [SSP 对接文档协议](#ssp-对接文档协议)
    - [文档说明](#文档说明)
    - [接入准备](#接入准备)
    - [接入说明](#接入说明)
        - [请求 URL](#请求-url)
        - [通信方式及编码](#通信方式及编码)
        - [广告请求](#广告请求)
            - [请求头](#请求头)
            - [AdRequest 字段信息](#adrequest-字段信息)
                - [imp 对象信息](#imp-对象信息)
                - [app 对象信息](#app-对象信息)
                - [device 对象信息](#device-对象信息)
                - [user 对象信息](#user-对象信息)
        - [广告返回](#广告返回)
            - [AdResponse 字段信息](#adresponse-字段信息)
                - [seatbid 对象信息](#seatbid-对象信息)
                    - [bid 对象信息](#bid-对象信息)
            - [素材格式](#素材格式)
            - [上报地址宏替换信息](#上报地址宏替换信息)
            - [不填充广告原因](#不填充广告原因)

## 文档说明

此文档仅供开发者或 SSP 与 AdVlion 交易平台（ADX） 使用 API 方式对接时使用。

## 接入准备

在 开发者（SSP）和 AdVlion交易平台（ADX） 商务人员沟通后，由 AdVlion交易平台（ADX）商务人员提供 开发者 账号和密码。

## 接入说明

### 请求 URL

当需要请求广告时，发送一个 HTTP POST 请求到下面的地址`http://adx.advlion.com/ssp`

### 通信方式及编码

ADX 和 开发者（SSP） 之间的基础通信协议采用 HTTP 协议、POST 方法，数据使用 JSON 格式，编码采用 UTF-8 编码。

### BidRequest 规范

BidRequest 请求是广告位请求广告的入口，由 SSP|ADX 按本文档中规定 URL 向 DSP 发送。

#### Http 请求头设置

######JSON 数据格式

 - Content-Type:application/json
 - X-Protocol-Ver:1.0

#### BidRequest 对象

| 字段名称 | 类型 |  描述 |
| --- | --- |  --- |
| id | string;required | 唯一请求id |
| imp | object array;required | 所需广告描述，至少包含一个Imp 对象 |
| site | object | Site 信息, Site流量必须 |
| app | object | APP 信息, App流量必须 |
| device | object | 设备信息 |
| user | object | 用户信息 |
| bcat | string array | 拒绝投放的广告行业类型名单 |
| badv | string array | 广告主黑名单，采用域名标注广告主 |
| bapp | string array | 拒绝的应用名单。Android 采用bundle 或package names 标识;IOS 采用numeric IDs |

##### Imp 对象

| 字段名称 | 类型  | 描述 |
| --- | --- | --- |
| id | string;required  | 唯一曝光id |
| banner | object   | 横幅、插屏或全屏广告描述信息 |
| video | object  | 视频广告描述信息 |
| auido | object  | 音频广告描述信息 |
| native | object  | 原生广告描述信息 |
| instl | integer  | 广告位类型<br>0- 插屏,开屏<br>1- 非插屏; banner对象必填 |
| tagid | string;required  | 广告位id |
| secure | integer  | 是否支持 https 链接的标识，默认为 0<br>0- 只支持http协议<br>1- 只支持https协议<br>2-http,https协议都支持 |
| ext | object  | 扩展对象 |

##### Imp.Ext 对象

| 字段名称 | 类型  | 描述 |
| --- | --- | --- |
| fullscreen | integer  | 是否全屏广告, banner对象必填<br>0: 不是<br>1: 是 |
| dl_support_status | integer  | download支持状态<br>0: 不支持<br>1: 支持 |
| dp_support_status | integer  | deeplink支持状态<br>0: 不支持任何形式的deeplink<br>1: 支持原生deeplink链接直接跳转<br>2: 支持进入H5落地页后跳转deeplink |

##### Banner 对象

| 字段名称 | 类型  | 描述 |
| --- | --- | --- |
| w   | integer | 建议返回广告素材的宽度 |
| h   | integer   | 建议返回广告素材的高度 |
| btype| string array | 拒绝投放的图片素材类型，取值参见:图片素材类型 |
| mimes| string array  | 支持的广告素材MIME类型，如果没有任何值或缺省，则表示没有类型限制。取值参见:广告物料MIMES |
| api| integer array  | 广告位支持的API 框架标准，如果没有任何值或缺省，则表示不支持任何API框架。取值参见:API Frameworks。 |

######备注:Imp.instl = 1，Banner 对象表示插屏广告素材;Imp.fullscreen = 1，Banner 对象表示全屏广告素材; Imp.instl = 0&& Imp.fullscreen = 0,Banner 对象表示横幅广告素材

##### Video 对象

| 字段名称 | 类型 | 描述 |
| --- | --- | --- |
| w | integer | 建议返回广告素材的宽底 |
| h | integer | 建议返回广告素材的高度 |
| mimes | string array | 支持的广告素材MIME 类型，如果没有任何值或缺省，则表示没有类型限制。取值参见:广告物料MIMES |
| api | integer  array | 广告位支持的API 框架标准，如果没有任何值或缺省，则表示不支持任何API框架。取值参见:API Frameworks。 |
| minduration | integer | 支持的最小视频时长，单位: 秒 |
| maxduration | integer | 支持的最大视频时长，单位: 秒 |
| startdelay | integer | 视频广告类型是: 前贴，中贴或片尾广告。取值参见:播放延时规范 |
| linearity | integer | 支持的视频广告类型: 线性广告或非线性广告。如果没有任何在或缺省，则表示所有类型都支持。取值参见:Video Linearity |
| skip | integer | 广告是否允许被跳过:0: 不允许，1:  允许 |
| minbitrate | integer | 视频素材允许的最小Kbps |
| maxbitrate | integer | 视频素材允许的最大Kbps |
| boxingallowed | integer | 是否允许投放视频素材与广告位要求的素材比例不一致。0: 不允许，1: 允许delivery integer array 支持的delivery methods。如果没有任何值或缺省，则表示支持所有delivery methods。取值参见:Delivery Methods |
| delivery | integer array| 支持的delivery methods。如果没有任何值或缺省，则表示支持所有delivery methods。取值参见:Delivery Methods |
| protocols | integer array | 支持的协议类型。如果没有任何值或缺省，表示不支持任何特殊协议。取值参见:protocols |
| ext | object | 扩展对象

##### Video.Ext 对象

| 字段名称 | 类型  | 描述 |
| --- | --- | --- |
| maxcreative | integer  | 支持创意数量，默认值为1。Vast Creatives 中的创意数量不大于该值。 |
| rwvd | integer  | 是否激励视频广告;0: 不是，1: 是 |

##### Audio 对象

| 字段名称 | 类型  | 描述 |
| --- | --- | --- |
| mimes   | string array | 支持的广告素材MIME 类型，如果没有任何值或缺省，则表示没有类型限制。取值参见:广告物料MIMES |
| api   | integer array   | 建议返回广告素材的高度广告位支持的API 框架标准，如果没有任何值或缺省，则表示不支持任何API框架。取值参见:API Frameworks。 |
| minduration | integer | 支持的最小音频时长，单位: 秒 |
| maxduration | integer | 支持的最大音频时长，单位: 秒 |
| startdelay | integer | 音频广告类型是: 前贴，中贴或片尾广告。取值参见:播放延时规范 |
| minbitrate | integer | 音频素材允许的最小Kbps |
| maxbitrate | integer | 音频素材允许的最大Kbps |
| delivery | integer array| 支持的delivery methods。如果没有任何值或缺省，则表示支持所有delivery methods。取值参见:Delivery Methods |
| protocols | integer array | 支持的协议类型。如果没有任何值或缺省，表示不支持任何特殊协议。取值参见:protocols |

##### Native 对象

| 字段名称 | 类型  | 描述 |
| --- | --- |  --- |
| request | string;required |  请求要求的原生广告规范 |
| ver | integer | 原生广告规范版本 |
| api | integer array | 广告位支持的API 框架标准。如果没有任何值或缺省，则表示不支持任何API框架。取值参见:API Frameworks |

##### App 对象

| 字段名称 | 类型 | 描述 |
| --- | --- | --- |
| id | string | Exchange 平台定义的APP ID |
| name | string | Android:package name; IOS:Bundle ID |
| bundle | string | BundleID 或者包名 |
| domain | string | Domain of app |
| storeurl | string | APP 在应用市场的下载地址 |
| cat | string array | 应用分类 |
| sectioncat | string array | 应用当前频道分类 | 
| pagecat | string array | 应用当前页面分类 | 
| ver | string  | APP 版本号 |
| paid | integer  | 是否为付费 APP<br>0- 不是<br>1- 是<br>2- 应用内付费 |
| publisher | object | 应用发布商详情 | 
| keywords | string | APP 关键字，可以用英文逗号分隔多个 |

##### Publisher 对象

| 字段名称 | 类型 | 描述 |
| --- | --- | --- |
| id | string | Exchange-specific publisher ID. |
| name | string | Publisher 名称 |
| cat | string array | Publisher 内容分类 |
| domain | string | Publisher 主域名 |

##### device 对象

| 字段名称  | 类型  | 描述 |
| --- | --- | --- |
| ua | string | 浏览器user-agent |
| geo | object | 地理位置信息对象 |
| dnt | integer | 0- 允许广告追踪<br>1- 不允许广告追踪 |
| ip | string | 客户端IP地址。如果从客户端直接发起请求，该字段可填空字符串；如果从服务端发起请求，请填写客户端的IP |
| ipv6 | string | ipv6 |
| devicetype | integer | 设备类型<br>1- 手机<br>2- 平板 |
| make | string | 设备制造商 |
| model | string | 设备型号 |
| os | string | 设备操作系统，二选一填写 Android 或 iOS |
| osv | string | 设备操作系统版本号 |
| w | integer | 设备屏幕分辨率宽，单位为像素 |
| h | integer | 设备屏幕分辨率高，单位为像素 |
| ppi | float | 每英寸像素密度 |
| js | integer | 是否支持 Javascript 脚本<br>1-支持<br>0-不支持 |
| language | string | 设备的语言设置,使用 `alpha-2/ISO 639-1` |
| carrier | string | 设备使用的运营商：MCC+MNC的值。没有则为空字符串。参考 `http://en.wikipedia.org/wiki/Mobile_Network_Code` |
| connectiontype | integer | 设备联网类型<br>1- wifi<br>2- 2G<br>3- 3G<br>4- 4G |
| ifa | string | 设备屏幕分辨率宽，单位为像素 |
| didsha1 | string | 设备IMEI，使用SHA1 进行哈希 |
| didmd5 | string | 设备IMEI，使用MD5 进行哈希 |
| dpidsha1 | string | Android Id，使用SHA1 进行哈希 |
| dpidmd5 | string | Android Id，使用MD5 进行哈希 |
| macsha1 | string | MAC 地址，使用SHA1 进行哈希 |
| macmd5 | string | MAC 地址，使用MD5 进行哈希 |
| imei | string | Android 设备的 IMEI 值 |
| idfa | string | iOS 设备必填，IDFA 值 |
| idfv | string | iOS 设备必填，IDFV 值 |
| androidid | string | Android 设备必填，AndroidID |
| gadid | string | Android 设备选填，Google Advertising ID<br>imei 或 gadid 必填其中一个 |
| mac | string | MAC 值，没有填空字符串 |
| imsi | string | 国际移动用户识别码，储存在 SIM 卡中 |
| battery | integer | 设备电量百分比，取整数，数值区间 0~100 |
| density | float | 设备屏幕像素密度 |
| orientation | integer | 设备屏幕方向<br>0- 竖向<br>1- 横向 |

##### Geo 对象

| 字段名称 | 类别  | 描述 |
| --- | --- | --- |
| lat | float | 纬度 |
| lon | float | 经度 |
| timestamp | integer | 获取经纬度数据时的时间戳 |
| country | string | 国家，使用 `ISO-3166-1 Alpha-3` |
| region | string | 地区，使用 `ISO 3166-2` |
| city | string | 城市，使用 `http://www.unece.org/cefact/locode/service/location.html` |
| ufcoffset | integer | 本地时区，如: 中国为UTC+8 |

##### user 对象信息

| 字段名称 | 类别  | 描述 |
| --- | --- | --- |
| id | string | 用户唯一 ID |
| yob | integer | 出生年，4 位数字 |
| gender | string | 性别<br>M- 男性<br>F- 女性<br>O- 其他<br>Null- 不确定 |
| geo | object | 用户家庭位置 |

### BidResponse 对象规范

#### BidResponse 字段

| 字段名称 | 类型  | 描述 |
| --- | --- | --- |
| id | string | 对应请求中的唯一请求id |
| nbr | integer | 无正式广告填充时返回，不填充的原因，详情见[不填充广告原因](#不填充广告原因) |
| seatbid | object array | 有广告填充时返回，广告信息 |
| bidid | string | BidResponse 唯一标识，由DSP 生成 |

##### SeatBid 对象

| 字段名称 | 类型  | 描述 |
| --- | --- | --- |
| bid | array of object | 广告信息 |
| seat | string | 广告商id,目前为1 |
                                                                                
###### Bid 对象
| 字段名称 | 类型  | 描述 |
| --- | --- | --- |
| impid | string | 对应请求中的曝光id |
| cid | string | 创意id |
| w | integer | 广告物料宽度，单位：像素 |
| h | integer | 广告物料高度，单位：像素 |
| nurl | string | Win Notice URL |
| adm | string | 素材，详情见[素材格式](#素材格式)<br>图片类（HTML）：HTML<br>图片类（图片+落地页）：JSON(目前不支持)<br>原生：JSON |
| ext | object | 扩展字段 |

###### Bid.Ext 对象
| 字段名称 | 类型  | 描述 |
| --- | --- | --- |
| interact_type | integer | 用户点击行为<br>1- 浏览网页<br>2- 下载应用 |
| ad_logo | string | 广告来源LOGO图片 |
| ad_icon | string | "广告"字样图片 |
| deeplink | string | deeplink<br>如果终端安装了对应的APP，则跳转到deeplink<br>如果没有安装，则跳转普通落地页 |
| imp_t | array of string | 曝光监测，可能有多条，需要依次上报<br>监测链接中可能有宏，需要开发者替换，见[上报地址宏替换信息](#上报地址宏替换信息) |
| clk_t | array of string | 点击监测，可能有多条，需要依次上报<br>监测链接中可能有宏，需要开发者替换，见[上报地址宏替换信息](#上报地址宏替换信息) |
| ds_t | array of string | interact_type = 2 时可能返回<br>应用下载开始监测，可能有多条，需要依次上报 |
| dc_t | array of string | interact_type = 2 时可能返回<br>应用下载完成监测，可能有多条，需要依次上报 |
| ic_t | array of string | interact_type = 2 时可能返回<br>应用安装完成监测，可能有多条，需要依次上报 |
| op_t | array of string | interact_type = 2 时可能返回<br>应用打开监测，可能有多条，需要依次上报 |
| d_app_name | string | interact_type = 2 时可能返回<br>下载应用的名称 |
| d_app_icon | string | interact_type = 2 时可能返回<br>下载应用的图标 |
| d_app_pkg | string | interact_type = 2 时可能返回<br>下载应用的包名 |
| d_app_size | integer | interact_type = 2 时可能返回<br>下载应用的大小 |

#### 上报地址宏替换信息

> 客户端在触发上报信息时，必须将监测链接中的宏变量替换上报。可能出现宏
> 需要替换的宏坐标如下：

| 宏变量 | 类型 | 说明 |
| --- | --- | --- |
| {UUID} | string | 设备唯一标识<br>iOS 使用 IDFA， Android 使用 IMEI |
| {LATITUDE} | float | 地理位置信息，纬度 |
| {LONGITUDE} | float | 地理位置信息，经度 |
| {CLICK_DOWN_X} | integer | 用户点击绝对坐标宏，用于回传用户点击坐标，广告位左上角为原点<br>获取用户点击落下的X坐标 |
| {CLICK_DOWN_Y} | integer | 获取用户点击落下的绝对Y坐标 |
| {CLICK_UP_X}   | integer | 获取用户点击抬起的绝对X坐标 |
| {CLICK_UP_Y}   | integer | 获取用户点击抬起的绝对Y坐标 |
| {R_CLICK_DOWN_X} | integer | 用户点击相对坐标宏，用于回传用户点击坐标相对于广告的位置，广告位左上角为原点，获取用户按下抬起坐标与广告右下角（广告最大尺寸值）的坐标的比，之后扩大 1000 倍取整数的结果<br>获取用户点击落下的相对X坐标 |
| {R_CLICK_DOWN_Y} | integer | 获取用户点击落下的相对Y坐标 |
| {R_CLICK_UP_X}   | integer | 获取用户点击抬起的相对X坐标 |
| {R_CLICK_UP_Y}   | integer | 获取用户点击抬起的相对Y坐标 |

#### 不填充广告原因

| 状态码 | 说明 |
| --- | --- |
| 101 | 返回测试广告 |
| 102 | 无测试广告且无正式广告返回 |
| 104 | BidRequest 解析 JSON 失败 |
| 105 | 广告位id无效 |
| 302 | device.androidid 缺失 |
| 304 | device.idfa 缺失 |
| 311 | app.id 缺失 |
| 312 | app.name 缺失 |
| 313 | app.bundle 缺失 |
| 314 | app.ver 缺失 |
| 315 | device.os 缺失 |
| 316 | device.os 无效 |
| 317 | device.osv 缺失 |
| 318 | device.carrier 缺失 |
| 320 | device.connectiontype 缺失 |
| 321 | device.connectiontype 无效 |
| 322 | device.ip 缺失 |
| 323 | device.make 缺失 |
| 324 | device.model 缺失 |
| 325 | device.w 缺失 |
| 326 | device.h 缺失 |
| 327 | device.devicetype 缺失 |
| 328 | device.devicetype 无效 |
| 341 | imp.instl 缺失 |
| 342 | imp.instl 无效 |
| 351 | 请求id 缺失 |
| 352 | 曝光id 缺失 |
| 353 | device.ua 缺失 |
| 354 | device.ppi 缺失 |
| 355 | device.density 缺失 |
| 410 | device.anid 格式错误 |
| 411 | device.imei 格式错误 |
| 412 | device.ip 格式错误 |
| 414 | device.idfa 格式错误 |
| 500 | 低质量流量 |
| 900 | ADX 广告服务器内部错误，请联系平台 |
