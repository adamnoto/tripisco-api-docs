# Tripisco API

[Tripisco](https://tripisco.com) is a business-to-business booking where you could get commissions
from each successful booking you made, uncancelled.

This is the API documentation that will you to integrate and connect with our service.

## Access Authorization

All APIs served by Tripisco is protected behind an Authorization layer.

To get authorized, client will need to supply a basic authorization header
for each API call. The value for the header is generated as follow:

1. Make text in format `id:password`, for example: `A000001:TCO-Server-12345678`.
2. Encode in strict base64: `QTAwMDAwMTpUQ08tU2VydmVyLTEyMzQ1Njc4`.
3. Embed the encoded id-password pair above in the `Authorization` header: `Basic QTAwMDAwMTpUQ08tU2VydmVyLTEyMzQ1Njc4`.

The `id` represents your agent's ID, and the password is your server key. Both
can be obtained after you had registered with Tripisco.

## Response type

There are two types of response:

> Valid response body

```json
{
  "version": 1,
  "response": {
    "email": "adam@tripisco.com",
    "token": "f2fd1573-5309-4dc9-aa40-64620dca8bba"
  }
}
```

1. Valid response, which indicate there is no error in the server side and that the request is legitimate. It always has `response` body.
2. Erratic response, which indicate the request as being illegitimate or containing some error. It always has `error` body.

> Erratic response body

```json
{
  "version": 1,
  "error": {
    "code": "ERRKEY",
    "message": "Server key illegitimate"
  }
}
```

There is no way a response is both having an `error` and a `response` body. Also, 
all response always contain the version ID of the producing API.

## Postman collection

We provide a postman collection of API calls which you can experiment with and
incorporate to your app. [Here is the postman collection for you](https://www.getpostman.com/collections/1eb5f910985639fec5ab).
