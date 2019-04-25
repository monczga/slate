---
title: Bitclude - API Reference

language_tabs: # must be one of https://git.io/vQNgJ
    - jsonnet: 

toc_footers:
  - <a href='https://panel.bitclude.com/account'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:

search: true
---
<div class="navbar-container">
    <nav class="navbar">
    <a class="logo-container" href="/"><div class="logo"></div></a>
    <ul>
    <li><a href="https://blog.bitclude.com/">Blog</a></li>
    <li><a href="https://panel.bitclude.com">Dashboard</a>
    <li><a href="https://status.bitclude.com">Status</a></li>
    </ul>
    </nav>
</div>

# Bitclude

In Bitclude we care about developers, if you have any suggestions please share them at <support@bitclude.com> please also note that due to the huge traffic passing through our servers, 
we try to use only specific trading communication.


# Authentication
To autenticate you can use your API keys which you can generate in 'account' tab, in case the keys leak please generate new one, if you will have probblem with that please contact <support@bitclude.com>.

You can generate keys [admin panel](https://panel.bitclude.com/account)

|Parameter|	Value |	Default	| Description
|----|-----|--|--|
|id	| INT | false | It is account id, can be find in 'account' tab.
|key|	STRING|	false|	It is token to authentication on API.


<aside class="notice">
You must generate <code>key</code> in your panel..
</aside>

# Limitations and restrictions


## Maximum number of calls

   * Public API 600 calls within 10 minutes.
   * Private API 300 calls within 10 minutes. Limits are calculated in relation to IP address.
   
   If you wish to increase the limit, please contact us.
   
# Public Data
 
## Orderbook

```json
            {
                "data": {
                    "market1": "BTC",
                    "market2": "PLN",
                    "timestamp": 1556101333
                },
                "bids": [
                    [
                        "0.01904635",
                        "20955.35"
                    ],
                    [
                        "0.00701408",
                        "20933.70"
                    ],
                ],
                "asks": [
                    [
                        "0.07903711",
                        "21132.75"
                    ],
                    [
                        "0.07052097",
                        "21141.04"
                    ],
            
                ]
            }
```

This endpoint allow you to get orderbook of single market

### HTTP Request
 
`GET https://api.bitclude.com/stats/orderbook_{market1}{market2}.json`
 
### Query Parameters
|Parameter	| Default | Values
|--|--|--|
|market1 | false | btc, ltc, bch ...
|market2 | false | btc, usd, eur ...
<aside class="notice">
  <code>btc / fiat market1</code> is always btc and market2 is 'fiat' currency,
 <br><code>crypto / btc market1</code> is always cryptocurrency and market2 is btc
</aside>
<aside class="success">
  Example url: <code>https://api.bitclude.com/stats/orderbook_btcusd.json</code>
<br> or <code>https://api.bitclude.com/stats/orderbook_ltcbtc.json</code>
</aside>
## Ticker

```json
            {
                "btc_pln": {
                    "bind": "crypto_fiat",
                    "last": "29008.57",
                    "ask": "1500.00",
                    "bid": "500.00",
                    "volumen": "0.02255062",
                    "max24H": "29008.57",
                    "min24H": "500.00",
                    "change": "96.61 %"
                },
                "ltc_btc": {
                    "bind": "crypto_crypto",
                    "last": "0.01395027",
                    "ask": "0.01404759",
                    "bid": "0.01395797",
                    "volumen": "0.01973978",
                    "max24H": "0.01395300",
                    "min24H": "0.01300340",
                    "change": "0.00 %"
                },
                ...
            }
```
 
 This endpoint allow you to get whole ticker data for all currencies
 
###HTTP Request
 
`GET https://api.bitclude.com/stats/ticker.json`
 
###Query Parameters

none
 
##History
 
```json
         {  
            "data":{  
               "market1":"BTC",
               "market2":"USD",
               "timestamp":1531917577
            },
            "history":[  
               {  
                  "time":1531917229,
                  "nr":"786",
                  "amount":"0.00018620",
                  "price":"7314.57",
                  "type":"a"
               },
               {  
                  "time":1531915300,
                  "nr":"783",
                  "amount":"0.00011760",
                  "price":"7314.57",
                  "type":"a"
               },
               {  
                  "time":1531911605,
                  "nr":"776",
                  "amount":"0.00010240",
                  "price":"7314.57",
                  "type":"a"
               }
            ]
         }
```

 This endpoint allow you to get history on one market
 
###HTTP Request
`GET https://api.bitclude.com/stats/history_{market1}{market2}.json`
 
###Query Parameters
|Parameter | Default | Values
|--|--|--|
|market1|false|btc, ltc, bch ...
|market2|false|btc, usd, eur ...

<aside class="notice">
  <code>btc / fiat market1</code> is always btc and market2 is 'fiat' currency,
 <br><code>crypto / btc market1</code> is always cryptocurrency and market2 is btc
</aside>
<aside class="success">
  Example url: <code>https://api.bitclude.com/stats/history_btcusd.json</code>
<br>or <code>https://api.bitclude.com/stats/history_ltcbtc.json</code>
</aside>
#Private
##Get info

```json
            {
                "success": true,
                "account": {
                    "nick": "test@bitclude.com",
                    "email": "test@bitclude.com",
                    "phone": "+48000000000",
                    "key_default": "..23082...",
                    "last_ip": "127.0.0.1",
                    "state": "2",
                    "data": {
                        "name": "John",
                        "surname": "Kowalski"
                    },
                    "fee": {
                        "maker": "0",
                        "taker": "0"
                    }
                },
                "balances": {
                    "USD": {
                        "active": "0.01",
                        "inactive": "0.00"
                    },
                    ...
                    "BTC": {
                        "active": "0.10458625",
                        "inactive": "0.00000000"
                },
                "deposit": {
                    "BTC": false,
                    "BCH": false,
                    "LTC": false
                },
                "has_address": true,
                "debit_fee": "0.03"
            }
```

 This endpoint allow you to get basic information about account
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter	| Value	| Description
|--|--|--|
|method | account | Read from account
|action | info | Get information
|id	| INT | eg. 918872936
|key |STRING | eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>
##Get history

```json
         {
             "success": true,
             "history": [
                 {
                     "currency1": "btc",
                     "currency2": "usd",
                     "amount": "0.00003251",
                     "time_close": 1516130375,
                     "price": "15380.22",
                     "fee_taker": "0",
                     "fee_maker": "0",
                     "type": "bid",
                     "action": "open"
                 },
                 {
                     "currency1": "btc",
                     "currency2": "usd",
                     "amount": "0.00003251",
                     "time_close": 1516130376,
                     "price": "15380.22",
                     "fee_taker": "0",
                     "fee_maker": "0",
                     "type": "bid",
                     "action": "open"
                 },...
                 {
                     "currency1": "btc",
                     "currency2": "usd",
                     "amount": "0.00100000",
                     "time_close": 1516212758,
                     "price": "4.00",
                     "fee_taker": "50",
                     "fee_maker": "0",
                     "type": "bid",
                     "action": "open"
                 }
               ]
         }
```
 This endpoint allow you to get history of all your transactions.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action | history | Get information
| id | INT | eg. 918872936
| key | STRING | eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>
<aside class="notice">
<code>fee taker</code> and <code>fee maker</code> represent 0.0001 * fee of trade.
</aside>
##Get volumes

```json
         {
             "success": true,
             "volumes": [
                 {
                     "amount": "0.97140262",
                     "currency": "btc"
                 }
             ]
         }
```
 This endpoint allow you to get history of all your transactions.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action | volumes | Get volumes
| id | INT | eg. 918872936
| key | STRING | eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>
##Get affiliation

```json
            {
                "success": true,
                "affiliate": {
                    "earned": 0,
                    "verified": "3",
                    "registered": "5",
                    "earnTabele": {
                        "usd": "320.00",
                        "eur": "0.00",
                        "gbp": "0.00",
                        "pln": "0.00",
                        "btc": "0.00205100",
                        "ltc": "0.00000000",
                        "bch": "0.00000000"
                    },
                    "list": []
                }
            }
```

This endpoint allow you to get history of all your transactions.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action | affiliate | Get affiliations
| id | INT | eg. 918872936
| key | STRING | eg. '54a44eb00b63f4d1cdde9...'
  
<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

##Get deposits

```json
         {
             "success": true,
             "history": [
                 {
                     "time": "1530883428",
                     "amount": "0.13750000",
                     "type": "b787400027b4eae298bad72150384540a23342daaa3eec1c8d17459c103c6bbc",
                     "state": "1"
                 },
                 {
                     "time": "1530887151",
                     "amount": "0.06875000",
                     "type": "1cc2b5a1f05ffda29d669077e0c7aa23ee99be3bd767833a23d9ea8b6684dd3d",
                     "state": "1"
                 },
                 {
                     "time": "1531220889",
                     "amount": "1.10000000",
                     "type": "4b6ae6d18f670cda08245f610f36e4199ac889c9ab18eb085e2834d9a1dbddcf",
                     "state": "1"
                 }
             ]
         }
```
This endpoint allow you to get information about deposits.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action | deposits|Get deposits
| currency	|btc, usd..	|Currency of deposits
| id	|INT	|eg. 918872936
| key	|STRING	|eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

##Get withdrawals

```json
         {
             "success": true,
             "history": [
                 {
                     "time": "1528545117",
                     "amount": "0.99482707",
                     "tx": "",
                     "address": "2N8hwP1WmJrFF5QWABn38y63uYLhnJYJYTF",
                     "state": "0"
                 },
                 {
                     "time": "1528715035",
                     "amount": "1.00000000",
                     "tx": "",
                     "address": "2N8hwP1WmJrFF5QWABn38y63uYLhnJYJYTF",
                     "state": "0"
                 },
                 {
                     "time": "1528812738",
                     "amount": "0.00100000",
                     "tx": "",
                     "address": "2N8hwP1WmJrFF5QWABn38y63uYLhnJYJYTF",
                     "state": "0"
                 },
                 {
                     "time": "1530883173",
                     "amount": "0.11589066",
                     "tx": "01b8ae6437843879574b69daf95542aff43a4aefaa90e8f70ebf572eccf01cad",
                     "address": "2N8hwP1WmJrFF5QWABn38y63uYLhnJYJYTF",
                     "state": "1"
                 }
             ]
         }
```

This endpoint allow you to get information about withdrawals.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action	|withdrawals	|Get withdrawals
| currency	|btc, usd..	|Currency of deposits
| id	|INT	|eg. 918872936
| key|	STRING	|eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

##Get limits

```json
         {
             "success": true,
             "limitMonthly": 0,
             "limitYearly": 0
         }
```
 This endpoint allow you to get information about limits of user.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action|	limits | Get limits
| id	|INT	|eg. 918872936
| key	|STRING	|eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

##Get wallets status

```json
         {
             "success": true,
             "btc": {
                 "last_block_time": "344353",
                 "node_status": "1",
                 "is_online": true,
                 "connections": "12",
                 "current_optimal_fee": "0.00002500",
                 "current_minimum_amount": "0.00100000",
                 "decimal_point": "8",
                 "id": "1",
                 "confirmations": "2"
             },
             "usd": {
                 "last_block_time": "0",
                 "node_status": "1",
                 "is_online": true,
                 "connections": "1",
                 "current_optimal_fee": "1.00",
                 "current_minimum_amount": "10.00",
                 "decimal_point": "2",
                 "id": "2",
                 "confirmations": "2"
             },...
             "chf": {
                 "last_block_time": "0",
                 "node_status": "1",
                 "is_online": true,
                 "connections": "1",
                 "current_optimal_fee": "2.00",
                 "current_minimum_amount": "10.00",
                 "decimal_point": "2",
                 "id": "21",
                 "confirmations": "2"
             }
         }
```
 This endpoint allow you to get information about currencies, minimum transfers, fees, and online status.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action	| getwalletsstatus	| Get getwalletsstatus
| currency	| btc, usd..	| Currency of deposits
| id	| INT	| eg. 918872936
| key	| STRING	| eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

##Withdrawal funds

```json
            {
                "success": true,
                "code": "5039",
                "message": "withdrawal request has been submitted"
            }
```
 This endpoint allow you to get information about limits of user.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action	|withdrawal	|Init withdrawal
| currency	|btc, usd..	|Currency of deposits
| amount	|STRING	|Amount in string for eg. '10.00'
| address	|STRING	|IBAN or Cryptocurrency address
| id	|INT	| eg. 918872936
| key	|STRING |	eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>


##Withdrawal funds - confirmation
```json
         {
             "success": true,
             "message": "withdrawal request has been submited"
         }
```
 This endpoint allow you to get information about limits of user.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action	| withdrawalconfirm |	Confirm
| id	| INT	| eg. 918872936
| key	| STRING	| eg. '54a44eb00b63f4d1cdde9...'
| token	| STRING	| Token send via email - eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>
  
<aside class="notice">  
<code>token</code> Due the security resons confirmation tokens are send via email.
</aside>

##Account login history
```json
{
    "0": {
        "timestamp": "1556024864185000",
        "ip": "282.102.20.212",
        "city": "Copenhagen",
        "country": "Denmark",
        "device": "Mozilla/5.0 (...)",
        "status": "Correct standard authorization",
        "country_code": "DK"
    },
   "success": true
}
```
This endpoint allow you to get information about login history.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action	| history	| Confirm
| id	| INT	| eg. 918872936
| key	| STRING	| eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

##Freez account
```json
         {
             "success": true,
             "result": "Account freezed"
         }
```
 This endpoint allow you to freez your account.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action	| freeze |	Confirm
| id	| INT	| eg. 918872936
| key	| STRING| 	eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

##Active offers
```json
          {
             "success": true,
             "offers": [
                 {
                     "nr": "1053",
                     "currency1": "ltc",
                     "currency2": "btc",
                     "amount": "0.50000000",
                     "price": "0.00200000",
                     "id_user_open": "717998789",
                     "time_open": "1531132114012",
                     "offertype": "bid"
                 }
             ]
         }
```
 This endpoint allow you to get your current active offers.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action | activeoffers |  Get offers
| id | INT	| eg. 918872936
| key | STRING | eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>



#Converter
##Check rate
```json
        {
            "success": true,
            "fulfilled": true,
            "midRate": "524.15",
            "endRate": "0.00",
            "midAmount": "104.83",
            "endAmount": 0,
            "fee": "0.52",
            "rate": "524.15",
            "ratePublic": "524.15",
            "amountReceive": "104.83"
        }
```
 This endpoint allow you to check rate of conversion.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | account | Read from account
| action | convertercheck | Confirm
| market1 | btc, usd.. | Currency from
| market2 | btc, usd.. | Currency to
| amount | STRING | eg. '10.00'
| id | INT | eg. 918872936
| key | STRING | eg. '54a44eb00b63f4d1cdde9...'


<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>


##Convert
```json
        {
            "success": true,
            "code": "5067",
            "fee": "0.07",
            "amountReceived": "14.83",
            "message": "Your coins has been successfully converted",
            "ordersConsumed": {
                "sell": [
                         "2583"
                         ],
            "order": null
                 }
         }
```
 This endpoint allow you to simple convert your currencies.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method	| account | Read from account
| action | convert	| Confirm
| market1	| btc, usd..	| Currency from
| market2	| btc, usd..	| Currency to
| amount	| STRING	| eg. '10.00'
| id	| INT	| eg. 918872936
|  key	| STRING	| eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

  
#Transactions
 
##Buy [Limit]
```json
          {
             "success": true,
             "code": "5053",
             "actions": {
                 "buy": [],
                 "order": "5880"
             },
             "message": "Order has been submited"
         }
```

 This endpoint allow you to buy orders with 'limit' order.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | transactions | Transaction statement
| action	| buy	| Buy on market base currency
| market1	| btc, usd..	| First currency of market naming
| market2	| btc, usd..	| Seconde currency of market naming
| amount	| STRING	| eg. '10.00'
| rate  | STRING | eg. '5320.24'
| id	| INT	| eg. 918872936
| key	| STRING	| eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

<aside class="notice">
 Please note that <code>market1</code> and <code>market2</code> here are used as naming of markets so market <code>btc/usd</code>, 
 <br>have <code>market1 = btc</code> and <code>market2 = usd</code> don't metter if you buy or sell
</aside>

##Sell [Limit]
```json
         {
             "success": true,
             "code": "5053",
             "actions": {
                 "sell": [],
                 "order": "5880"
             },
             "message": "Order has been submited"
         }
```
 This endpoint allow you to sell orders with 'limit' order.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | transactions | Transaction statement
| action	| buy	| Buy on market base currency
| market1	| btc, usd..	| First currency of market naming
| market2	| btc, usd..	| Seconde currency of market naming
| amount	| STRING	| eg. '10.00'
| rate  | STRING | eg. '5320.24'
| id	| INT	| eg. 918872936
| key	| STRING	| eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

<aside class="notice">
 Please note that <code>market1</code> and <code>market2</code> here are used as naming of markets so market <code>btc/usd</code>, 
 <br>have <code>market1 = btc</code> and <code>market2 = usd</code> don't metter if you buy or sell
</aside>

##Cancel offer
```json
         {
             "success": true,
             "code": "5053",
             "actions": {
                 "sell": [],
                 "order": "5880"
             },
             "message": "Order has been submited"
         }
```
 This endpoint allow you to cancel your oder
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Type | Description
|--|--|--|
|method | transactions | Transaction statement
| action	| cancel	| Cancel one offer
| order	| INT	| Id of offer
| typ	| bid or ask	| Type of offer
| id	| INT	| eg. 918872936
| key	| STRING	| eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>


##Bulk offers cancel

```json
{
        "success": true,
        "code": "5059",
        "message": "Orders has been canceled"
}
```
 This endpoint allow you to bulkoffers cancel.
 
###HTTP Request
`GET https://api.bitclude.com/`
 
###Query Parameters
|Parameter | Value | Description
|--|--|--|
|method | transaction | Read from account
| action | canceloffers | Confirm
| bid | ARRAY | Offers ID, eg. ["1053","1054"]
| ask | ARRAY | Offers ID, eg. ["1055","1056"]
| id | INT | eg. 918872936
| key | STRING | eg. '54a44eb00b63f4d1cdde9...'

<aside class="notice">
<code>id</code> and <code>key</code> can be generated in <code>https://panel.bitclude.com</code>
</aside>

#WebSocket feed
The websocket feed delivers real-time market data updates for orders, trades, status and tickers.

`wss://n1.ws.bitclude.com`

###Description
Real-time market data updates provide the fastest insight into order flow and trades. This however means that you are responsible for reading the message stream and using the message relevant for your needs which can include building real-time order books or tracking real-time trades.
The websocket feed is publicly available.

##Subscribe and unsubscribe

>Example

```json
      {
          op: "subscribe", 
          headers: {id: "39013", token: "54a44eb00b63f4d1cdde9..."}, 
          args: ["all"]
      }      
      
      {
          op: "subscribe",
          headers: {id: "39013", token: "54a44eb00b63f4d1cdde9..."}, 
          args: [ 
             "trades:BTC_USD" , 
              "orderbooks:BTC_USD", 
              "balances:BTC", 
              "balances:USD", 
              "connected:all", 
              "tickers:all"
          ],
      }
```

Selection of the query option `op` 

###Connect


To start receiving fed messages, you must first send a `subscribe` message to the server indicating which arguments do you want to receive.

```json
       {
          op: "unsubscribe",
          headers: {id: "39013", token: "54a44eb00b63f4d1cdde9..."}, 
          args: [ 
             "trades:BTC_USD" , 
              "orderbooks:BTC_USD", 
              "connected:all", 
              "tickers:all"
          ]
        }
```

###Disconnect



When you want to stop receiving information from some of the arguments, send an `unsubscribe` message. The structure is similar to `subscribe` messages.




##Headers

```json
      {
          op: "subscribe", 
          headers: {id: "39013", token: "54a44eb00b63f4d1cdde9..."}, 
          args: ["all"]
      }
```

For `headers` we can specify the following parameters:

|Parameter | Type | Description
|--|--|--|
|id| INT | eg. 71834
|token| STRING | eg .54a44eb00b639...
 
##Arguments

For `args` we can specify the fallowing parameters:       

 
```json
   { action: "trade", symbol: "BTC_USD", size: "0.00230000", price: "1932.00", side: "Buy" }
``` 


**TRADES**<br>
  eg. trades:BTC_USD<br>
  alt. trades:all<br>
           
```json
   { action: "orderbook", symbol: "BTC_USD", size: "0.00230000", price: "1932.00", side: "bid" }
```
   
**ORDERBOOKS**<br>
            eg. orderbooks:BTC_USD<br>
            alt. orderbooks:all<br>
          
```json
   { action: "connected", connected: 99, time: 1555327761477, telemtric: { last_server: 43, last_user: 32423} }
```
**CONNECTED**<br>
            eg. connected<br><br>


```json
   { action: "ticker", symbol: "BTC_USD", last: "1932.00", volume: "0.32400000", change: "- 2.00%" }
```
**TICKERS**<br>
             eg. tickers:BTC_USD<br>
             alt. tickers:all<br>

```json
   { action: "execution", symbol: "BTC_USD", size: "0.00230000", price: "1932.00", side: "Buy" }
```
**EXECUTIONS**<br>
            eg. executions:BTC<br><br>
                 
```json
   { action: "balance", symbol: "BTC", value: {active: "0.00032333", inactive: "0.232333333"}}
```
**BALANCES**<br>
             eg. balances:BTC<br>
             alt. balances:all<br>

```json
   { action: order, symbol: "BTC_USD", prop: "new", price: "19203.32", size: "0.00012333", slide: "ask", id: 999}
   { action: order, symbol: "BTC_USD", prop: "remove", price: "19203.32", size: "0.00012333", slide: "ask", id: 999}
   { action: order, symbol: "BTC_USD", prop: "change", price: "19203.32", size: "0.00001000", slide: "ask", id: 999}
```
**ORDERS**<br>
             eg. orders:BTC_USD<br>
             alt. orders:all<br><br>
                    
```json
   { action: deposit, symbol: "BTC", size: "0.01432432"}
   { action: withdrawal, symbol: "BTC", size: "0.01432432"}
```

**WALLETS**<br>
            eg wallets:BTC<br>
            alt. wallets:all<br>

<aside class="warning">
For <b>private</b> (executions,balances,orders,wallets) args you need <code>id</code> and <code>token</code>
</aside>
        