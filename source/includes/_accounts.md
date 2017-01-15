# Accounts

## Signup

<table><tbody><tr><td>Base URL</td><td>/api/v1/accounts/signup</td>
</tr><tr><td>Method</td><td>POST</td></tr></table>

> Successful registration response body

```json
{
  "version": 1,
  "response": {
    "user": {
      "email": "tommy2@tripisco.com",
      "name": "PT. Tripisco"
    }
  }
}
```

Parameters:

Name | Type | Required | Description
---- | ----- | ----- | -----
merchant_name | String | Y | Name of the agent
merchant_phone | String | Y | Phone of the agent
merchant_address | String | Y | Physical address of the agent
user_email | String | Y | Email address of the agent, used for login
password | String | Y | Password used for logging into the system

All the fields above have to be sent, or otherwise a `WRGINP` error be raised.
If a user with the same email is found, a `DUPDAT` error will be raised.
Else, registration must be successful.

## Login

<table><tbody><tr><td>Base URL</td><td>/api/v1/accounts/login</td>
</tr><tr><td>Method</td><td>POST</td></tr></table>

Parameters:

Name | Type | Required | Description
---- | ----- | ----- | -----
email | String | Y | Email of the user intending to sign in
password | String | Y | Password of the user intending to sign in

> Successful login response

```json
{
  "version": 1,
  "response": {
    "email": "adam@tripisco.com",
    "token": "15ad7047-31f5-4fdd-9df1-4f6df9321948"
  }
}
```

Name | Type | Required | Description
---- | ----- | ----- | -----
email | String | Y | The email for which the token is generated
password | String | Y | The generated token to identify the user’s session

## Logout

<table><tbody><tr><td>Base URL</td><td>/api/v1/accounts/logout</td>
</tr><tr><td>Method</td><td>DELETE</td></tr></table>

Parameters:

Name | Type | Required | Description
---- | ----- | ------- | ------
token | String | Y | The token that get generated after the user is signed in

Successful response is a JSON document containing:

Field name | Type | Description
---------- | ----- | ------
`inactive` | Boolean | Indicating if the user should already be inactive/logged out
