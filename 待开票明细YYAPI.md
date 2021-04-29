
# 待开票明细管理YYAPI

> **修改历史**
> 
> | 版本号 | 变更日期   | 变更内容                                                                                                                                                                                     | 变更人 | 批准 |
> | :----- | :--------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :----: | :--: |
> | V2.0  | 2021-03-16 | 销售管理模块对接相关修改 <br> 1.修改待开票明细新增接口，支持负数单据，增加lydjlx、lymxid、revurl、zdzfbz字段 <br>   2.增加删除接口 <br>  3.增加作废接口  <br>4.增加查询界面相关接口  <br>5.完善回调说明 | 梁吉明 |      |

[TOC]


----------

## 待开票明细新增单据
### 请求说明
> URL:``http://<HOST>:< PORT>/output-tax/yyapi/invoice-will/save``
> 格式：application/json; charset=UTF-8
> http请求方式：POST
> 编码类型：UTF-8

----------

### 请求头参数

>| 参数   |     类型 | 是否必填 |   描述   | 备注           |
>| :--- | -----: | :--: | :----: | ------------ |
>| sign | String |  是   | 请求签名信息 | 使用JWT生成token |

> JWT签名说明详见 https://jwt.io/，各类编程语言参考官网的支持列表。
> 一个JWT实际上就是一个字符串，它由三部分组成，头部、载荷与签名。
> **注意事项**<font color ="red">
> 1、签名使用的密钥必须必须与平台appid注册的一致
> 2、具体使用方式参考[样例代码](#样例代码)示例

----------

### 请求体参数
>| 参数           | 是否必填 | 类型   |       描述        |                                   说明                                   |
>| :------------ | :------ | :----- | ---------------- | ------------------------------------------------------------------------ |
>| djqqlsh       | 是       | String | 单据请求流水号     |                                                                          |
>| orgCode       | 是       | String | 开票点编码        |                                                                          |
>| lydjlx        | 否       | String | 来源单据类型       | V2.0新增字段，枚举值1：YS-YB-SO                                            |
>| lyid          | 否       | String | 来源id            |                                                                          |
>| lydjh         | 是       | String | 来源单据号         | V2.0新增字段，最长支持40个字符                                              |
>| gmfMc         | 是       | String | 购买方名称        |                                                                          |
>| gmfDzdh       | 否       | String | 购买方地址电话     |                                                                          |
>| gmfNsrsbh     | 否       | String | 购买方纳税人识别号 |                                                                          |
>| gmfYhzh       | 否       | String | 购买方银行账户     |                                                                          |
>| revurl1       | 否       | String | 回调url地址1      | V2.0新增字段   开具蓝票、开具红票、作废均回调此地址，[回调说明](#回调数据样例) |
>| revurl2       | 否       | String | 回调url地址2      | V2.0新增字段   开具蓝票、开具红票、作废均回调此地址，[回调说明](#回调数据样例) |
>| revurl3       | 否       | String | 回调url地址3      | V2.0新增字段   开具蓝票、开具红票、作废均回调此地址，[回调说明](#回调数据样例) |
>| lc            | 否       | String | 联次              |                                                                          |
>| bz            | 否       | String | 备注              |                                                                          |
>| fplx          | 否       | String | 发票类型          | 默认1，1：增值税电子普通发票  3：增值税普通发票 4：增值税专用发票             |
>| invoiceWillBs |         |        | 待开票明细        |                                                                          |
>| xmmc          | 是       | String | 商品名称          | 匹配商品档案，档案中商品名称不唯一                                          |
>| lyid          | 否       | String | 来源id            | V2.0新增字段                                                              |
>| lymxid        | 否       | String | 来源明细id        | V2.0新增字段                                                              |
>| spbm          | 否       | String | 商品编码          | 匹配商品档案，档案中商品编码唯一                                            |
>| spssflbm      | 否       | String | 商品税收分类编码   | yb环境下分类编码需要输入                                                   |
>| sl            | 是       | String | 税率              | yb环境下分类编码需要输入                                                   |
>| xmjshj        | 是       | Double | 项目价税合计       |                                                                          |
>| hh            | 是       | String | 行号              |                                                                          |
>| zdrq          | 是       | String | 制单日期          | 格式为yyyy-MM-dd                                                          |



```json
{
	"djqqlsh":"单据请求流水号",
	"orgCode":"组织编码",
	"lydjlx":"1",
	"lyid":"1",
	"gmfMc":"购买方名称",
	"gmfDzdh":"",
	"gmfNsrsbh":"",
	"gmfYhzh":"",
	"revurl1":"http://",
	"lc":"",
	"bz":"",
	"fplx":"",
	"zdrq ":"",
	"invoiceWillBs":[{
		"xmmc":"项目(商品)名称",
		"xmjshj":"价税合计",
		"hh":"行号",
		"spbm":"商品编码税收分类编码",
	    "lyid":"来源id",
		"lymxid":"来源明细id",
    }]

```

----------
### 返回结果说明

>| 参数   | 类型     | 描述   | 说明              |
>| :--- | ------ | :--- | :-------------- |
>| code | String | 状态码  | [详见状态码说明](#状态码) |
>| msg  | String | 信息说明 |                 |

#### 返回样例
```json
{
    "code":"0000",
    "msg":"success"
}
```
----------

## 待开票明细删除
### 请求说明
> URL:``http://<HOST>:< PORT>/output-tax/yyapi/invoice-will/delete``
> 格式：application/json; charset=UTF-8
> http请求方式：POST
> 编码类型：UTF-8

----------
### 请求头参数

>| 参数 |   类型 | 是否必填 |    描述     |
>| :--- | -----: | :-----: | ----------- |
>| sign | String |   是    | 请求签名信息 |

> JWT签名说明详见 https://jwt.io/，各类编程语言参考官网的支持列表。
> 一个JWT实际上就是一个字符串，它由三部分组成，头部、载荷与签名。
> **注意事项**<font color ="red">
> 1、签名使用的密钥必须必须与平台appid注册的一致

----------
### 请求体参数
>| 参数     | 是否必填 | 类型   |     描述      | 说明 |
>| :------ | :------ | :----- | ------------- | ---- |
>| lyid    | 否      | String | 来源id        |      |
>| djqqlsh | 是      | String | 单据请求流水号 |      |

----------
#### 请求样例
```json
{

​    "lyid" : “来源id”,
​    "djqqlsh" : “单据请求流水号”
}
```
----------
### 返回结果说明

>| 参数 |  类型  | 描述     | 说明                                                 |
>| :--- | ------ | :------ | :--------------------------------------------------- |
>| code | String | 状态码   | 0000-查询成功;1002-数据不存在;[详见状态码说明](#状态码) |
>| msg  | String | 信息说明 |                                                      |

#### 返回样例
```json
{
    "code": "0000",
    "msg": "SUCCESS"
}
```

----------

## 待开票明细作废
### 请求说明
> URL:``http://<HOST>:< PORT>/output-tax/yyapi/invoice-will/invalid``
> 格式：application/json; charset=UTF-8
> http请求方式：POST
> 编码类型：UTF-8

----------
### 请求头参数

>| 参数 |   类型 | 是否必填 |    描述     |
>| :--- | -----: | :-----: | ----------- |
>| sign | String |   是    | 请求签名信息 |

> JWT签名说明详见 https://jwt.io/，各类编程语言参考官网的支持列表。
> 一个JWT实际上就是一个字符串，它由三部分组成，头部、载荷与签名。
> **注意事项**<font color ="red">
> 1、签名使用的密钥必须必须与平台appid注册的一致

----------
### 请求体参数
>| 参数     | 是否必填 | 类型   |     描述      | 说明 |
>| :------ | :------ | :----- | ------------- | ---- |
>| lyid    | 否      | String | 来源id        |      |
>| djqqlsh | 是      | String | 单据请求流水号 |      |

----------
#### 请求样例
```json
{

​    "lyid" : “来源id”,
​    "djqqlsh" : “单据请求流水号”
}
```
----------
### 返回结果说明

>| 参数 |  类型  | 描述     | 说明                                                 |
>| :--- | ------ | :------ | :--------------------------------------------------- |
>| code | String | 状态码   | 0000-查询成功;1002-数据不存在;[详见状态码说明](#状态码) |
>| msg  | String | 信息说明 |                                                      |

#### 返回样例
```json
{
    "code": "0000",
    "msg": "SUCCESS"
}
```

----------

## 待开票明细查询页面
### 请求说明
> URL:``http://<HOST>:< PORT>/output-tax/yyapi/invoice-will/query``
> 格式：application/x-www-form-urlencoded; charset=UTF-8
> http请求方式：Post
> 编码类型：UTF-8

----------
### 请求头参数

>| 参数 |   类型 | 是否必填 |    描述     |
>| :--- | -----: | :-----: | ----------- |
>| sign | String |   是    | 请求签名信息 |

> JWT签名说明详见 https://jwt.io/，各类编程语言参考官网的支持列表。
> 一个JWT实际上就是一个字符串，它由三部分组成，头部、载荷与签名。
> **注意事项**<font color ="red">
> 1、签名使用的密钥必须必须与平台appid注册的一致

----------
### 请求体参数
>| 参数             | 是否必填 | 类型   |     描述      | 说明 |
>| :--------------- | :------ | :----- | ------------- | ---- |
>| lyid             | 否       | String | 来源id        |      |
>| djqqlsh          | 是       | String | 单据请求流水号 |      |
>| yht_access_token | 是       | String |               |      |

----------
#### 请求样例

lyid=12345678901234567890&djqqlsh=12345678901234567890&  yht_access_token=12345678901234567890

----------
### 返回结果说明

>| 参数   |  类型  | 描述     | 说明                                                 |
>| :---- | ------ | :------- | :--------------------------------------------------- |
>| code  | String | 状态码   | 0000-查询成功;1002-数据不存在;[详见状态码说明](#状态码) |
>| msg   | String | 信息说明 |                                                      |
>| datas | String | 地址信息 | 单据号对应的单据明细信息页面地址                        |

#### 返回样例
```json
{
    "code": "0000",
    "datas": "http://<HOST>:< PORT>/ent-views/index.html#/system-docking/invoice-detail?type=invoice&serviceCode=TAXOT0106&hid=1382971465429467136",
    "msg": "SUCCESS"
}
```

## 待开票明细查询
### 请求说明
> URL:``http://<HOST>:< PORT>/output-tax/yyapi/invoice-will/result?yht_access_token=XXXXX``
> 格式：application/json; charset=UTF-8
> http请求方式：POST
> 编码类型：UTF-8

----------

### 请求头参数

>| 参数   |     类型 | 是否必填 |   描述   | 备注           |
>| :--- | -----: | :--: | :----: | ------------ |
>| sign | String |  是   | 请求签名信息 | 使用JWT生成token |

> JWT签名说明详见 https://jwt.io/，各类编程语言参考官网的支持列表。
> 一个JWT实际上就是一个字符串，它由三部分组成，头部、载荷与签名。
> **注意事项**<font color ="red">
> 1、签名使用的密钥必须必须与平台yht_access_token注册的一致
> 2、具体使用方式参考[样例代码](#样例代码)示例

----------

### 请求体参数
>| 参数     | 是否必填 | 类型   |     描述      | 说明 |
>| :------- | :------ | :----- | ------------- | ---- |
>| lyid     | 否      | String | 来源id        |      |
>| djqqlsh  | 是      | String | 单据请求流水号 |      |
>| orgCode  | 是      | String | 开票点编码     |      |
>| pageNum  | 是      | int    | 页码          |      |
>| pageSize | 是      | String | 每页数据数量   |      |
```
{
	"lyid":"so001",
	"djqqlsh":"",
	"orgCode":"组织编码",
	"pageNum":1,
	"pageSize":15
}

```

----------

### 返回结果说明

>| 参数   | 类型     | 描述   | 说明              |
>| :--- | ------ | :--- | :-------------- |
>| code | String | 状态码  | [详见状态码说明](#状态码) |
>| msg  | String | 信息说明 |                 |
>| accountNote| String | 记账备注|                 |
>| accountStatus| String | 记账状态：1-未记账 2-已记账|                 |
>|accountTime | String |记账日期 yyyy-MM-dd |  |
>|accountUser | String  |记账人 |  |
>|accountVoucherNo | String |记账凭证号 |  |
>|bz|String|备注|
>|djqqlsh|String|单据请求流水号|
>|fhr|String|复核人|
>|fplx | String  |1-增值税电子普通发票 2-增值税电子专用发票 3-增值税普通发票 4-增值税专用发票 5-机动车销售统一发票 6-货物运输业增值税专用发票 8-增值税电子普通发票(成品油) 9-成品油普通发票(卷式) 10-增值税普通发票(成品油) 11-增值税专用发票(成品油) 12-增值税普通发票(卷式) |  |
>|gmfDzdh|String|购买方地址电话|
>|gmfMc|String|购买方名称|
>|gmfNsrsbh|String|购买方纳税人识别号、
>|gmfYhzh|String|购买方银行账户|
>|hisJe |Double|已开票金额 |  |
>|hisSe |Double|已开票税额 |  |
>|je | Double | 单据金额|  |
>|jshj | Double  |单据价税合计 |  |
>|kpr|String|开票人|
>|lyid|String|单据号|
>|orgName|String|组织编码|
>|se|Double|税额|
>|skr|String|收款人
>|unJe | Double |待开票金额 |  |
>|xsfDzdh|String|销售方地址电话|
>|xsfMc|String|销售方名称|
>|xsfNsrsbh|String|销售方纳税人识别号|
>|xsfYhzh|String|销售方银行账户|
>|lc|Integer|联次 2-二联 3-三联 5-五联|
>|zdrq|String|制单日期|
>|dw|String|单位|
>|hh|String|行号|
>|hisJe|Double|已开票金额|
>|hisJshj|Double|已开票价税合计|
>|se|Double|税额|
>|sl|Double|税率|
>|spbm|String|商品编码|
>|spssflbm|String|商品税收分类编码|
>|xmje|Double|项目金额|
>|xmjshj|Double|项目价税合计|
>|xmmc|String|项目名称|
>|bred|String|是否被红冲   Y-被红冲 N-正常|
>|fpDm|String|发票代码|
>|fpHm|String|发票号码|
>|fplx|String|发票类型|
>|fpqqlsh|String|开票请求流水号|
>|hh|String|行号|
>|se|Double|税额|
>|sl|Double|税率|
>|status|String|发票状态  1-待开票 2-开票中 3-开票失败 4-开票成功|
>|xmje|Double|项目金额|
>|xmjshj|Double|项目价税合计|
>|zfbz|String|是否作废  Y=已作废，N-未作废，|




#### 返回样例
```json
{
    "code":"0000",
    "datas":{
        "dtos":[
            {
                "accountNote":"32",
                "accountStatus":"2",
                "accountTime":1592150400000,
                "accountVoucherNo":"32",
                "bz":"",
                "djqqlsh":"1272434265238585345",
                "fhr":"",
                "fplx":"",
                "gmfDzdh":"",
                "gmfMc":"123123",
                "gmfNsrsbh":"",
                "gmfYhzh":"",
                "hisJe":10,
                "hisSe":1,
                "invoiceWillBs":[
                    {
                        "dw":"",
                        "hh":"1",
                        "hisJe":10,
                        "hisJshj":11,
                        "records":[
                            {
                                "bred":"N",
                                "fpDm":"144005044197",
                                "fpHm":"65264302",
                                "fplx":"1",
                                "fpqqlsh":"1272447230817132544",
                                "hh":"0",
                                "se":1,
                                "sl":0.1,
                                "status":"4",
                                "xmje":10,
                                "xmjshj":11,
                                "zfbz":"N"
                            }
                        ],
                        "se":1,
                        "sl":0.1,
                        "spbm":"污水处理费",
                        "spssflbm":"2010300000000000000",
                        "xmje":10,
                        "xmjshj":11,
                        "xmmc":"污水处理费"
                    }
                ],
                "je":10,
                "jshj":11,
                "kpr":"",
                "lyid":"",
                "orgName":"0000ceshi",
                "se":1,
                "skr":"",
                "unJe":0,
                "xsfDzdh":"北京市海淀区北清路68号 010-86396688",
                "xsfMc":"太极计算机股份有限公司",
                "xsfNsrsbh":"111222333456111",
                "xsfYhzh":"一",
                "zdrq":"2020-06"
            }
        ],
        "totalCount":1
    },
    "msg":"SUCCESS"
}
```
##  回调数据样例

```json

{
    "id": 1291549930190450700,
    "djqqlsh": "1291549930190450689",
    "corpId": "1937501a-b06f-4bf6-87d6-d5b515dacd26",
    "orgId": 12011618,
    "orgName": "0000ceshi",
    "code": "1291549930190450690",
    "fplx": "1",
    "xsfNsrsbh": "111222333456111",
    "xsfMc": "太极计算机股份有限公司",
    "xsfDzdh": "北京市海淀区北清路68号 010-86396688",
    "xsfYhzh": "七八九十一二三四五六七八231123131",
    "gmfNsrsbh": "123456789012345",
    "gmfMc": "jackhui141",
    "gmfDzdh": "中关村科技园腾讯大厦",
    "gmfYhzh": "中国人民银行",
    "kpr": "开票人",
    "skr": "",
    "fhr": "",
    "lc": 2,
    "bz": "",
    "lylx": "1",
    "lyid": "",
    "creator": "7ae11f43-e591-4634-a465-00cad57915f3",
    "zdrq": "2020-08-07",
    "accountStatus": "1",
    "je": 14.28,
    "jshj": 15,
    "createTime": 1596764474000,
    "ts": 1596764706000,
    "isBilling": "1",
    "se": 0.72,
    "hisJe": 14.28,
    "unJe": 0,
    "hisSe": 0.72,
    "redInfos": [],
    "enableRed": false,
    "invoiceWillBs": [
        {
            "id": 1291549930656018400,
            "hh": "1",
            "spbm": "1288294598931034112",
            "xmmc": "冬枣",
            "spssflbm": "1030299000000000000",
            "ggxh": "11",
            "dw": "",
            "xmhsdj": 3.333333,
            "xmsl": 1.5,
            "xmje": 4.76,
            "sl": 0.05,
            "se": 0.24,
            "xmjshj": 5,
            "hisJe": 4.76,
            "hisJshj": 5,
            "hisSpsl": 1.5,
            "createTime": 1596764474000,
            "lymxid": "111",
            "lyid": "222",
            "ts": 1618571221000,
            "isBilling": "1",
            "records": [
                {
                    "id": 1291550791943762000,
                    "fplx": "1",
                    "hh": "1",
                    "fpqqlsh": "1291550791243313152",
                    "fpDm": "383952242045",
                    "fpHm": "09703033",
                    "kprq": "2020-09-03 14:51:56",
                    "xmsl": 1.5,
                    "xmhsdj": 3.33,
                    "xmje": 4.76,
                    "xmjshj": 5,
                    "se": 0.24,
                    "sl": 0.05,
                    "status": "4",
                    "zfbz": "N",
                    "bred": "N",
                    "czrq": "2020-08-07",
                    "createTime": "2020-08-07 09:45:06",
                    "ts": 1599115932000,
                    "bid": 1291549930656018400,
                    "hid": 1291549930190450700
                }
            ],
            "lslbs": "",
            "hid": 1291549930190450700
        },
        {
            "id": 1291549930656018400,
            "hh": "2",
            "spbm": "1288294598931034112",
            "xmmc": "冬枣",
            "spssflbm": "1030299000000000000",
            "ggxh": "11",
            "dw": "",
            "xmhsdj": 3.333333,
            "xmsl": 3,
            "xmje": 9.52,
            "sl": 0.05,
            "se": 0.48,
            "xmjshj": 10,
            "hisJe": 9.52,
            "hisJshj": 10,
            "hisSpsl": 3,
            "createTime": 1596764474000,
            "lymxid": "111",
            "lyid": "111",
            "ts": 1618571224000,
            "isBilling": "1",
            "records": [
                {
                    "id": 1291550791943762000,
                    "fplx": "1",
                    "hh": "2",
                    "fpqqlsh": "1291550791243313152",
                    "fpDm": "383952242045",
                    "fpHm": "09703033",
                    "kprq": "2020-09-03 14:51:56",
                    "xmsl": 3,
                    "xmhsdj": 3.33,
                    "xmje": 9.52,
                    "xmjshj": 10,
                    "se": 0.48,
                    "sl": 0.05,
                    "status": "4",
                    "zfbz": "N",
                    "bred": "N",
                    "czrq": "2020-08-07",
                    "createTime": "2020-08-07 09:45:06",
                    "ts": 1599115932000,
                    "bid": 1291549930656018400,
                    "hid": 1291549930190450700
                }
            ],
            "lslbs": "",
            "hid": 1291549930190450700
        }
    ]
}


```

### 回调服务发票详细信息

- 发票头数据

>| 参数           |  类型  | 描述                                   | 说明 |
>| :------------ | ------ | :------------------------------------ | :--- |
>| djqqlsh       | String | 单据请求流水号                          |      |
>| corpId        | String | 企业（集团）编码                        |      |
>| fplx          | String | 发票类型                               |      |
>| xsfNsrsbh     | String | 销售方纳税人识别号                      |      |
>| xsfMc         | String | 销售方名称                             |      |
>| xsfDzdh       | String | 销售方地址、电话                        |      |
>| xsfYhzh       | String | 销售方银行、账户                        |      |
>| gmfDzdh       | String | 购买方地址、电话                        |      |
>| gmfMc         | String | 购买方名称                             |      |
>| gmfNsrsbh     | String | 购买方纳税人识别号                      |      |
>| gmfYhzh       | String | 购买方银行、账户                        |      |
>| kpr           | String | 开票人                                 |      |
>| fhr           | String | 复核人                                 |      |
>| skr           | String | 收款人                                 |      |
>| bz            | String | 备注                                   |      |
>| lc            | String | 联次 2-二联 3-三联 5-五联               |      |
>| lylx          | String | 来源类型1-手工开具 2-接口传入 3-文件导入 |      |
>| lyid          | String | 来源id                                 |      |
>| zdrq          | String | 制单日期                               |      |
>| accountStatus | String | 记账状态 1-未记账 2-已记账'             |      |
>| creator       | String | 创建人id                               |      |
>| je            | String | 金额                                   |      |
>| jshj          | String | 价税合计                               |      |
>| isBilling     | String | 单据是否开过票（1-开过  0-没开过）       |      |
>| se            | String | 税额                                   |      |
>| orgName       | String | 组织名称                               |      |
>| hisJe         | String | 已开票金额                             |      |
>| unJe          | String | 待开票金额                             |      |
>| hisSe         | String | 已开票税额                             |      |
>| enableRed     | String | 红冲按钮[true/false]                   |      |
>| zdzfbz        | String | 单据是否整单作废                        |      |
>| invoiceWillBs | List   | 单据明细行数据                          |      |

- 发票明细行数据

>| 参数      |  类型  | 描述                                                               | 说明 |
>| :-------- | ------ | :---------------------------------------------------------------- | :--- |
>| xmmc      | String | 项目名称                                                           |      |
>| lyid      | String | 来源id                                                             |      |
>| lymxid    | String | 来源明细id                                                         |      |
>| ggxh      | String | 规格型号                                                           |      |
>| dw        | String | 单位                                                               |      |
>| xmsl      | doube  | 项目数量                                                           |      |
>| xmdj      | doube  | 项目单价                                                           |      |
>| xmje      | doube  | 项目金额                                                           |      |
>| xmjshj    | String | 项目价税合计                                                       |      |
>| sl        | String | 税率                                                               |      |
>| se        | String | 税额                                                               |      |
>| hh        | string | 行号                                                               |      |
>| spbm      | string | 商品编码                                                           |      |
>| spssflbm  | string | 商品税收分类编码                                                    |      |
>| xmhsdj    | string | 含税单价                                                           |      |
>| hisJe     | string | 已开票金额                                                         |      |
>| hisJshj   | string | 已开票价税合计                                                      |      |
>| hisSpsl   | string | 已开票商品数量                                                      |      |
>| isBilling | string | 单据是否开过票（1-开过  0-没开过）                                   |      |
>| lslbs     | string | 零税率标识；空：非零利率，0：出口退税，1：免税，2：不征收，3普通零税率' |      |
>| records   | List   | 开票记录数据                                                       |      |

- 发票开票记录数据

>| 参数        |  类型  | 描述                                               | 说明 |
>| :--------- | ------ | :------------------------------------------------ | :--- |
>| fplx       | String | 发票类型                                           |      |
>| fpqqlsh    | String | 发票请求流水号                                      |      |
>| fpDm       | String | 发票代码                                           |      |
>| fpHm       | String | 发票号码                                           |      |
>| kprq       | String | 开票日期                                           |      |
>| xmsl       | String | 条目数量                                           |      |
>| xmhsdj     | String | 发票类型                                           |      |
>| xmje       | String | 开票金额                                           |      |
>| xmjshj     | String | 开票价税合计                                       |      |
>| se         | String | 开票税额                                           |      |
>| sl         | String | 税率                                               |      |
>| status     | String | 状态 1-待开票 2-开票中 3-开票失败 4-开票成功'        |      |
>| zfbz       | String | 作废标志；Y=已作废，N-未作废，I=正在作废，F=作废失败' |      |
>| bred       | String | 是否被红冲 Y-被红冲 N-正常                          |      |
>| czrq       | String | 操作日期                                           |      |
>| createTime | String | 创建时间                                           |      |
>| hid        | String | 未开票表头id                                       |      |
>| bid        | String | 未开票明细id                                       |      |


### 回调服务返回结果
回调服务对回调信息处理后，需要返回处理结果信息。
返回参数约定如下：
>| 参数 |  类型  | 描述            | 说明                                         |
>| :--- | ------ | :-------------- | :------------------------------------------- |
>| code | String | 处理结果编码     | 0000：表示回调服务处理成功                     |
>| msg  | String | 处理结果明细信息 | 回调处理的明细信息。如果存在错误，此处为错误信息 |

#### 返回样例
```json
{
    "code": "0000",
    "msg": "SUCCESS"
}
```

## 附录

### 状态码
>| 状态码  | 说明         |
>| :--- | ---------- |
>| 0000 | 操作成功       |
>| 1001 | 数据不合法，传入参数 |
>| 1002 | 数据不存在      |
>| 9999 | 未知错误       |

----------

### 样例代码

#### **Java（适用于JDK1.6及其更高版本）**
##### **Maven配置文件依赖**
依赖配置如下
```xml
		<!-- httpclient，发送HTTP请求 -->
		<dependency>
			<groupId>org.apache.httpcomponents</groupId>
			<artifactId>httpclient</artifactId>
			<version>4.5</version>
		</dependency>
		<!-- gson，json转换工具 -->
		<dependency>
			<groupId>com.google.code.gson</groupId>
			<artifactId>gson</artifactId>
			<version>2.7</version>
		</dependency>
		<!-- jjwt，Java Web Token签名工具包 -->
		<dependency>
			<groupId>io.jsonwebtoken</groupId>
			<artifactId>jjwt</artifactId>
			<version>0.6.0</version>
		</dependency>
```
##### **API调用代码**
```java
import com.google.gson.GsonBuilder;
import com.yonyou.einvoice.einvoiceApply.JwtParamBuilder;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.impl.compression.CompressionCodecs;
import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.HttpClient;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.conn.ssl.SSLConnectionSocketFactory;
import org.apache.http.conn.ssl.TrustStrategy;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.message.BasicHeader;
import org.apache.http.protocol.HTTP;
import org.apache.http.ssl.SSLContextBuilder;
import org.apache.http.util.EntityUtils;
import org.bouncycastle.util.io.pem.PemReader;
import javax.net.ssl.HostnameVerifier;
import javax.net.ssl.SSLContext;
import javax.net.ssl.SSLSession;
import java.io.FileInputStream;
import java.io.FileReader;
import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.security.*;
import java.security.cert.CertificateException;
import java.security.spec.InvalidKeySpecException;
import java.security.spec.PKCS8EncodedKeySpec;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

/**
 * @date 2018/5/25
 * <p>
 * 扫码开票接口测试代码，适用于JDK1.6及更高版本，jdk1.6版本需要对签名方法稍做修改，修改方法在签名方法内已经写明
 * 请求参数的注意事项也在参数构建的过程中写明，请详细阅读样例代码。
 */

public class InsertForQRInvoice {

    //测试环境有测试appid和证书，正式环境有正式appid和证书，请务必对应使用
    //测试环境appid就用这个，正式环境需要替换成正式的
    private static String APPID = "commontesterCA";
    //这个是测试环境的域名，正式环境为https://fapiao.yonyoucloud.com
    private static String DOMAIN = "https://yesfp.yonyoucloud.com";
    private static String URL = DOMAIN + "/input-tax/api/pit/report/import?appid=" + APPID;
    //pro22.pfx为测试环境通讯证书，正式环境需要替换成正式的
    private static String KEYPATH = "src/main/resources/certificate/pro22.pfx";
    //证书密码
    private static String PASSWORD = "password";

    public static void main(String[] args) {
        try {
            new InsertForQRInvoice().callQRInvoiceApply();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static CloseableHttpClient createSSLClientDefault() {
        try {
            SSLContext sslContext = new SSLContextBuilder().loadTrustMaterial(null, new TrustStrategy() {
                @Override
                public boolean isTrusted(java.security.cert.X509Certificate[] chain, String authType) throws CertificateException {
                    return true;
                }
            }).build();

            SSLConnectionSocketFactory sslsf = new SSLConnectionSocketFactory(sslContext, new HostnameVerifier() {
                @Override
                public boolean verify(String s, SSLSession sslSession) {
                    return true;
                }
            });
            return HttpClients.custom().setSSLSocketFactory(sslsf).build();
        } catch (KeyManagementException e) {
            e.printStackTrace();
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
        } catch (KeyStoreException e) {
            e.printStackTrace();
        }
        return HttpClients.createDefault();
    }

    public void callQRInvoiceApply() throws Exception {
//        提供两种构建HttpClient实例的方法，如果使用被注释掉的方法构建实例报证书不被信任的错误，那么请使用未被注释的构建方法
//        HttpClient httpClient = HttpClients.custom().build();
        HttpClient httpClient = createSSLClientDefault();    //信任所有https证书
        HttpPost httpPost = new HttpPost(URL);

        // 构造POST请求体
        String body = this.buildRequestDatas();
        // 签名
        String sign = this.sign(body);
        httpPost.addHeader("sign", sign);
        httpPost.addHeader(HTTP.CONTENT_TYPE, "application/json");
        StringEntity se = new StringEntity(body.toString(), "UTF-8");
        se.setContentType("text/json");
        se.setContentEncoding(new BasicHeader(HTTP.CONTENT_TYPE, "application/json"));
        httpPost.setEntity(se);
        // 发送http post请求，并得到响应结果
        HttpResponse response = httpClient.execute(httpPost);
        String result = "";
        if (response != null) {
            HttpEntity resEntity = response.getEntity();
            if (resEntity != null) {
                result = EntityUtils.toString(resEntity, "UTF-8");
                System.out.println(result);
            }
        }
    }


    /**
     * 签名
     *
     * @param paramsMap 表单参数
     * @return 签名值
     * @throws Exception
     */
    private String sign(String paramsMap) throws Exception {

        // 读取CA证书与PEM格式证书需要根据实际证书使用情况而定,目前这两种都支持
        PrivateKey privateKey = loadPrivateKeyOfCA();
        // PrivateKey privateKey = loadPrivateKeyOfPem();

        Map<String, Object> claims =
                JwtParamBuilder.build().setSubject("tester").setIssuer("einvoice").setAudience("einvoice")
                        .addJwtId().addIssuedAt().setExpirySeconds(300).setNotBeforeSeconds(300).getClaims();
        // 此签名数据必须存在，否则在验证签名时会不通过。
        claims.put("requestdatas", getMD5(paramsMap));
        // 使用jdk1.6版本时，删除下面代码的中.compressWith(CompressionCodecs.DEFLATE)
        String compactJws = Jwts.builder().signWith(SignatureAlgorithm.RS512, privateKey)
                .setClaims(claims).compressWith(CompressionCodecs.DEFLATE).compact();

        return compactJws;
    }


    /**
     * 计算MD5
     *
     * @param str
     * @return
     * @throws UnsupportedEncodingException
     * @throws NoSuchAlgorithmException
     */
    private String getMD5(String str) throws UnsupportedEncodingException, NoSuchAlgorithmException {
        byte[] buf = null;
        buf = str.getBytes("utf-8");
        MessageDigest md5 = null;
        md5 = MessageDigest.getInstance("MD5");
        md5.update(buf);
        byte[] tmp = md5.digest();
        StringBuilder sb = new StringBuilder();
        for (byte b : tmp) {
            sb.append(String.format("%02x", b & 0xff));
        }
        return sb.toString();
    }


    /**
     * 读取证书私钥
     *
     * @return
     * @throws UnrecoverableKeyException
     * @throws KeyStoreException
     * @throws NoSuchAlgorithmException
     * @throws CertificateException
     * @throws IOException
     */
    protected PrivateKey loadPrivateKeyOfCA() throws UnrecoverableKeyException, KeyStoreException,
            NoSuchAlgorithmException, CertificateException, IOException {
        FileInputStream in = new FileInputStream(KEYPATH);
        KeyStore ks = KeyStore.getInstance("pkcs12");
        ks.load(in, PASSWORD.toCharArray());
        String alias = ks.aliases().nextElement();
        PrivateKey caprk = (PrivateKey) ks.getKey(alias, PASSWORD.toCharArray());
        return caprk;
    }


    /**
     * 构造请求的json数据
     *
     * @return
     */
    private String buildRequestDatas() {
       
        return "这应该是一个json格式字符串";
    }

```
#####**API相关工具类**
```java
package com.yonyou.einvoice.test;

import java.util.HashMap;
import java.util.Map;
import java.util.UUID;


/**
 * @author wangweir
 *
 */
public class JwtParamBuilder {

  /** JWT {@code Issuer} claims parameter name: <code>"iss"</code> */
  public static final String ISSUER = "iss";

  /** JWT {@code Subject} claims parameter name: <code>"sub"</code> */
  public static final String SUBJECT = "sub";

  /** JWT {@code Audience} claims parameter name: <code>"aud"</code> */
  public static final String AUDIENCE = "aud";

  /** JWT {@code Expiration} claims parameter name: <code>"exp"</code> */
  public static final String EXPIRATION = "exp";

  /** JWT {@code Not Before} claims parameter name: <code>"nbf"</code> */
  public static final String NOT_BEFORE = "nbf";

  /** JWT {@code Issued At} claims parameter name: <code>"iat"</code> */
  public static final String ISSUED_AT = "iat";

  /** JWT {@code JWT ID} claims parameter name: <code>"jti"</code> */
  public static final String ID = "jti";

  private Map<String, Object> claims;

  private final long now;

  private JwtParamBuilder() {
    claims = new HashMap<>();
    now = System.currentTimeMillis() / 1000l;
  }

  public static JwtParamBuilder build() {
    return new JwtParamBuilder();
  }

  public JwtParamBuilder addIssuedAt() {
    claims.put(ISSUED_AT, now);
    return this;
  }

  public JwtParamBuilder setExpirySeconds(final Integer expirySeconds) {
    claims.put(EXPIRATION, now + expirySeconds);
    return this;
  }

  public JwtParamBuilder setNotBeforeSeconds(final Integer beforeSeconds) {
    claims.put(NOT_BEFORE, now - beforeSeconds);
    return this;
  }

  public JwtParamBuilder setSubject(String sub) {
    addOneClaim(SUBJECT, sub);
    return this;
  }

  public JwtParamBuilder setIssuer(String iss) {
    addOneClaim(ISSUER, iss);
    return this;
  }

  public JwtParamBuilder setAudience(String aud) {
    addOneClaim(AUDIENCE, aud);
    return this;
  }

  public JwtParamBuilder addJwtId() {
    return setJwtId(UUID.randomUUID().toString());
  }

  public JwtParamBuilder setJwtId(String jwtid) {
    addOneClaim(ID, UUID.randomUUID().toString());
    return this;
  }

  public JwtParamBuilder claim(String name, Object value) {
    if (value == null) {
      this.claims.remove(name);
    } else {
      this.claims.put(name, value);
    }
    return this;
  }

  private void addOneClaim(String key, String value) {
    if (value != null && value.length() > 0) {
      claims.put(key, value);
    }
  }


  /**
   * @return the claims
   */
  public Map<String, Object> getClaims() {
    return claims;
  }


}

```
