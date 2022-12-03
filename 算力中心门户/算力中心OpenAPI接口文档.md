# 算力中心OpenAPI


**简介**:算力中心OpenAPI


**HOST**:http://localhost:18080


**联系人**:


**Version**:1.0.0.1


**接口路径**:/v3/api-docs


[TOC]






# 0-通用接口


## 开放联盟链框架查询


**接口地址**:`/ddcoai/sys/v1/opb/frame/framework/searches`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded`


**响应数据类型**:`*/*`


**接口描述**:<p>可以在运营系统的&#39;网络接入-网关管理-接入方式管理&#39;选择对外开放的框架 </p>



**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«List«OutOpbChainRecordSearches»»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||array|OutOpbChainRecordSearches|
|&emsp;&emsp;opbAlgorithmName|开放联盟链链算法名称|string||
|&emsp;&emsp;opbAlgorithmType|开放联盟链链算法类型|integer(int32)||
|&emsp;&emsp;opbChainId|开放联盟链链ID|integer(int64)||
|&emsp;&emsp;opbChainName|开放联盟链链名称|string||
|&emsp;&emsp;opbChainType|开放联盟链链类型|string||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": [
		{
			"opbAlgorithmName": "",
			"opbAlgorithmType": 0,
			"opbChainId": 0,
			"opbChainName": "",
			"opbChainType": ""
		}
	],
	"errorLogCode": "0",
	"message": "0"
}
```


# 1-官方DDC


## DDC生成


**接口地址**:`/ddcoai/sys/v1/ddc/save`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded,application/json`


**响应数据类型**:`*/*`


**接口描述**:<p>生成指定开放联盟链框架的ddc，‘门户配置管理-门户功能配置’勾选了官方ddc之后才能使用</p>



**请求示例**:


```javascript
{
  "ddcDesc": "描述",
  "ddcOwner": "0x0000000000000000000",
  "ddcPubTotal": "100",
  "ddcType": 721,
  "imgFileBase64": "png,iVBORw0KGgoAAAAN...(其中png为文件格式)",
  "imgFileName": "file1",
  "opbChainId": 1,
  "securityData": "附加数据",
  "userTradeCode": "用户第三方流水号"
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||
|inDdcSave|InDdcSave|body|true|InDdcSave|InDdcSave|
|&emsp;&emsp;ddcDesc|描述||false|string||
|&emsp;&emsp;ddcOwner|链账户地址||true|string||
|&emsp;&emsp;ddcPubTotal|发行数量：1155必填||false|string||
|&emsp;&emsp;ddcType|DDC类型(721,1155)||true|integer(int32)||
|&emsp;&emsp;imgFileBase64|文件base64编码，支持的格式(png,jpg,jpeg,bmp,gif,doc,docx,pdf)，大小限制2m||true|string||
|&emsp;&emsp;imgFileName|图片文件名称(不包含拓展名)||true|string||
|&emsp;&emsp;opbChainId|链标识(调用“开放联盟链框架查询”接口查询)||true|integer(int64)||
|&emsp;&emsp;securityData|附加数据||true|string||
|&emsp;&emsp;userTradeCode|用户第三方流水号||true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutDdcTrade»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutDdcTrade|OutDdcTrade|
|&emsp;&emsp;tradeCode|算力交易流水号|string||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"tradeCode": "DDC00000000001"
	},
	"errorLogCode": "0",
	"message": "0"
}
```


## DDC发送


**接口地址**:`/ddcoai/sys/v1/ddc/send`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded,application/json`


**响应数据类型**:`*/*`


**接口描述**:<p>发送指定开放联盟链框架的ddc到同一个算力中心方的链账户地址，‘门户配置管理-门户功能配置’勾选了官方ddc之后才能使用</p>



**请求示例**:


