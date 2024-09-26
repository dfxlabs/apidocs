Market
===========

# 1. Get Depth information

## GET `/api/v1/spot/depth`


| **PARAMETER** | **TYPE** | **Mandatory** | **DESCRIPTION** |
| --- | --- | --- | --- |
| symbol | STRING | YES | Trading pair, e.g. `BTC-USDT` |
| limit | INTEGER | NO | The number of items returned by each query, default 10 |



``` java
{
	"code": "0",
	"msg": "success",
	"data": {
		"lastUpdateId": 21302031,
		"symbol": "BTC-USDT",
		"asks": [
					["69185.83", "0.001"],
					["69203.83", "0.00012"],
					["69215.83", "0.00052"],
					["69239.83", "0.00068"],
					["69256.83", "0.00022"],
					["69313.83", "0.00041"],
					["69606.81", "0.00041"],
					["69615.81", "0.00143"],
					["69626.81", "0.0014"],
					["69630.81", "0.00008"]
				],
		"bids": [
					["69153.83", "0.00062"],
					["69147.83", "0.0009"],
					["69023.83", "0.00091"],
					["68976.83", "0.00011"],
					["68954.83", "0.00043"],
					["68875.83", "0.001"],
					["68822.83", "0.00072"],
					["68771.83", "0.00139"],
					["68644.81", "0.00117"],
					["68642.81", "0.00097"]
			]
		}
	}
```



# 2. Get Recent Transaction Records information
## GET `/api/v1/spot/trade`


| **PARAMETER** | **TYPE** | **Mandatory** | **DESCRIPTION** |
| --- | --- | --- | --- |
| symbol | STRING | YES | Trading pair , e.g. `BTC-USDT` |
| limit | INTEGER | NO | The number of items returned by each query, default 10 |



``` java
{
	"code": "0",
	"msg": "success",
	"data": [{
			"price": "69169.83",
			"quantity": "0.00107",
			"amount": "74.0117181",
			"time": "1712741081857",
			"isBuyerMaker": true
		}, {
			"price": "69137.81",
			"quantity": "0.00078",
			"amount": "53.9274918",
			"time": "1712741076833",
			"isBuyerMaker": true
		}
	}]
```



# 3. Get Kline information
## GET `/api/v1/spot/kline`


| **PARAMETER** | **TYPE** | **Mandatory** | **DESCRIPTION** |
| --- | --- | --- | --- |
| symbol | STRING | YES | Trading pair, e.g. `BTC-USDT` |
| interval | STRING    | YES | kline type, e.g. `M1, M3, M5, M15, M30, H1, H2, H4, H6, H8, H12, D1, W1, MON1`
| limit | INTEGER | NO | The number of items returned by each query, default 10, max 500 |
| startTime    | LONG    | NO | StartTime in milliseconds, e.g. `1678772870000`
| endTime    | LONG    | NO | endTime in milliseconds, e.g. `1678772870000`

**If startTime and endTime are not provided, the server's default time will be used. For example, if querying minute-based K-line data with limit=10, the data for the last ten minutes will be retrieved. If querying daily K-line data with limit=20, the data for the last twenty days will be retrieved.**

``` java
		{
			"code": "0",
			"msg": "success",
			"data": [
				[1712742060000(current timestamp), "68986.54"(openPrice), "69097.9"(highestPrice), "68938.8"(lowestPrice), "68993.9"(closePrice), "0.00862"( quantity of base currency), 1712742119999(close timestamp), "594.8774428"(quantity of quote currency), 12(count of trades happened during the kline startTime and closeTime), "0"(Taker buy base asset volume), "0"(Taker buy quote asset volume)],
				[1712742120000, "68952.9", "69035.9", "68920.9", "69035.9", "0.00944", 1712742179999, "651.210746", 12, "0", "0"],
				[1712742180000, "68991.4", "69041.43", "68898.4", "69014.93", "0.00909", 1712742239999, "627.2675547", 12, "0", "0"],
				[1712742240000, "69054.93", "69054.93", "68942.93", "69025.43", "0.01011", 1712742299999, "697.6899023", 12, "0", "0"],
				[1712742300000, "69007.43", "69048.43", "68983.93", "69015.43", "0.00891", 1712742359999, "614.9698663", 12, "0", "0"],
				[1712742360000, "69012.93", "69102.43", "68991.93", "69024.43", "0.00863", 1712742419999, "595.6636409", 11, "0", "0"],
				[1712742420000, "69008.43", "69071.43", "68950.93", "68979.81", "0.00852", 1712742479999, "588.1277438", 12, "0", "0"],
				[1712742480000, "68910.81", "69064.59", "68848.31", "69064.59", "0.01155", 1712742539999, "796.3953895", 12, "0", "0"],
				[1712742540000, "68960.59", "69038.05", "68943.05", "68943.05", "0.00992", 1712742599999, "684.3789962", 12, "0", "0"],
				[1712742600000, "68988.05", "69029.37", "68888.01", "69013.51", "0.00695", 1712742659999, "479.3320907", 8, "0", "0"]
			]
		}

```



