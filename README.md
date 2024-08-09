# Ascory API documentation
This documentation will help in mastering the basic API for working with Ascory
## Getting started
Almost any interaction with the API requires specifying a store ID and hash. You can easily find out the store ID in the parameters of your store or from support. The hash must be generated by you personally. 

The hash is a BCrypt hashed string containing the first storage key, the second storage key, and the IP address of the server from which the request was sent. A ":" must be inserted between the data. Note that your server can send the request via IPv6.

Example:
```php
<?php
$id = 1;
$key1 = "c0a9cc6d8d4243c4a644f8e57d085438";
$key2 = "56d4f8ee1ee480707ee9f3210da5aca2";
$string = $id.":".$key1.":".$key2; # 1:c0a9cc6d8d4243c4a644f8e57d085438:56d4f8ee1ee480707ee9f3210da5aca2
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
## Webhook alerts
> [!WARNING]
> Webhook alerts don't just come at the time of a successful payment. Please check the data->type element, which can take the following values: success, refund, fail.
> [!WARNING]
> Webhook notifications come from the following IP addresses: 193.222.99.133
