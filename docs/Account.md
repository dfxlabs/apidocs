User Api
===========


# 1. Get User information
## GET `/api/v1/user/info`



| **PARAMETER** | **TYPE** | **Mandatory** | **DESCRIPTION** |
| --- | --- | --- | --- |
|   No Parameters|


``` java
{
	"code": "0",
	"msg": "success",
	"data": {
		"clientType": "OP",
		"accounts": [{
			"id": "1403134775",
			"name": "ccc",
			"type": "SUB",
			"status": "ACTIVE",
			"enableTrading": true
		}, {
			"id": "1156814394",
			"name": "123123",
			"type": "SUB",
			"status": "ACTIVE",
			"enableTrading": true
		}, {
			"id": "2",
			"name": "haha",
			"type": "SUB",
			"status": "ACTIVE",
			"enableTrading": true
		}]
	}
}
```



# 2、 Get Account Balance information
## GET `/api/v1/account/balance`



| **PARAMETER** | **TYPE** | **Mandatory** | **DESCRIPTION** |
| --- | --- | --- | --- |
| accountId | STRING | YES | Account ID |
| token             | STRING    | NO | Token Code, e.g. `ETH`



``` java
{
	"code": "0",
	"msg": "success",
	"data": [{
		"tokenId": 1,
		"tokenCode": "BTC",
		"total": "100000005079.99928",
		"avaliable": "99999999999.87084",
		"frozen": "5080.12844"
	}, {
		"tokenId": 2,
		"tokenCode": "ETH",
		"total": "100000005037",
		"avaliable": "100000000000",
		"frozen": "5037"
	}, {
		"tokenId": 3,
		"tokenCode": "USDT",
		"total": "100541314472.2230964",
		"avaliable": "99818221220.3435715",
		"frozen": "723093251.8795249"
	}, {
		"tokenId": 4,
		"tokenCode": "HKD",
		"total": "100000000000",
		"avaliable": "100000000000",
		"frozen": "0"
	}, {
		"tokenId": 5,
		"tokenCode": "USD",
		"total": "100000000000",
		"avaliable": "100000000000",
		"frozen": "0"
	}, {
		"tokenId": 6,
		"tokenCode": "STK",
		"total": "100000000000",
		"avaliable": "100000000000",
		"frozen": "0"
	}]
}
```



# 3、 Get Account Trade List information.
## GET `/api/v1/account/trades`



| **PARAMETER** | **TYPE** | **Mandatory** | **DESCRIPTION** |
| --- | --- | --- | --- |
| symbol | STRING | NO | Trading pair, e.g. `BTC-USDT` |
| accountId | STRING | NO | Account ID |
| orderId | LONG | NO | Order ID |
| fromId | LONG | NO | Start from tradeId, exclusive  |
| startTime | LONG | NO | Start timestamp on order creation time |
| endTime | LONG | NO | End timestamp on order creation time |
| limit | INTEGER | NO | 10 by default, with a maximum limit of 100 items |
#### *Trades are returned in descending order of tradeId


``` java
{
	"code": "0",
	"msg": "success",
	"data": [{
		"tradeId": "663522",
		"symbol": "BTC-USDT",
		"price": "68986.17",
		"quantity": "0.00082",
		"amount": "56.5686594",
		"type": "LIMIT",
		"side": "BUY",
		"isMaker": true,
		"feeAsset": "BTC",
		"fee": "0.00000123",
		"time": "1712739162861"
	}, {
		"tradeId": "663521",
		"symbol": "BTC-USDT",
		"price": "68924.17",
		"quantity": "0.00105",
		"amount": "72.3703785",
		"type": "LIMIT",
		"side": "BUY",
		"isMaker": true,
		"feeAsset": "BTC",
		"fee": "0.000001575",
		"time": "1712739158534"
	}]
}
```
