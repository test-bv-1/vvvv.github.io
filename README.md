
心跳规则：2s一次<br />{"event":"ping"}<br />{"event":"pong"}


| 公用code码 （type字段为订阅的业务类型） |  |
| --- | --- |
| 成功订阅 | {"code":1,"desc":"success","type":"MARKET"}   |
| 重复订阅 | {"code":10001,"desc":"重复订阅","type":"MARKET"} |
| 参数异常 | {"code":10000,"desc":"参数异常","type":"MARKET"} |



U合约：USDT<br />币本位：SWAPS<br />币币：SPOT


<a name="NEdfS"></a>
# 一、公开订阅事件
测试环境ws地址:  ws://172.30.96.33:9080/ws<br />生产环境地址：wss://push.bitvito.com/ws

<a name="dRn1d"></a>
## 指数
| 指数推送示例 |  |
| --- | --- |
| 请求订阅 | {"event":"SUB","type":"INDEX_PRICE","businessType":"USDT","product":1001} |
| 订阅回执 | {"code":1,"desc":"success","type":"INDEX_PRICE","first":true} |
| 取消订阅 | {"event":"UNSUB","type":"INDEX_PRICE","product":1001} |
| 首次返回 | {"pid":1001,"type":"INDEX_PRICE","data":"47"} |
| 增量返回 | {"pid":1001,"type":"INDEX_PRICE","data":"47"} |






<a name="pFlU4"></a>
## 深度
| 深度 |  |  |
| --- | --- | --- |
| 请求 | {"event":"SUB","type":"DEPTH","product":1001,"params":{"step":"0"}} | step:档位（0-N）注：step只针对现货，具体档位值找龙哥 |
| 取消订阅 | {"event":"UNSUB","type":"DEPTH","product":1001} | 取消订阅 |
| 订阅回执 | {"code":1,"desc":"success","type":"DEPTH"} |  |
| 首次返回 | {"id":"1","pid":1001,"type":"DEPTH","data":{"asks":[["7051","47231"],["33220.51","714000"],["33222.17","501228"],["33232.14","414120"],["33242.11","499800"],["33252.08","571200"],["33262.06","642600"],["33272.04","856800"],["33360","1"],["33438.4","795820"],["33605.59","672826"],["33773.62","723734"],["33942.49","585188"],["34000","32"],["34112.2","88023"],["34200","33"],["34300","1"],["34400","2"],["34778","30"],["34888","50"],["34908.08","2000000"],["35905.46","3000000"],["36500","1"],["37000","352"],["37500","1"],["38350","1"],["38500","1"],["39305","15"],["39500","1"],["40000","1"]],"bids":[["27888","2"],["28000","52"],["28200","51"],["28458","100"],["28500","12"],["28523.7","1"],["28700","1"],["29001","1"],["30000","3"],["30586.13","3000000"],["31500","5"],["31583.51","2000000"],["31888","2"],["32000","3"],["32100","138"],["32131","30"],["32154.49","1"],["32491.12","596898"],["32518","30"],["32654.39","734546"],["32700","1"],["32818.48","700208"],["32983.4","821195"],["33149.15","823200"],["33159.1","617400"],["33169.05","548800"],["33179","480200"],["33188.96","397880"],["33198.92","481572"],["33200.58","686000"]]},"first":true} | asks 卖<br />bids 买<br /><br />["7051","47231"]<br /> 价格     数量<br /> |
| 增量返回 | {"id":"9","pid":1001,"type":"DEPTH","data":{"asks":[["13546","47231"],["30032","0"]],"bids":null}} |  |



<a name="xOWpQ"></a>
## 左侧行情列表
| 左侧行情列表（币对价格、涨跌幅） |  |  |
| --- | --- | --- |
| 请求订阅 | <br /><br />{"event": "SUB","more":"1","type": "ALL_TICKER","params": {"ids": "1001,1002,1003,1004,1005,1006,1007,1008,1009,1010,1011,1012,1013,1014,1015,1016,1017,1018,1020,1021,1022,1023,1024,1025,1026,1027,1028,1029,1030,1031,1032,1033,1034,1035,1036,1037,1038,1040,1041,1042,1043,1044,1045"}} | ids:币对id<br />如需要详细数据传参more  |
| 取消订阅 | {"event":"UNSUB","type":"ALL_TICKER"} | 取消数据具体到订阅类型，不支持币对细颗粒度取消 |
| 订阅回执 | {"code":1,"desc":"success","type":"ALL_TICKER"} |  |
| 首次返回 | {"type":"ALL_TICKER","data":[{"last":"34379.94","productId":"1001","change":"-3.18"}],"businessType":"USDT","first":true} | last:价格<br />productId:币对id<br />change：涨跌幅 |
| 增量返回 | {"type":"ALL_TICKER","data":[{"last":"34374.94","productId":"1001","change":"-3.11"}],"businessType":"USDT"} | 增量只推送币对行情有变化的数据 |


