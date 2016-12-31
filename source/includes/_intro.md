# Tripisco API

[Tripisco](https://tripisco.com) is a business-to-business booking where you could get commissions
from each successful booking you made, uncancelled. This is the API that you
will use to connect to our app as a service.

All APIs served by Tripisco is protected behind an Authorization layer.
The Authorization layer make use of each agent's own agent ID and server key,
and then encoded in Base 64. If the agent ID is 'M000001' and the server key
is 'TCO-Server-12345678', the Authorization key is generated as follow:

1. Use basic format (`id:password`): `M000001:TCO-Server-12345678`.
2. Encode in base64 strictly: `TTAwMDAwMTpUQ08tU2VydmVyLTEyMzQ1Njc4`.
3. Embed the encoded id-password pair above in `Authorization` header in each request to the API: `Basic TTAwMDAwMTpUQ08tU2VydmVyLTEyMzQ1Njc4`.

## Response type

There are two types of response:

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

```json
{
  "version": 1,
  "error": {
    "code": "ERRKEY",
    "message": "Server key illegitimate"
  }
}
```

There is no way a response both having `error` and `response` body. Also, 
all response always contains the version ID of the called API.

## Postman collection

We provide a postman collection of API calls which you can experiment with and
incorporate to your app. [Here is the postman collection for you](https://www.getpostman.com/collections/1eb5f910985639fec5ab).
