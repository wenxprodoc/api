
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
| `symbol`| `string` | **Optional**. Symbol Name.  E.g ETHBTC |

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

| Parameter | Type | Example | Description
| :--- | :--- | :--- |
| `time`| `long` | 1538728740000 | Open Time
| `symbol`| `string` | ETHBTC | Symbol Name
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time
| `time`| `long` | 1538728740000 | Open Time



The `message` attribute contains a message commonly used to indicate errors or, in the case of deleting a resource, success that the resource was properly deleted.

The `success` attribute describes if the transaction was successful or not.

The `data` attribute contains any other metadata associated with the response. This will be an escaped string containing JSON data.

## Status Codes

Gophish returns the following status codes in its API:

| Status Code | Description |
| :--- | :--- |
| 200 | `OK` |
| 201 | `CREATED` |
| 400 | `BAD REQUEST` |
| 404 | `NOT FOUND` |
| 500 | `INTERNAL SERVER ERROR` |