```javascript
{
  "ddcId": "100",
  "ddcOwner": "0x00000000000",
  "ddcType": 721,
  "opbChainId": 9,
  "recipientAccount": "0x0000000000",
  "securityData": "附加数据",
  "sendNumber": "10",
  "userTradeCode": "用户第三方流水号"
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||
|inDdcSend|InDdcSend|body|true|InDdcSend|InDdcSend|
|&emsp;&emsp;ddcId|DDC ID||true|string||
|&emsp;&emsp;ddcOwner|拥有者链账户地址||true|string||
|&emsp;&emsp;ddcType|DDC类型(721,1155)||true|integer(int32)||
|&emsp;&emsp;opbChainId|链标识(调用“开放联盟链框架查询”接口查询)||true|integer(int64)||
|&emsp;&emsp;recipientAccount|接收者账户地址||true|string||
|&emsp;&emsp;securityData|附加数据||true|string||
|&emsp;&emsp;sendNumber|发送数量||true|string||
|&emsp;&emsp;userTradeCode|用户第三方流水号||true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutDdcTrade»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutDdcTrade|OutDdcTrade|
|&emsp;&emsp;tradeCode|算力交易流水号|string||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"tradeCode": "DDC00000000001"
	},
	"errorLogCode": "0",
	"message": "0"
}
```


## DDC销毁


**接口地址**:`/ddcoai/sys/v1/ddc/burn`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded,application/json`


**响应数据类型**:`*/*`


**接口描述**:<p>销毁指定开放联盟链框架的ddc且必须为同一个算力中心方，‘门户配置管理-门户功能配置’勾选了官方ddc之后才能使用</p>



**请求示例**:


```javascript
{
  "ddcId": "100",
  "ddcOwner": "0x00000000000",
  "ddcType": 721,
  "opbChainId": 9,
  "securityData": "附加数据",
  "userTradeCode": "用户第三方流水号"
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||
|inDdcBurn|InDdcBurn|body|true|InDdcBurn|InDdcBurn|
|&emsp;&emsp;ddcId|DDC ID||true|string||
|&emsp;&emsp;ddcOwner|拥有者链账户地址||true|string||
|&emsp;&emsp;ddcType|DDC类型(721,1155)||true|integer(int32)||
|&emsp;&emsp;opbChainId|链标识(调用“开放联盟链框架查询”接口查询)||true|integer(int64)||
|&emsp;&emsp;securityData|附加数据||true|string||
|&emsp;&emsp;userTradeCode|用户第三方流水号||true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutDdcTrade»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutDdcTrade|OutDdcTrade|
|&emsp;&emsp;tradeCode|算力交易流水号|string||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"tradeCode": "DDC00000000001"
	},
	"errorLogCode": "0",
	"message": "0"
}
```


## DDC交易定价查询


**接口地址**:`/ddcoai/sys/v1/ddc/fee/searches`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded`


**响应数据类型**:`*/*`


**接口描述**:<p>查询DDC交易与算力值定值列表，算力值支持小数点后两位</p>



**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«List«OutDdcFeeSearches»»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||array|OutDdcFeeSearches|
|&emsp;&emsp;txAmount|DDC交易价格|number(bigdecimal)||
|&emsp;&emsp;txType|DDC交易类型：20=生成 22=流转 23=销毁|integer(int32)||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": [
		{
			"txAmount": 6,
			"txType": 1
		}
	],
	"errorLogCode": "0",
	"message": "0"
}
```


## DDC交易明细查询


