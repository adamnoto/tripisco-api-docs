# Accounts

## Login

Path: `/api/v1/accounts/login` (POST)

```json
{
  "email": "adam@tripisco.com",
  "password": "Password01"
}
```

Parameters:

Name | Type | Required | Description
---- | ----- | ----- | -----
`email` | String | Y | Email of the user intending to sign in
`password` | String | Y | Password of the user intending to sign in

Successful response is a JSON document containing:

```json
{
  "version": 1,
  "response": {
    "email": "adam@tripisco.com",
    "token": "15ad7047-31f5-4fdd-9df1-4f6df9321948"
  }
}
```

Field name | Type | Description
---------- | ----- | ------
`email` | String | The email for which the token is generated
`token` | String | The generated token to identify the user's session

## Logout

Path: `/api/v1/accounts/logout` (DELETE)

Parameters:

Name | Type | Required | Description
---- | ----- | ------- | ------
`token` | String | Y | Token generated after the user signed in

Successful response is a JSON document containing:

Field name | Type | Description
---------- | ----- | ------
`inactive` | String | Indicating if the user should already be inactive/logged out

