# Erratic responses

## List of erratic responses

Erratic response have a unique code for each error type, and is provided with
message given in English. You may want to substitute the message
to your local language if appropriate.

We will add support for Bahasa Indonesia in the future release.

code | meaning
---- | -------
INTERR | Type of error cannot be covered in detail by other error codes listed bellow; an internal error.
ERRKEY | You send an invalid `Authorization` header upon which no agent can be found.
INVCRED | The user's given email and password cannot be found.
OUTFAIL | Logout action cannot be performed due to an internal error, please retry.
NOANS | Search request yielded no results.
WRGDATE | Wrong inputs on the date, eg. search date is yesterday/day in the past.
MISPAR | Certain required parameter is missing from the request body.