**接口地址**:`/ddcoai/sys/v1/ddc/transfer/searches`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded,application/json`


**响应数据类型**:`*/*`


**接口描述**:<p>查询DDC交易明细列表，包含官方DDC交易的状态结果</p>



**请求示例**:


```javascript
{
  "tradeCode": "",
  "txType": 0,
  "userTradeCode": ""
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||
|inDdcTransferSearches|InDdcTransferSearches|body|true|InDdcTransferSearches|InDdcTransferSearches|
|&emsp;&emsp;tradeCode|算力交易流水号||false|string||
|&emsp;&emsp;txType|交易类型   20=DDC生成  22=DDC流转   23=DDC销毁||false|integer(int32)||
|&emsp;&emsp;userTradeCode|用户第三方流水号||false|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«List«OutDdcTransferSearches»»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||array|OutDdcTransferSearches|
|&emsp;&emsp;burnQuantity|销毁数量|integer(int64)||
|&emsp;&emsp;ddcId|DdcId|string||
|&emsp;&emsp;ddcOwner|接收者账户地址|string||
|&emsp;&emsp;ddcType|DDC类型|integer(int32)||
|&emsp;&emsp;mintQuantity|生成数量|integer(int64)||
|&emsp;&emsp;opbChainId|开放联盟链链ID|integer(int64)||
|&emsp;&emsp;opbChainName|开放联盟链链名称|string||
|&emsp;&emsp;sendAccount|发送者账户地址|string||
|&emsp;&emsp;tradeCode|帐户交易编号|string||
|&emsp;&emsp;tradeQuantity|流转数量|integer(int64)||
|&emsp;&emsp;txHash|交易哈希|string||
|&emsp;&emsp;txStatus|交易状态：0=处理中 1=成功 2=失败|integer(int32)||
|&emsp;&emsp;txType|交易类型   20=DDC生成  22=DDC流转   23=DDC销毁|integer(int32)||
|&emsp;&emsp;userTradeCode|用户第三方流水号|string||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": [
		{
			"burnQuantity": 0,
			"ddcId": "",
			"ddcOwner": "",
			"ddcType": 0,
			"mintQuantity": 0,
			"opbChainId": 0,
			"opbChainName": "",
			"sendAccount": "",
			"tradeCode": "",
			"tradeQuantity": 0,
			"txHash": "",
			"txStatus": 0,
			"txType": 0,
			"userTradeCode": ""
		}
	],
	"errorLogCode": "0",
	"message": "0"
}
```


# 2-链账户管理


## 创建链账户


**接口地址**:`/ddcoai/sys/v1/chainaccount/save`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded,application/json`


**响应数据类型**:`*/*`


**接口描述**:<p>创建算力中心支持的开放联盟链框架的链账户</p>



**请求示例**:


```javascript
{
  "opbChainClientName": "test1",
  "opbChainId": 9
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||
|inOpbChainAccountSave|InOpbChainAccountSave|body|true|InOpbChainAccountSave|InOpbChainAccountSave|
|&emsp;&emsp;opbChainClientName|链账户名称||true|string||
|&emsp;&emsp;opbChainId|链框架id||true|integer(int64)||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutChainAccountSave»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutChainAccountSave|OutChainAccountSave|
|&emsp;&emsp;opbChainClientAddress|链账户地址|string||
|&emsp;&emsp;privateKey|链账户私钥|string||
|&emsp;&emsp;publicKey|链账户公钥|string||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"opbChainClientAddress": "0xaaaaaaaaaaaaaaaaaa",
		"privateKey": "**************",
		"publicKey": "**************"
	},
	"errorLogCode": "0",
	"message": "0"
}
```


## 链账户列表


**接口地址**:`/ddcoai/sys/v1/chainaccount/searches`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded,application/json`


**响应数据类型**:`*/*`


**接口描述**:<p>算力中心门户用户查询自己的链账户数据</p>



**请求示例**:


