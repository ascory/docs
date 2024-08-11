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
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/item/all");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "shop" => 1, # Shop ID
        "hash" => '$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS', # Generated API key
]));
$response = curl_exec($ch);
?>
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
Ready to accept money? You will need to create an invoice.
### Create invoice
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/invoice/create");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "shop" => 1, # Shop ID
        "hash" => '$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS', # Generated API key
        "item" => 1, # Item ID
        "comment", => "It's time to pay for apple-pineapple", # Optional: Invoice comment (5 to 50 characters)
        "backURL" => "https://ananasoshop.com/shopping-cart", # Optional: Backlink to your site
        "successURL" => "https://ananasoshop.com/shopping-cart?event=success", # Optional: Backlink to your website in case of successful payment
        "failURL" => "https://ananasoshop.com/shopping-cart?event=fail" # Optional: Backlink to your site in case of unsuccessful payment
]));
$response = curl_exec($ch);
?>
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
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/invoice/check");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "shop" => 1, # Shop ID
        "hash" => '$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS', # Generated API key
        "id" => 1 # Invoice ID
]));
$response = curl_exec($ch);
?>
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
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/invoice/all");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "shop" => 1, # Shop ID
        "hash" => '$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS', # Generated API key
]));
$response = curl_exec($ch);
?>
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
This part of the API allows you to customize the payment method selection window. Normal users don't need this at all, as this API is used by pay.ascory.com by default for them.
### Payment detail
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/payment/detail");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "id" => 1, # Invoice ID
        "hash" => '$2a$12$mSD6cinEXuGikQPiOhGn.O5VterRiPQldN9jipmYZN6opJqPAXTF2' # Hash of invoice reference
]));
$response = curl_exec($ch);
?>
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
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/payment/confirm");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "id" => 1, # Invoice ID
        "hash" => '$2a$12$mSD6cinEXuGikQPiOhGn.O5VterRiPQldN9jipmYZN6opJqPAXTF2' # Hash of invoice reference
        "email" => "cowwithananas@gmail.com", # Email of the person making the payment
        "method" => "cryptobot" # Method passed in the payment information
]));
$response = curl_exec($ch);
?>
```
```json
{
    "code": 200,
    "data": "https://t.me/CryptoBot?start=poiuytrewq"
}
```
## Shop
Shop management using API keys
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
View Ascory commissions and tariffs
### All tariffs
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/commission/all");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([]));
$response = curl_exec($ch);
?>
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
Ascory service exchange rate pegged to the dollar
### All currencies
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/currency/all");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([]));
$response = curl_exec($ch);
?>
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
Manual reading of webhooks through API keys
### Check webhooks
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/webhook/check");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "shop" => 1, # Shop ID
        "hash" => '$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS', # Generated API key
]));
$response = curl_exec($ch);
?>
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
