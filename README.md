**Table of Contents**
- [GET TICKER](#get-ticker)
- [GET ORDER BOOK](#get-order-book)


## GET TICKER

24 hour price change statistics. Careful when accessing this no symbol.

```http
GET https://api.wenxpro.com/openapi/quote/v1/ticker/24hr
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `symbol`| `string` | Symbol Name.  E.g ETHBTC (**Optional**) |

### REQUEST


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

### RESPONSE

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

### REQUEST

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

### RESPONSE

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



## Status Codes

wenxpro returns the following status codes in its API:

| Status Code | Description |
| :--- | :--- |
| 200 | `OK` |
| 400 | `BAD REQUEST` |
| 404 | `NOT FOUND` |
| 500 | `INTERNAL SERVER ERROR` |