```javascript
{
  "data": {
    "opbChainClientAddress": "0xXXX",
    "opbChainClientName": "test1",
    "opbChainId": 9
  },
  "page": {
    "pageNum": 1,
    "pageSize": 5
  }
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||
|requestPageInfo«InOpbChainAccountSearches»|RequestPageInfo«InOpbChainAccountSearches»|body|true|RequestPageInfo«InOpbChainAccountSearches»|RequestPageInfo«InOpbChainAccountSearches»|
|&emsp;&emsp;data|请求报文体，不能为null，可以为空对象||true|InOpbChainAccountSearches|InOpbChainAccountSearches|
|&emsp;&emsp;&emsp;&emsp;opbChainClientAddress|链账户地址||false|string||
|&emsp;&emsp;&emsp;&emsp;opbChainClientName|链账户名称||false|string||
|&emsp;&emsp;&emsp;&emsp;opbChainId|链框架id，可以从‘开放联盟链框架查询’接口查到具体信息||false|integer||
|&emsp;&emsp;page|分页入参||true|InPage|InPage|
|&emsp;&emsp;&emsp;&emsp;pageNum|分页：从1开始||false|integer||
|&emsp;&emsp;&emsp;&emsp;pageSize|每页大小。||false|integer||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfoPage«List«OutOpbChainAccountSearches»»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||array|OutOpbChainAccountSearches|
|&emsp;&emsp;energyValueBalance|能量值余额（eos：NET:111111bytes,CPU:111111us,RAM:11111bytes）|string||
|&emsp;&emsp;gasLastUpdateTime|能量值/资源更新时间|string(date-time)||
|&emsp;&emsp;opbChainAccountStatus|链账户状态（已启用/已冻结）|integer(int32)||
|&emsp;&emsp;opbChainClientAddress|链账户地址|string||
|&emsp;&emsp;opbChainClientCode|链账户code|string||
|&emsp;&emsp;opbChainClientName|链账户名称|string||
|&emsp;&emsp;opbChainName|链名称|string||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||
|resultPageInfo||PageInfo|PageInfo|
|&emsp;&emsp;firstPage||boolean||
|&emsp;&emsp;lastPage||boolean||
|&emsp;&emsp;pageNum||integer(int32)||
|&emsp;&emsp;pageSize||integer(int32)||
|&emsp;&emsp;pages||integer(int32)||
|&emsp;&emsp;total||integer(int64)||


**响应示例**:
```javascript
{
	"code": 0,
	"data": [
		{
			"energyValueBalance": "20000000",
			"gasLastUpdateTime": "",
			"opbChainAccountStatus": 2,
			"opbChainClientAddress": "0xaaaaaaaaaaaaaaaaaa",
			"opbChainClientCode": "wertyuiopoiuytr",
			"opbChainClientName": "test1",
			"opbChainName": "0xaaaaaaaaaaaaaaaaaa"
		}
	],
	"errorLogCode": "0",
	"message": "0",
	"resultPageInfo": {
		"firstPage": true,
		"lastPage": true,
		"pageNum": 0,
		"pageSize": 0,
		"pages": 0,
		"total": 0
	}
}
```


## 能量值定价查询


**接口地址**:`/ddcoai/sys/v1/chainaccount/hashrate/gas/search`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded,application/json`


**响应数据类型**:`*/*`


**接口描述**:<p>1算力值可兑换的能量值，具体设置可以到运营系统菜单‘链账户管理-能量值价格管理’里修改</p>



**请求示例**:


```javascript
{
  "opbChainId": 2
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||
|inHashRateGasRatioSearch|InHashRateGasRatioSearch|body|true|InHashRateGasRatioSearch|InHashRateGasRatioSearch|
|&emsp;&emsp;opbChainId|开放联盟链id||true|integer(int64)||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutHashRateGasRatioSearch»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutHashRateGasRatioSearch|OutHashRateGasRatioSearch|
|&emsp;&emsp;gasQuantity|1算力值对应的能量值|number(bigdecimal)||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"gasQuantity": 1000000
	},
	"errorLogCode": "0",
	"message": "0"
}
```


## eos资源定价查询


**接口地址**:`/ddcoai/sys/v1/chainaccount/hashrate/resource/search`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded`


**响应数据类型**:`*/*`


**接口描述**:<p>eos资源定价查询，具体设置可以到运营系统菜单‘链账户管理-能量值价格管理’里修改</p>



**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutHashRateResourceRatioDtoSearch»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutHashRateResourceRatioDtoSearch|OutHashRateResourceRatioDtoSearch|
|&emsp;&emsp;eosCpu|cpu单价 (算力/SYS/天)|number(double)||
|&emsp;&emsp;eosNet|net单价 (算力/SYS/天)|number(double)||
|&emsp;&emsp;eosRam|ram单价 (算力/KB)|number(double)||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"eosCpu": 0.02,
		"eosNet": 0.01,
		"eosRam": 0.04
	},
	"errorLogCode": "0",
	"message": "0"
}
```


## 能量值充值


**接口地址**:`/ddcoai/sys/v1/chainaccount/gas/recharge`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded,application/json`


**响应数据类型**:`*/*`


**接口描述**:<p>算力中心门户用户可以给自己链账户地址充值能量值</p>



**请求示例**:


```javascript
{
  "hashRateValue": 200,
  "opbChainClientAddress": "0x2b46090ba0c945b69b754a3670e5c79c25abfe9e",
  "opbChainId": 2
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||
|inGasRecharge|InGasRecharge|body|true|InGasRecharge|InGasRecharge|
|&emsp;&emsp;hashRateValue|算力值：具体算力值对应的能量值请通过接口‘能量值定价查询’接口查询||true|number(bigdecimal)||
|&emsp;&emsp;opbChainClientAddress|链账户地址||true|string||
|&emsp;&emsp;opbChainId|开放联盟链id，可以从‘开放联盟链框架查询’接口查到具体信息||true|integer(int64)||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutEnergyRecharge»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutEnergyRecharge|OutEnergyRecharge|
|&emsp;&emsp;energyValue|充值成功的能量值|number(bigdecimal)||
|&emsp;&emsp;opbChainClientAddress|链账户地址|string||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"energyValue": 20000000,
		"opbChainClientAddress": "0xaaaaaaaaaaaaaaaaaa"
	},
	"errorLogCode": "0",
	"message": "0"
}
```


## 中移链资源充值


**接口地址**:`/ddcoai/sys/v1/chainaccount/resource/recharge`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded,application/json`