# 4. Get Quotes in the last 24 hours information
## GET `/api/v1/spot/ticker/24hr`


| **PARAMETER** | **TYPE** | **Mandatory** | **DESCRIPTION** |
| --- | --- | --- | --- |
| symbol | STRING | YES | Trading pair, e.g. `BTC-USDT` |




``` java
{
	"code": "0",
	"msg": "success",
	"data": {
		"symbol": "BTC-USDT",
		"priceChange": "-1358.93",
		"priceChangePercent": "-1.93",
		"weightedAvgPrice": "69207.1619993331955896",
		"lastPrice": "69169.83",
		"openPrice": "70528.76",
		"highPrice": "70529.1",
		"lowPrice": "68727.05",
		"volume": "0.01",
		"amount": "147380.8039073"
	}
}

```



# 5. Get Latest price（reference Price） information
GET `/api/v1/spot/ticker/price`

###  Note
* Please note that the reference price is the last transaction price of frequently traded items.
If there are no transactions within a certain period, DFX will set the reference price to the
average market price. For more details, please refer to the DFX Labs Trading Rules and Operations
[please refer Here.](https://github.com/dfxlabs/dfxlabs.github.io/blob/main/docs/Public%20Market%20Data.md).


| **PARAMETER** | **TYPE** | **Mandatory** | **DESCRIPTION** |
| --- | --- | --- | --- |
| symbol | STRING | YES | Trading pair, e.g. `BTC-USDT` |




``` java
{
	"code": "0",
	"msg": "success",
	"data": "69169.83"
}

```




# 6. Get Symbol Order Top Of Book information.
## GET `/api/v1/spot/ticker/book_ticker`

| **PARAMETER** | **TYPE** | **Mandatory** | **DESCRIPTION** |
| --- | --- | --- | --- |
| symbol | STRING | YES | Trading pair, e.g. `BTC-USDT` |




``` java
{
	"code": "0",
	"msg": "success",
	"data": {
		"symbol": "BTC-USDT",
		"ask": [
			["69185.83", "0.001"]
		],
		"bid": [
			["69153.83", "0.00062"]
		],
		"time": 1712741085087
	}
}

```



# 7. Get Symbol Basic information.
## GET `/api/v1/symbols`


| **PARAMETER** | **TYPE** | **Mandatory** | **DESCRIPTION** |
| --- | --- | --- | --- |
| clientType | STRING | YES | Client Type, e.g. `OP, CP, IP, CR, IR` |
| symbol | STRING | NO | Trading pair, e.g. `BTC-USD` |



``` java
		{
			"code": "0",
			"msg": "success",
			"data": [{
				"symbol": "BTC-USD",
				"baseToken": "BTC",
				"quoteToken": "USD",
				"quoteIncrement": "0.01",
				"quoteMinSize": "5",
				"baseIncrement": "0.00001",
				"baseMinSize": "0.00001",
				"priceIncrement": "0.01",
				"enableTrading": true,
				"priceLimitRate": "0.1"
			}, {
				"symbol": "ETH-USD",
				"baseToken": "ETH",
				"quoteToken": "USD",
				"quoteIncrement": "0.01",
				"quoteMinSize": "5",
				"baseIncrement": "0.0001",
				"baseMinSize": "0.0001",
				"priceIncrement": "0.01",
				"enableTrading": true,
				"priceLimitRate": "0.1"
			}, {
				"symbol": "BTC-USDT",
				"baseToken": "BTC",
				"quoteToken": "USDT",
				"quoteIncrement": "0.01",
				"quoteMinSize": "5",
				"baseIncrement": "0.00001",
				"baseMinSize": "0.00001",
				"priceIncrement": "0.01",
				"enableTrading": true,
				"priceLimitRate": "0.1"
			}, {
				"symbol": "ETH-USDT",
				"baseToken": "ETH",
				"quoteToken": "USDT",
				"quoteIncrement": "0.01",
				"quoteMinSize": "5",
				"baseIncrement": "0.0001",
				"baseMinSize": "0.0001",
				"priceIncrement": "0.01",
				"enableTrading": true,
				"priceLimitRate": "0.1"
			}, {
				"symbol": "USDT-USD",
				"baseToken": "USDT",
				"quoteToken": "USD",
				"quoteIncrement": "0.01",
				"quoteMinSize": "5",
				"baseIncrement": "0.01",
				"baseMinSize": "5",
				"priceIncrement": "0.01",
				"enableTrading": false,
				"priceLimitRate": "0.01"
			}]
		}

```