<a name="wLsG2"></a>
## 行情组合（k线、行情、实时成交）
| 行情组合（k线、行情、实时成交） |  |  |
| --- | --- | --- |
| 请求订阅 | <br /><br />{"event":"SUB","type":"MARKET","product":1001,"params":{"period":"1day","since":"1617438148000", "end":"1625214208000","need":"kline,ticker,realTime"},"businessType":"USDT"} | period:k线类型<br />"1min":0<br />"5min": 2	<br />"15min":3	<br />"30min":4<br />"1hour":5<br />"4hour":7<br />"1day":10<br />"1week":11	<br />"1month":12<br />"1year":13<br />since，end ：<br />开始结束时间戳 （精确到分钟）<br /><br />need ：组合 |
| 取消订阅 | {"event":"UNSUB","type":"MARKET","product":1001} | 取消数据具体到订阅类型，不支持币对细颗粒度取消 |
| 订阅回执 | {"code":1,"desc":"success","type":"MARKET"} |  |
| 首次返回 | {	"product": "1001",<br />	"type": "MARKET",<br />	"data": {<br />		"realTime": [{<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565426<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565426<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565312<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565312<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565089<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565089<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564993<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564993<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564789<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564789<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564685<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564685<br />		}],<br />		"kline": [{<br />			"open": "340000",<br />			"high": "340000",<br />			"low": "33000",<br />			"close": "340000",<br />			"volume": 20620077,<br />			"amount": "14019315240",<br />			"productId": 1001,<br />			"type": 10,<br />			"time": 1626019200000<br />		}],<br />		"ticker": {<br />			"open": "340000",<br />			"high": "340000",<br />			"low": "33000",<br />			"last": "340000",<br />			"volume": "20620077",<br />			"amount": "14019315240",<br />			"productId": "1001",<br />			"change": "0",<br />			"YearChange": "0",<br />			"time": "1626087771813"<br />		}<br />	}<br />} | realTime(实时成交):<br />size 数量<br />price 价格<br />side 方向 1:买 2：卖<br />kline:<br />open 开盘价<br />high 高<br />low 低<br />close 收<br />volume 成交数<br />amount 成交额<br />type kline时间类型<br />ticker：<br />change 涨跌幅<br />last  最新价<br />YearChange 年涨幅<br />*其他同上 |
| 增量返回 | {	"product": "1001",<br />	"type": "MARKET",<br />	"data": {<br />		"realTime": [{<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565426<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565426<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565312<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565312<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565089<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565089<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564993<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564993<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564789<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564789<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564685<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564685<br />		}],<br />		"kline": [{<br />			"open": "340000",<br />			"high": "340000",<br />			"low": "33000",<br />			"close": "340000",<br />			"volume": 20628967,<br />			"amount": "14025360440",<br />			"productId": 1001,<br />			"type": 10,<br />			"time": 1626019200000<br />		}],<br />		"ticker": {<br />			"open": "340000",<br />			"high": "340000",<br />			"low": "33000",<br />			"last": "340000",<br />			"volume": "20628967",<br />			"amount": "14025360440",<br />			"productId": "1001",<br />			"change": "0",<br />			"YearChange": "0",<br />			"time": "1626087775669"<br />		}<br />	}<br />} |  |