**响应数据类型**:`*/*`


**接口描述**:<p>中移链资源充值</p>



**请求示例**:


```javascript
{
  "cpuPlusValue": 100,
  "netPlusValue": 100,
  "opbChainClientAddress": "reddatas1234",
  "ramPlusValue": 100,
  "resourceValidDate": "2022-12-31"
}
```


**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||
|inEosResourceRecharge|InEosResourceRecharge|body|true|InEosResourceRecharge|InEosResourceRecharge|
|&emsp;&emsp;cpuPlusValue|充值cpu容量（不能为小数）||true|number(biginteger)||
|&emsp;&emsp;netPlusValue|充值net容量（不能为小数）||true|number(biginteger)||
|&emsp;&emsp;opbChainClientAddress|链账户地址||true|string||
|&emsp;&emsp;ramPlusValue|充值ram容量（不能为小数）||true|number(biginteger)||
|&emsp;&emsp;resourceValidDate|资源有效期||true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutEosResourceRecharge»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutEosResourceRecharge|OutEosResourceRecharge|
|&emsp;&emsp;cpuPlusValue|充值cpu量|number(biginteger)||
|&emsp;&emsp;netPlusValue|充值net量|number(biginteger)||
|&emsp;&emsp;opbChainClientAddress|链账户地址|string||
|&emsp;&emsp;ramPlusValue|充值ram量|number(biginteger)||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"cpuPlusValue": 100,
		"netPlusValue": 100,
		"opbChainClientAddress": "0xaaaaaaaaaaaaaaaaaa",
		"ramPlusValue": 100
	},
	"errorLogCode": "0",
	"message": "0"
}
```


# 3-网络接入


## 接入key查询


**接口地址**:`/ddcoai/sys/v1/appaccess/access/key/search`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded`


**响应数据类型**:`*/*`


**接口描述**:<p>通过此接口可以查询用户接入节点网关需要使用的key</p>



**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutAccessKeySearch»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutAccessKeySearch|OutAccessKeySearch|
|&emsp;&emsp;accessKey|接入key|string||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"accessKey": "a96234234234ea343b233c343423c1960040343242332223326"
	},
	"errorLogCode": "0",
	"message": "0"
}
```


## 接入key更新


**接口地址**:`/ddcoai/sys/v1/appaccess/access/key/modify`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded`


**响应数据类型**:`*/*`


**接口描述**:<p>通过此接口可以更新用户接入节点网关需要使用的key</p>



