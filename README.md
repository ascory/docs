# Ascory API documentation
This documentation will help in mastering the basic API for working with Ascory
# Getting started
Almost any interaction with the API requires specifying a store ID and hash. 

All requests to the API must be sent as a POST request.

If the request is successful, the server returns an array where the "code" element is assigned the value 200 and the "data" element is assigned the information you required from the API.

Example:
```json
{
    "code": 200,
    "data": "OK"
}
```

```json
{
    "code": 400,
    "data": {
        "ru": "Пример сообщения об ошибке.",
        "en": "Example error message."
    }
}
```

# API Features
## Item
### Create item
```bash
curl -X POST https://api.ascory.com/v1/item/create \
-H "accept: application/json" \
-d '{
    "shop": 1,
    "hash": "$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS",
    "name": "Apple",
    "description": "Delicious Apple",
    "amount": 0.5
}'
```
```json
{
    "code": 200,
    "data": {
        "id": 1,
        "shop": 1,
        "name": "Apple",
        "description": "Delicious Apple",
        "amount": 0.5
    }
}
```
### Check item
```bash
curl -X POST https://api.ascory.com/v1/item/check \
-H "accept: application/json" \
-d '{
    "shop": 1,
    "hash": "$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS",
    "id": 1
}'
```
```json
{
    "code": 200,
    "data": {
        "id": 1,
        "shop": 1,
        "name": "Apple",
        "description": "Delicious Apple",
        "amount": 0.5
    }
}
```
### Delete item
```bash
curl -X POST https://api.ascory.com/v1/item/delete \
-H "accept: application/json" \
-d '{
    "shop": 1,
    "hash": "$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS",
    "id": 1
}'
```
```json
{
    "code": 200,
    "data": {
        "id": 1,
        "shop": 1,
        "name": "Apple",
        "description": "Delicious Apple",
        "amount": 0.5
    }
}
```
### Edit item
```bash
curl -X POST https://api.ascory.com/v1/item/edit \
-H "accept: application/json" \
-d '{
    "shop": 1,
    "hash": "$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS",
    "name": "Pineapple",
    "description": "Very tasty apple, ah, oops, pineapple",
    "amount": 0.6
}'
```
```json
{
    "code": 200,
    "data": {
        "id": 1,
        "shop": 1,
        "name": "Pineapple",
        "description": "Very tasty apple, ah, oops, pineapple",
        "amount": 0.6
    }
}
```
### All items
```bash
curl -X POST https://api.ascory.com/v1/item/all \
-H "accept: application/json" \
-d '{
    "shop": 1,
    "hash": "$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS"
}'
```
```json
{
    "code": 200,
    "data": {
        "count": 1,
        "items": [
            {
                "id": 1,
                "shop": 1,
                "name": "Pineapple",
                "description": "Very tasty apple, ah, oops, pineapple",
                "amount": 0.6
            }
        ]
    }
}
```
## Invoice
### Create invoice
```bash
curl -X POST https://api.ascory.com/v1/invoice/create \
-H "accept: application/json" \
-d '{
    "shop": 1,
    "hash": "$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS",
    "item": 1,
    "comment": "It'\''s time to pay for apple-pineapple",
    "backURL": "https://ananasoshop.com/shopping-cart",
    "successURL": "https://ananasoshop.com/shopping-cart?event=success",
    "failURL": "https://ananasoshop.com/shopping-cart?event=fail"
}'
```
```json
{
    "code": 200,
    "data": {
        "id": 1,
        "shop": 1,
        "item": 1,
        "comment": "It's time to pay for apple-pineapple",
        "backURL": "https://ananasoshop.com/shopping-cart",
        "successURL": "https://ananasoshop.com/shopping-cart?event=success",
        "failURL": "https://ananasoshop.com/shopping-cart?event=fail",
        "time": 1722793426,
        "hash": "$2a$12$mSD6cinEXuGikQPiOhGn.O5VterRiPQldN9jipmYZN6opJqPAXTF",
        "url": "https://pay.ascory.com/?id=7&hash=$2a$12$mSD6cinEXuGikQPiOhGn.O5VterRiPQldN9jipmYZN6opJqPAXTF"
    }
}
```
### Check invoice
```bash
curl -X POST https://api.ascory.com/v1/invoice/check \
-H "accept: application/json" \
-d '{
    "shop": 1,
    "hash": "$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS",
    "id": 1
}'
```
```json
{
    "code": 200,
    "data": {
        "id": 1,
        "shop": 1,
        "item": 1,
        "comment": "It's time to pay for apple-pineapple",
        "backURL": "https://ananasoshop.com/shopping-cart",
        "successURL": "https://ananasoshop.com/shopping-cart?event=success",
        "failURL": "https://ananasoshop.com/shopping-cart?event=fail",
        "time": 1722793426,
        "hash": "$2a$12$mSD6cinEXuGikQPiOhGn.O5VterRiPQldN9jipmYZN6opJqPAXTF",
        "url": "https://pay.ascory.com/?id=7&hash=$2a$12$mSD6cinEXuGikQPiOhGn.O5VterRiPQldN9jipmYZN6opJqPAXTF"
    }
}
```
### All invoices
```bash
curl -X POST https://api.ascory.com/v1/invoice/all \
-H "accept: application/json" \
-d '{
    "shop": 1,
    "hash": "$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS"
}'
```
```json
{
    "code": 200,
    "data": {
        "count": 1,
        "invoices": [
            {
                "id": 1,
                "shop": 1,
                "item": 1,
                "comment": "It's time to pay for apple-pineapple",
                "backURL": "https://ananasoshop.com/shopping-cart",
                "successURL": "https://ananasoshop.com/shopping-cart?event=success",
                "failURL": "https://ananasoshop.com/shopping-cart?event=fail",
                "time": 1722793426,
                "hash": "$2a$12$mSD6cinEXuGikQPiOhGn.O5VterRiPQldN9jipmYZN6opJqPAXTF",
                "url": "https://pay.ascory.com/?id=7&hash=$2a$12$mSD6cinEXuGikQPiOhGn.O5VterRiPQldN9jipmYZN6opJqPAXTF"
            }
        ]
    }
}
```
## Payment
### Payment detail
```bash
curl -X POST https://api.ascory.com/v1/payment/detail \
-H "accept: application/json" \
-d '{
    "id": 1,
    "hash": "$2a$12$mSD6cinEXuGikQPiOhGn.O5VterRiPQldN9jipmYZN6opJqPAXTF2"
}'
```
```json
{
    "code": 200,
    "data": {
        "amount": {
            "USD": 0.1,
            "RUB": 10,
            "EUR": 0.09,
            "CNY": 0.73
        },
        "backURL": "https://client.apexnodes.xyz",
        "methods": [
            {
                "name": {
                    "ru": "Bitcoin (BTC)",
                    "en": "Bitcoin (BTC)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/bitcoin.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            },
            {
                "name": {
                    "ru": "Ethereum (ETH)",
                    "en": "Ethereum (ETH)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/ethereum.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            },
            {
                "name": {
                    "ru": "Tether (USDT)",
                    "en": "Tether (USDT)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/usdt.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            },
            {
                "name": {
                    "ru": "Toncoin (TON)",
                    "en": "Toncoin (TON)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/ton.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            },
            {
                "name": {
                    "ru": "Notcoin (NOT)",
                    "en": "Notcoin (NOT)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/not.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            },
            {
                "name": {
                    "ru": "Gram (GRAM)",
                    "en": "Gram (GRAM)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/gram.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            },
            {
                "name": {
                    "ru": "MyTonWallet (MY)",
                    "en": "MyTonWallet (MY)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/my.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            },
            {
                "name": {
                    "ru": "Litecoin (LTC)",
                    "en": "Litecoin (LTC)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/litecoin.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            },
            {
                "name": {
                    "ru": "Binance Coin (BNB)",
                    "en": "Binance Coin (BNB)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/bnb.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            },
            {
                "name": {
                    "ru": "TRON (TRX)",
                    "en": "TRON (TRX)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/tron.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            },
            {
                "name": {
                    "ru": "USD Coin (USDC)",
                    "en": "USD Coin (USDC)"
                },
                "method": "cryptobot",
                "url": "https://cdn.ascory.com/pay/images/usdc.png",
                "amount": {
                    "USD": 0.1,
                    "RUB": 8.83,
                    "EUR": 0.09,
                    "CNY": 0.74
                },
                "comission": 3
            }
        ]
    }
}
```
### Confirm payment
```bash
curl -X POST https://api.ascory.com/v1/payment/confirm \
-H "accept: application/json" \
-d '{
    "id": 1,
    "hash": "$2a$12$mSD6cinEXuGikQPiOhGn.O5VterRiPQldN9jipmYZN6opJqPAXTF2",
    "email": "cowwithananas@gmail.com",
    "method": "cryptobot"
}'
```
```json
{
    "code": 200,
    "data": "https://t.me/CryptoBot?start=poiuytrewq"
}
```
## Shop
### Balance
```bash
curl -X POST https://api.ascory.com/v1/shop/balance \
-H "accept: application/json" \
-d '{
    "shop": 1,
    "hash": "$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS"
}'
```
```json
{
    "code": 200,
    "data": {
        "amount": 1,
        "hold": 0,
        "history": [
            {
                "id": 1,
                "amount": 1,
                "time": 1722854524
            }
        ]
    }
}
```
## Commissions and tariffs
### All tariffs
```bash
curl -X POST https://api.ascory.com/v1/commission/all \
-H "accept: application/json"
```
```json
{
    "code": 200,
    "data": {
        "count": 5,
        "commissions": [
            {
                "id": "1",
                "amount": "0",
                "ru": "NULLED",
                "en": "NULLED",
                "cryptobot": "3",
                "operation": "0",
                "max": "0"
            },
            {
                "id": "2",
                "amount": "0",
                "ru": "Старт",
                "en": "Start",
                "cryptobot": "10",
                "operation": "50",
                "max": "500"
            },
            {
                "id": "3",
                "amount": "9.99",
                "ru": "Поток",
                "en": "Flow",
                "cryptobot": "5",
                "operation": "100",
                "max": "1000"
            },
            {
                "id": "4",
                "amount": "99.99",
                "ru": "Максимум",
                "en": "Maximum",
                "cryptobot": "3",
                "operation": "1000",
                "max": "10000"
            },
            {
                "id": "5",
                "amount": "999.99",
                "ru": "Глобус",
                "en": "Globe",
                "cryptobot": "3",
                "operation": "1000000000000",
                "max": "1000000000000"
            }
        ]
    }
}
```
## Currency rate
### All currencies
```bash
curl -X POST https://api.ascory.com/v1/currency/all \
-H "accept: application/json"
```
```json
{
    "code": 200,
    "data": {
        "USD": 1,
        "RUB": 85.7,
        "EUR": 0.92,
        "CNY": 7.16,
        "UAH": 41
    }
}
```
## Webhooks
### Check webhooks
```bash
curl -X POST https://api.ascory.com/v1/webhook/check \
-H "accept: application/json" \
-d '{
    "shop": 1,
    "hash": "$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS"
}'
```
```json
{
    "code": 200,
    "data": [
        {
            "id": 1,
            "data": {
                "id": 1,
                "item": 1,
                "amount": 0.6,
                "email": "cowwithananas@gmail.com",
                "comment": "It's time to pay for apple-pineapple",
                "type": "success"
            },
            "hash": "NO-INFO"
        }
    ]
}
```

# Webhook alerts
We send a payment status change notification to your webhook server.
> [!WARNING]
> Webhook alerts don't just come at the time of a successful payment. Please check the data->type element, which can take the following values: success, refund, fail.

> [!WARNING]
> Webhook notifications come from the following IP addresses: 193.222.99.133. Always check which IP address your webhook requests are being sent from, otherwise your site could be hacked. If you use protection (like Cloudflare), please whitelist these IP addresses.

Example:
```json
{
    "data": {
        "id": 1,
        "item": 1,
        "amount": 0.6,
        "email": "cowwithananas@gmail.com",
        "comment": "It's time to pay for apple-pineapple",
        "type": "success"
    }
}
