
# Introduction

Gophish was built from the ground-up with a JSON API that makes it easy for developers and sysadmins to automate simulated phishing campaigns.

These docs describe how to use the [Gophish](https://getgophish.com) API. We hope you enjoy these docs, and please don't hesitate to [file an issue](https://github.com/gophish/gophish/issues/new) if you see anything missing.

{% hint style="info" %}
**Is Python your language of choice?** If so, we have a [fully-supported Python API client](https://docs.getgophish.com/python-api-client/) that makes working with the Gophish API a piece of cake!
{% endhint %}

## Use Cases

There are many reasons to use the Gophish API. The most common use case is to gather report information for a given campaign, so that you can build custom reports in software you're most familiar with, such as Excel or Numbers.

However, automating the creation of campaigns and campaign attributes such as templates, landing pages, and more provides the ability to create a fully automated phishing simulation program. This would allow campaigns to be run throughout the year automatically. This also allows the Gophish administrator to be included in the campaigns, since they wouldn't know exactly which day it would start!

## GET TICKER

24 hour price change statistics. Careful when accessing this no symbol.

```http
GET https://api.wenxpro.com/openapi/quote/v1/ticker/24hr
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `symbol`| `string` | Symbol Name.  E.g ETHBTC **Optional** |

## Responses


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

## RESPONSE

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


## GET TICKER

24 hour price change statistics. Careful when accessing this no symbol.

```http
GET https://api.wenxpro.com/openapi/quote/v1/depth
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `symbol`| `string` |  Symbol Name. E.g ETHBTC  **Required**  |
| `limit`| `integer` |  Symbol Name. E.g ETHBTC  **Optional**  |

## Responses

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

## RESPONSE

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
