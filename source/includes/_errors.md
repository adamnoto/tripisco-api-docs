# Erratic responses

## List of erratic responses

Erratic response have a unique code for each error type, and is provided with
message given in English. You may want to substitute the message
to your local language if appropriate.

We will add support for Bahasa Indonesia in the future release.

code | meaning
---- | -------
BKGERR | Error in doing the booking request.
DUPDAT | Duplicate record attempted to be made, for instance: attempting to register the user, account with an already registered email address.
ERRKEY | You send an invalid `Authorization` header upon which no agent can be found.
INTERR | Type of error cannot be covered in detail by other error codes listed bellow; an internal error.
INVCRED | The user's given email and password cannot be found, or no authenticated user info can be found on API endpoint that requires `user_token`.
MISPAR | Certain required parameter is missing from the request body.
NOANS | Search request yielded no results.
NOTAVL | Hotel/room is not available for booking (sending old request?)
OUTFAIL | Logout action cannot be performed due to an internal error, please retry.
WRGDATE | Wrong inputs on the date, eg. search date is yesterday/day in the past.
WRGINP | General wrong inputs, please ensure all fields are filled correctly.
WRGSTS | Wrong status/inappropriate status. Eg. customer attempt to pay already paid booking.
