## Listing bookings

<table><tbody><tr><td>Base URL</td><td>/api/v1/books/all</td>
</tr><tr><td>Method</td><td>GET</td></tr></table>

This listing endpoint allows you to retrieve all the booking requests
that you send to Tripisco. This API paginate the response, each page contains
10 booking records.

List of parameters:

Name | Type | Required | Description
---- | ---- | ---- | ---- |
user_token | String | Y | Token of the logged in user, if invalid an `INVCRED` error will be raised.
page | String | N | The page to be requested, index starts from 1. It raises `WRGINP` if the given value is less than 1.
status | String | N | Filtering by the status, raises a `WRGINP` if not one of the known status above.

### Listing bookings response

```json
{
  "version": 1,
  "response": {
    "page": 1,
    "total": 7,
    "has_next": false,
    "bookings": [
      {
        "agent": "A00052",
        "doer": "88FD5AE951",
        "ticket_email": "adam@tripisco.com",
        "type": "HOTEL",
        "booking": {
          "id": "BCB8C00",
          "status": "UNPAID"
        },
        "rate": {
          "currency": "IDR",
          "rate": "909993.0",
          "rate_cents": 90999300
        },
        "contact": {
          "first_name": "Dirga Pahlevi",
          "last_name": "Nusantara",
          "phone": {
            "hand": "085607071341",
            "home": "3953672"
          },
          "address": {
            "location": "Jalan Sagu",
            "city": "Gresik",
            "country_code": null,
            "postcode": "61151"
          }
        }
      }
    ]
  }
}
```

Field name | Type | Description
---------- | ---- | ------------
page | Integer | Indicate the current page
total | Integer | Number of all records
has_next | Boolean | Indicate if there is a next page that contains other records
bookings | Object | Data of booking, similar to the object returned when booking a hotel
