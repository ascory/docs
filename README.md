# Ascory API documentation
This documentation will help in mastering the basic API for working with Ascory
# Getting started
Almost any interaction with the API requires specifying a store ID and hash. You can easily find out the store ID in the parameters of your store or from support. The hash must be generated by you personally. 

The hash is a BCrypt hashed string containing the first storage key, the second storage key, and the IP address of the server from which the request was sent. A ":" must be inserted between the data. Note that your server can send the request via IPv6.

Example:
```php
<?php
$ip = "1.1.1.1";
$key1 = "c0a9cc6d8d4243c4a644f8e57d085438";
$key2 = "56d4f8ee1ee480707ee9f3210da5aca2";
$string = $key1.":".$key2.":".$ip; # c0a9cc6d8d4243c4a644f8e57d085438:56d4f8ee1ee480707ee9f3210da5aca2:1.1.1.1
$hash = password_hash($string, PASSWORD_BCRYPT); 
```

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
Contains a cost and brief information about yourself. Required to create an invoice.
### Create item
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/item/create");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "shop" => 1, # Shop ID
        "hash" => '$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS', # Generated API key
        "name" => "Apple", # Item name (5 to 30 characters)
        "description" => "Delicious Apple", # Item description (5 to 50 characters)
        "amount" => 0.5 # Item price in dollars (number to hundredths from 0.1 to 100)
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
        "name": "Apple",
        "description": "Delicious Apple",
        "amount": 0.5
    }
}
```
### Check item
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/item/check");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "shop" => 1, # Shop ID
        "hash" => '$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS', # Generated API key
        "id" => 1 # Item ID
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
        "name": "Apple",
        "description": "Delicious Apple",
        "amount": 0.5
    }
}
```
### Delete item
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/item/delete");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "shop" => 1, # Shop ID
        "hash" => '$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS', # Generated API key
        "id" => 1 # Item ID
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
        "name": "Apple",
        "description": "Delicious Apple",
        "amount": 0.5
    }
}
```
### Edit item
```php
<?php
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://api.ascory.com/v1/item/edit");
curl_setopt($ch, CURLOPT_HTTPHEADER, [
        "accept: application/json"
]);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
        "shop" => 1, # Shop ID
        "hash" => '$2a$12$XV0yN.1HFjuLawrEJLq3buF.rboZUW5jYw0N4Ckuz0lofy7A0wEaS', # Generated API key
        "name" => "Pineapple", # Optional: Item name (5 to 30 characters)
        "description" => "Very tasty apple, ah, oops, pineapple", # Optional: Item description (5 to 50 characters)
        "amount" => 0.6 # Optional: Item price in dollars (number to hundredths from 0.1 to 100)
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
            "hash": "$2y$10$Wi1j4wrgwrgwe884g5vw8bgvfewfwefweg/GG"
        }
    ]
}
```

# Webhook alerts
We send a payment status change notification to your webhook server.
> [!WARNING]
> Webhook alerts don't just come at the time of a successful payment. Please check the data->type element, which can take the following values: success, refund, fail.

> [!WARNING]
> Webhook notifications come from the following IP addresses: 193.222.99.133. If you use protection (like Cloudflare), please whitelist these IP addresses.

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
    },
    "hash": "$2y$10$Wi1j4wrgwrgwe884g5vw8bgvfewfwefweg/GG"
}
```

Keep in mind that the hash sent to your webhook server is not the hash for interacting with the API! A webhook hash is generated like this:
```php
<?php
$shopId = 1;
$key1 = "c0a9cc6d8d4243c4a644f8e57d085438";
$key2 = "56d4f8ee1ee480707ee9f3210da5aca2";
$data = $_REQUEST["data"];
$hash = $shopId.json_encode($data)..$key1.$key2;
```

"if hash = newHash" will not work for hash verification. This is because BCrypt returns different values each time. How to verify BCrypt hash check in the documentation of your programming language.

Example:
```php
<?php
$shopId = 1;
$key1 = "c0a9cc6d8d4243c4a644f8e57d085438";
$key2 = "56d4f8ee1ee480707ee9f3210da5aca2";
$data = $_REQUEST["data"];
$hash = $shopId.json_encode($data)..$key1.$key2;
if(!password_verify($hash, $_REQUEST["hash"])){
    die("Incorrect hash.");
}
```