<a name="ZZRcx"></a>
## 
<a name="s5kRD"></a>
## 单次调用业务post接口
| 单次获取行情组合数据（所有post） |  |  |
| --- | --- | --- |
| 请求订阅 | <br /><br />{<br />	"event": "REQ",<br />	"params": {<br />		"url": "/v1/order/place",<br />		"apiType": "test"<br />	},<br />	"postParams": {<br />		"body": {<br />			"currencyPairId": 1001044,<br />			"orderType": 2,<br />			"positionSide": 1,<br />			"price": 0,<br />			"quantity": 1,<br />			"side": 1,<br />			"fsafsda": {<br />				"fdafdsa": "reqwre"<br />			}<br />		},<br />		"head": {<br />			"businessType": "1",<br />			"requestFrom": "3",<br />			"ACCESS_TOKEN": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NDI0OTE1NDgsInVzZXJJZFNob3ciOiJIQXpDYkpVQmtLIiwidGVuYW5jeSI6NjA0ODAwLCJ0ZW5hbnRJZCI6MCwidXNlclR5cGUiOjEsInJhbmRvbSI6ImY1MjQxOTZlLWJjNzgtNDMwZC1iYWQ0LWIyMmQ1YzNlNTcxYiIsInRpbWVzdGFtcCI6MTY0MTg4Njc0ODI1OCwia2V5IjoiYml0dml0byIsInVpZCI6Ijk0Nzk3MjgzMjI0OTE1NyJ9.0Jk_ACjeP14FSJVby1hqmTsVHv0kqdlvFtRcnm4OR7c"<br />		}<br />	},<br />	"type": "POST"<br />} | <br /><br />url：接口后缀<br />例：/v1/order/place<br />apitype:客户端自定义 <br />head:http head转成json结构<br />body: http body 转成json结构 |
| 返回 | {"type":"POST","apiType":"test","data":"{\\"message\\":\\"Missing JWT token in request\\",\\"code\\":100024}"} |  |

<a name="aakFU"></a>
# 


<a name="f2awo"></a>
## 单次获取行情组合数据
| 单次获取行情组合数据 |  |  |
| --- | --- | --- |
| 请求订阅 | <br /><br />{"event":"REQ","type":"FULL_BAR_DATA","product":1031044,"businessType":"USDT","params":{"period":"1day","since":"1594547169000", "end":"196342369000"}} | period:k线类型<br />"1min":0<br />"5min": 2	<br />"15min":3	<br />"30min":4<br />"1hour":5<br />"4hour":7<br />"1day":10<br />"1week":11	<br />"1month":12<br />"1year":13<br />since，end ：<br />开始结束时间戳 （精确到分钟）<br /><br />need ：组合 |
| 返回 | {	"product": "1001",<br />	"type": "MARKET",<br />	"data": {<br />		"realTime": [{<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565426<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565426<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565312<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565312<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565193<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565089<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072565089<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564993<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564993<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564895<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564789<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564789<br />		}, {<br />			"size": 389,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564685<br />		}, {<br />			"size": 500,<br />			"price": "340000",<br />			"side": 1,<br />			"time": 1626072564685<br />		}],<br />		"kline": [{<br />			"open": "340000",<br />			"high": "340000",<br />			"low": "33000",<br />			"close": "340000",<br />			"volume": 20628967,<br />			"amount": "14025360440",<br />			"productId": 1001,<br />			"type": 10,<br />			"time": 1626019200000<br />		}],<br />		"ticker": {<br />			"open": "340000",<br />			"high": "340000",<br />			"low": "33000",<br />			"last": "340000",<br />			"volume": "20628967",<br />			"amount": "14025360440",<br />			"productId": "1001",<br />			"change": "0",<br />			"YearChange": "0",<br />			"time": "1626087775669"<br />		}<br />	}<br />} | realTime(实时成交):<br />size 数量<br />price 价格<br />side 方向 1:买 2：卖<br />kline:<br />open 开盘价<br />high 高<br />low 低<br />close 收<br />volume 成交数<br />amount 成交额<br />type kline时间类型<br />ticker：<br />change 涨跌幅<br />last  最新价<br />YearChange 年涨幅<br />*其他同上 |

<a name="zBMPx"></a>
# 
<a name="Ji7BF"></a>
# 二、个人中心
测试环境ws地址:  ws://172.30.96.33:9080/personal<br />生产环境地址：wss://push.bitvito.com/personal

| 仓位（前置条件登录） |  |  |
| --- | --- | --- |
| 请求 | {"event":"SUB","type":"ASSET","businessType":"USDT", "params":{"margin_mode":"1"} }' | margin_mode ：1：全仓<br />2：逐仓 |
| 取消订阅 | {"event":"UNSUB","type":"ASSET"} | 取消订阅 |
| 订阅回执 | {"code":1,"desc":"success","type":"ASSET"} |  |
| 首次返回 | <br /><br />全仓 marginMode:"1"<br /><br /><br />{	"type": "ASSET",<br />	"businessType": "USDT",<br />	"userId": 1,<br />	"marginMode": 1,<br />	"data": {<br />   "grade": 1,<br />   "addProfitRate": "0.01",<br />		"userAccountList": [{<br />			"currencyId": 1001,<br />			"quantity": "993.52",<br />			"holdQuantity": "4.24"<br />		}],<br />		"userPositionList": [{<br />			"marginMode": 1,<br />			"currencyPairId": 1001,<br />			"side": 1,<br />			"leverage": "100",<br />			"positionPrice": "1000",<br />			"quantity": "100",<br />			"availableQuantity": "100",<br />			"positionMargin": "2",<br />			"closeCommission": "0.06",<br />			"positionValue": "200"<br />		}]<br />	}<br />}<br /><br /><br /><br /><br />逐仓 marginMode:"2"<br /><br />{	"type": "ASSET",<br />	"businessType": "USDT",<br />	"userId": 1,<br />	"marginMode": 2,<br />	"data": {<br />   "grade": 1,<br />   "addProfitRate": "0.01",<br />		"userAccountList": [{<br />			"currencyId": 1001,<br />			"quantity": "993.52",<br />			"holdQuantity": "4.24"<br />		}],<br />		"userSubPositionMarginList": [{<br />			"currencyPairId": 1001,<br />			"positionMargin": "993.52"<br />		}]<br />	}<br />} | <br /><br />无法识别标识是否是首次数据<br />字段含义：<br />(王伟联调)<br />grade:VIP等级<br />sddProfitRate:盈利加成 |
| 增量返回 | {"type":"ASSET","businessType":"USDT","userId":1,"marginMode":1,"data":{<br /> "grade": 1,<br /> "addProfitRate": "0.01",<br />"userAccount":{"quantity":"983.28","holdQuantity":"4.24"},"userPositionList":[{"marginMode":1,"currencyPairId":1001,"side":1,"leverage":"100","positionPrice":"1000","quantity":"600","availableQuantity":"400","positionMargin":"12","closeCommission":"0.24","positionValue":"1200"}]}} |  |


| 止盈止损（前置条件登录） |  |  |
| --- | --- | --- |
| 请求 | {"event":"SUB","type":"ASSET","businessType":"USDT", "userId":"1","params":{"margin_mode":"1"} }' | margin_mode ：1：全仓<br />2：逐仓 |
| 取消订阅 | {"event":"UNSUB","type":"ASSET"} | 取消订阅 |
| 订阅回执 | {"code":1,"desc":"success","type":"ASSET"} |  |
| 首次返回 | <br /><br />全仓 marginMode:"1"<br /><br />{<br />	"data": {<br />		"list": [{<br />			"orderType": 1, //执行类型1:现价单,2:市价单<br />			"side": 1, //买卖方向,1:买,2:卖<br />			"planType": 1, //类型,1:止盈,2:止损,3:计划委托<br />			"quantity": 100, //下单数量<br />			"positionSide": 1, //持仓方向,1:多,2:空<br />			"currencyPairId": 1001, //交易币对id<br />			"marginMode": 1, //保证金模式,1:全仓,2:逐仓<br />			"userId": 1, //用户id<br />			"stopPrice": 11.3, //触发价格<br />			"price": 20.3, //执行价格<br />			"tenantId": 11, //租户id<br />			"id": 1000001, //数据id<br />			"userType": 2, //用户类型，1:做市用户，2:普通用户<br />			"businessType": 1, //业务类型，1:U合约，2:币本位<br />			"workingType": 1, //触发类型，1：成交价格，2:指数价格<br />			"status": 2 //状态,1:未生效,2:已生效,3:已触发,4:取消<br />		}]<br />	},<br />	"marginMode": 1,<br />	"type": "ASSET",<br />	"userId": 1,<br />	"businessType": "1",<br />  "tag": 1, //首次1，增量2 <br />}<br /><br /><br />逐仓 marginMode:"2"<br /><br />{<br />	"data": {<br />		"list": [{<br />			"orderType": 1,<br />			"side": 1,<br />			"planType": 1,<br />			"quantity": 100,<br />			"positionSide": 1,<br />			"currencyPairId": 1001,<br />			"marginMode": 1,<br />			"userId": 1,<br />			"stopPrice": 11.3,<br />			"price": 20.3,<br />			"tenantId": 11,<br />			"id": 1000001,<br />			"userType": 2,<br />			"businessType": 1,<br />			"workingType": 1,<br />			"status": 2<br />		}]<br />	},<br />	"marginMode": 2,<br />	"type": "ASSET",<br />	"userId": 1,<br />	"businessType": "1",<br />  "tag": 1, //首次1，增量2 <br />} | <br /><br />找马永旭联调 |
| 增量返回 | {    "data": [<br />        {<br />            "orderType": 1,<br />            "side": 1,<br />            "planType": 1,<br />            "quantity": 100,<br />            "positionSide": 1,<br />            "currencyPairId": 1001,<br />            "marginMode": 1,<br />            "userId": 1,<br />            "stopPrice": 11.3,<br />            "price": 20.3,<br />            "tenantId": 11,<br />            "id": 1000001,<br />            "userType": 2,<br />            "businessType": 1,<br />            "workingType": 1,<br />            "status": 2<br />        }<br />    ],<br />    "marginMode": 2,<br />    "type": "ASSET",<br />    "userId": 1,<br />     "businessType": "1",<br />    "tag":"1"//首次1，增量2  <br />    <br />} |  |


<a name="QlJYe"></a>
## 通知类型消息
| 通知类型消息(前置条件登录) |  |  |
| --- | --- | --- |
| 请求 | {"event":"SUB","type":"ORDER",  "businessType":"USDT"} |  |
| 订阅回执 | {"code":1,"desc":"success","type":"ORDER"} |  |
| 增量返回 | {"type":"ORDER","businessType":"USDT","userId":1,"data":{"currencyPairId":1001,"orderType":1,"price":"1000","quantity":"200","leverage":"100","side":1,"positionSide":1,"operationType":101}} | currencyPairId：币对id<br />orderType：类型 1-限价 2-市价<br />price：价格<br />quantity：数量<br />leverage：杠杆<br />side： 买卖方向,1:买,2:卖<br />positionSide：持仓方向,1:多,2:空<br />operationType：操作类型，101：成交，102：委托 |


<a name="Ot85B"></a>
## 登录
| 登录 |  |  |
| --- | --- | --- |
| 请求 | {"event":"LOGIN","params": {"token":"eyJhY2Nlc3NUb2tlbiI6IntcInVpZFwiOjMzLFwidXNlcklkU2hvd1wiOlwiYWFcIixcInRpbWVzdGFtcFwiOjE2MjU4MTUzNDAyNDAsXCJ0ZW5hbmN5XCI6ODY0MDAwMDAsXCJyYW5kb21cIjpcIjM0ZjFkMmM5LTNiZjEtNGIwMC04NWFiLTIyZDcwNWVjODY2NlwifSIsImFsZyI6IkhTMjU2In0.eyJhdWQiOiJhdXRob3IifQ.nrJ50fCIgvePww70gKt6Rq8QOJIsPOWZLWXVGnia0aQ"}} |  |
| 登录回执 | {"code":1,"desc":"success","type":"LOGIN"} |  |

<a name="eZGYU"></a>
## 批量指数推送（用于仓位涨幅计算）
| 批量指数推送（用于仓位涨幅计算） |  |
| --- | --- |
| 请求订阅 | {"event":"SUB","type":"INDEX_PRICE_ALL","params": {"ids": "1031044,1041044"}} |
| 订阅回执 | {"code":1,"desc":"success","type":"INDEX_PRICE_ALL","first":true} |
| 取消订阅 | {"event":"UNSUB","type":"INDEX_PRICE_ALL"} |
| 首次返回 | {"type":"INDEX_PRICE_ALL","data":[{"pid":1031044,"data":"54.1154"},{"pid":1041044,"data":"54"}],"first":true} |
| 增量返回 | {"type":"INDEX_PRICE_ALL","data":[{"pid":1031044,"data":"18.1118"},{"pid":1041044,"data":"18"}]} |