**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutAccessKeyModify»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutAccessKeyModify|OutAccessKeyModify|
|&emsp;&emsp;accessKey|更新后的接入Key|string||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"accessKey": "更新后的接入Key"
	},
	"errorLogCode": "0",
	"message": "0"
}
```


# 4-用户中心


## 我的算力余额查询


**接口地址**:`/ddcoai/sys/v1/user/account/info/search`


**请求方式**:`POST`


**请求数据类型**:`application/x-www-form-urlencoded`


**响应数据类型**:`*/*`


**接口描述**:<p>查询算力中心门户用户的算力值余额，如要充值可以到门户了解充值方式</p>



**请求参数**:


| 参数名称 | 参数说明 | 请求类型    | 是否必须 | 数据类型 | schema |
| -------- | -------- | ----- | -------- | -------- | ------ |
|apitoken|apitoken|header|true|string||


**响应状态**:


| 状态码 | 说明 | schema |
| -------- | -------- | ----- | 
|200|OK|ResultInfo«OutUserAccountInfoSearch»|
|201|Created||
|401|Unauthorized||
|403|Forbidden||
|404|Not Found||


**响应参数**:


| 参数名称 | 参数说明 | 类型 | schema |
| -------- | -------- | ----- |----- | 
|code|成功：0，失败：-1|integer(int32)|integer(int32)|
|data||OutUserAccountInfoSearch|OutUserAccountInfoSearch|
|&emsp;&emsp;accountBalance|账户余额：算力值|number(bigdecimal)||
|errorLogCode|此标记同时写入到日志文件中，方便查找|string||
|message|都是消息编码，前端自行国际化处理|string||


**响应示例**:
```javascript
{
	"code": 0,
	"data": {
		"accountBalance": 10
	},
	"errorLogCode": "0",
	"message": "0"
}
```


# 附录


## 0-OpenAPI 说明


### 0. 响应异常消息编码
# 0. 响应异常消息编码

| 编码                   | 说明                                |
|----------------------|-----------------------------------|
| MSG_20010005         | apitoken 授权认证失败                   |
| MSG_10051001         | 当前交易开放联盟链框架在算力中心不支持               |
| MSG_10051002         | 中移资源参数不能为空                        |
| MSG_10051007         | 链账户不存在                            |
| MSG_10051008         | 链账户已锁定                            |
| MSG_10051009         | 链账户不是启用状态                         |
| MSG_10051010         | 创建的链账户地址在官方ddc中尚未开通ddc，无法做官方ddc交易 |
| MSG_10051011         | 查询链账户余额为空                         |
| MSG_10051012         | 链账户余额不足                           |
| MSG_10051013         | 充值中移链资源扣款异常                       |
| MSG_10051014         | 充值能量值扣款异常                         |
| MSG_10051015         | 调用openapi充值能量值失败                  |
| MSG_10051018         | 创建链账户服务内部出错                       |
| MSG_10051019         | 能量值数值错误                           |
| MSG_10051020         | 算力值数值错误                           |
| MSG_10051022         | 该条链未配置算力值能量值比例                    |
| MSG_10051023         | 未匹配到当前时间的算力值/gas比例生效记录            |
| MSG_10051024         | 该条链未配置算力值资源比例                     |
| MSG_10051025         | 未匹配到当前时间的算力值/资源比例生效记录             |
| MSG_10051026         | 查询算力值/能量值比例异常                     |
| MSG_10051027         | 查询算力值/资源比例异常                      |
| MSG_10051028         | 资源有效期必须大于1天                       |
| MSG_10051029         | 调用openapi分配资源失败                   |
| MSG_10051030         | 链类型错误链类型错误                        |
| MSG_10051031         | 中移链链账户不符合规则                       |
| MSG_10051032         | 算力值必须大于0                          |
| MSG_10051033         | 资源充值容量必须大于0                       |
| MSG_10051035         | 链账户名称已存在                          |
| MSG_10051036         | gas充值退款异常                         |
| MSG_10051037         | 资源充值退款异常                          |
| MSG_10051038         | 能量值充值失败                           |
| MSG_10051039         | 资源充值失败                            |
| MSG_10051041         | 日期格式错误                            |
| MSG_10053001         | DDC生成失败                           |
| MSG_10053002         | DDC发送失败                           |
| MSG_10053003         | DDC销毁失败                           |
| MSG_10028041         | 接入key同步到节点网关失败                    |
| MSG_10028042         | 更新key同步到节点网关失败                    |
| MSG_200BALANCE_SHORT | 算力值余额不足                           | 
| MSG_10021051         | 算力交易流水号不正确                        |
| MSG_10028061         | 文件业务类型不存在                         |
| MSG_10028062         | 文件格式不能为空                          |
| MSG_10028063         | 文件内容不能为空                          |
| MSG_10028064         | 文件超过规定大小                          |
| MSG_10028065         | 文件格式有误                            |
| MSG_40100000         | 无接口访问权限                           |
| MSG_10053010         | DDC当前状态不可发送                       |
| MSG_10053011         | DDC当前状态不可销毁                       |
| MSG_10053012         | 第三方流水号重复                       |
### 1. API Changelog 
# 1. API Changelog 

---
##  V1.0.0.1 Release in progress
算力中心全新版本


