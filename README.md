**Table of Contents**
- [GET PAIR](#get-pair)
- [GET TICKER](#get-ticker)
- [GET ORDER BOOK](#get-order-book)
- [GET TRADE](#get-trade)

## GET PAIR
Current broker trading rules and symbol information.

```http
GET https://api.wenxpro.com/openapi/v1/brokerInfo
```
### **Parameters:**

None

### RESPONSE BODY
name|type|example|description
------------ | ------------ | ------------ | ------------
`timezone`|string|`UTC`|Timezone of timestamp
`serverTime`|long|`1554887652929`|Retrieves the current time on server (in ms).

In the `symbols` field, the endpoint will return information on current actively trading cryptos. You can ignore this section.

In the `options` field:
All actively trading options will be displayed.

Name|Type|Example|Description
------------ | ------------ | ------------ | ------------
`symbol`|string|`BTC0308CS3900`|Name of the option
`status`|string|`TRADING`|Status of the option
`baseAsset`|string|`BTC0308CS3900`|Underlying asset for the option
`baseAssetPrecision`|float|`0.001`|Precision of the option quantity
`quoteAsset`|string|`BUSDT`|Quote asset for the option
`quoteAssetPrecision`|float|`0.01`|Precision of the option price
`icebergAllowed`|string|`false`|Whether iceberg orders are allowed.

For `filters` in `options` field:

Name|Type|Example|Description
------------ | ------------ | ------------ | ------------
`filterType`|string|`PRICE_FILTER`|Type of the filter.
`minPrice`|float|`0.001`|Precision of the option price。
`maxPrice`|float|`100000.00000000`|
`tickSize`|float|`0.001`|Precision of the option price.
`minQty`|float|`0.01`|Minimal trading quantity of the option
`maxQty`|float|`100000.00000000`|
`stepSize`|float|`0.001`|Precision of the option quantity
`minNotional`|float|`1`|Precision of the option order size (quantity * price)

```javascript
{
  'timezone': 'UTC',
  'serverTime': '1555048558151',
  'brokerFilters': [],
  'symbols': [{...}],
  'options': [
        {
          'filters': [
            {
              'minPrice': '0.01',
              'maxPrice': '100000.00000000',
              'tickSize': '0.01',
              'filterType': 'PRICE_FILTER'
            },
            {
              'minQty': '0.01',
              'maxQty': '100000.00000000',
              'stepSize': '0.001',
              'filterType': 'LOT_SIZE'
            },
            {
              'minNotional': '1',
              'filterType': 'MIN_NOTIONAL'
            }
          ],
          'exchangeId': '301',
          'symbol': 'BTC0412PS5100',
          'status': 'TRADING',
          'baseAsset': 'BTC0412PS5100',
          'baseAssetPrecision': '0.001',
          'quoteAsset': 'USDT',
          'quotePrecision': '0.01',
          'icebergAllowed': False
          },...
        ]
}

```

## GET TICKER

24 hour price change statistics. Careful when accessing this no symbol.

```http
GET https://api.wenxpro.com/openapi/quote/v1/ticker/24hr
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `symbol`| `string` | Symbol Name.  E.g ETHBTC (**Optional**) |

### RESPONSE BODY


```javascript
## Single ticker 
{
  "time": 1538725500422,
  "symbol": "ETHBTC",
  "bestBidPrice": "4.00000200",
  "bestAskPrice": "4.00000200",
  "lastPrice": "4.00000200",
  "openPrice": "99.00000000",
  "highPrice": "100.00000000",
  "lowPrice": "0.10000000",
  "volume": "8913.30000000"
}
## Multiple ticker info when symbol is omiited
[
  {
    "time": 1538725500422,
    "symbol": "ETHBTC",
    "lastPrice": "4.00000200",
    "openPrice": "99.00000000",
    "highPrice": "100.00000000",
    "lowPrice": "0.10000000",
    "volume": "8913.30000000"
 },...
```

### RESPONSE DESCRIPTION

| Name | Type | Example | Description
| :--- | :--- | :--- | :--- |
| `time`| `long` | 1538728740000 | Open Time
| `symbol`| `string` | ETHBTC | Symbol Name
| `bestBidPrice`| `float` | 4.000002000 | Best Bid Price
| `bestAskPrice`| `float` | 4.000002000 | Best Ask Price
| `lastPrice`| `float` | 4.000002000 | Last Price
| `openPrice`| `float` | 99.0000000 | Open Price
| `highPrice`| `float` | 100.0000000 | High Price
| `lowPrice`| `float` | 0.10000000 | Low Price
| `volume`| `float` | 8913.300000 | Trade Volume





## GET ORDER BOOK

This endpoint retrieve market depth data.

```http
GET https://api.wenxpro.com/openapi/quote/v1/depth
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `symbol`| `string` |  Symbol Name. E.g ETHBTC  (**Required**)  |
| `limit`| `integer` |  Symbol Name. E.g ETHBTC  (**Optional**)  |

### RESPONSE BODY

Successfully retrieved market depth data

```javascript
{
  "bids": [
    [
      "3.90000000",   // PRICE
      "431.00000000"  // QTY
    ],
    [
      "4.00000000",
      "431.00000000"
    ]
  ],
  "asks": [
    [
      "4.00000200",  // PRICE
      "12.00000000"  // QTY
    ],
    [
      "5.10000000",
      "28.00000000"
    ]
  ]
}
```

### RESPONSE DESCRIPTION

| Name | Type | Example | Description
| :--- | :--- | :--- | :--- |
| `time`| `long` | 1550829103981 | Current timestamp (ms)
| `bids`| `list` | (see below) | List of all bids, best bids first. See below for entry details.
| `asks`| `list` | (see below) | List of all asks, best asks first. See below for entry details.

The fields `bids` and `asks` are lists of order book price level entries, sorted from best to worst.

| Name | Type | Example | Description
| :--- | :--- | :--- | :--- |
| '' | `float` | 123.10 | price level
| '' | `float` | 300 | The total quantity of orders for this price level



## GET TRADE

This endpoint retrieves latest trades

```http
GET https://api.wenxpro.com/openapi/quote/v1/trades
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `symbol`| `string` |  Symbol Name. E.g. BTCUSDT (**Required**)  |
| `limit`| `integer` |  Default 500; Max 1000  (**Optional**)  |

### RESPONSE BODY

Successfully retrieved recent trades

```javascript
[
  {
    "price": "4.00000100",
    "qty": "12.00000000",
    "time": 1499865549590,
    "isBuyerMaker": true
  },...
]
```

### RESPONSE DESCRIPTION

| Name | Type | Example | Description
| :--- | :--- | :--- | :--- |
| `price`| `float` | 0.055 | The price of the trade
| `time`| `long` | 1537797044116 | Current timestamp (ms)
| `qty`| `float` | 5 | The quantity traded
| `isBuyerMaker`| `string` | true | Maker or taker of the trade. true= maker, false = taker



## Status Codes

wenxpro returns the following status codes in its API:

| Status Code | Description |
| :--- | :--- |
| 200 | `OK` |
| 400 | `BAD REQUEST` |
| 404 | `NOT FOUND` |
| 500 | `INTERNAL SERVER ERROR` |
