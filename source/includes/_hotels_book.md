## Booking request

Calling this API will create a booking record at Tripisco. However,
the booking will have an `UNPAID` status. For making payment to the
booking, a call to the pay API is required.

<table><tbody><tr><td>Base URL</td><td>/api/v1/hotels/book</td>
</tr><tr><td>Method</td><td>POST</td></tr></table>

> Example of a booking request payload

```json
{
  "first_name": "Dirga Pahlevi",
  "last_name": "Nusantara",
  "hand_phone": "085607071341",
  "home_phone": "3953672",
  "address": "Jalan Sagu",
  "city": "Gresik",
  "postal_code": "61151",
  "ticket_email": "adam@tripisco.com",
  "storage_id": "tsco88a_cdcc34c0-5ac6-4baf-b066-a5d63437d325",
  "user_token": "782cd05c-80c8-4be4-afd7-c362773b028e"
}
```

Booking request parameters:

Name | Type | Required | Description
---- | ----- | ----- | -----
user_token | String | Y | Token of the logged in user, if invalid an `INVCRED` error will be raised.
first_name | String | Y | First/given name of the customer.
last_name | String | Y | Last/family name of the customer.
hand_phone | String | Y | The customer's mobile phone number. 
home_phone | String | Y | The customer's home phone number.
address | String | Y | The customer's home address.
country_code | String | N | [Alpha2](https://www.iso.org/obp/ui/#search) country code (eg. ID, KR).
province_code | String | N | Code for the province/subregion.
city | String | N | Name of the city of the customer's home address.
postal_code | String | Y | Postal code of the home address.
ticket_email | String | Y | Email address of which the itinerary ticket be sent to.
storage_id | String | Y | Storage ID as provided in the availability request.

### Hotel booking response

> Hotel booking response

```json
{
  "version": 1,
  "response": {
    "agent": "A00052",
    "doer": "88FD5AE951",
    "ticket_email": "adam@tripisco.com",
    "booking": {
      "id": "B453B32",
      "status": "UNPAID"
    },
    "rate": {
      "currency": "IDR",
      "rate": "1399993.0",
      "rate_cents": 139999300
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
}
```

Field name | Type | Description
---------- | ---- | ------------
agent | String | The agent's ID.
doer | String | ID of the user making the booking.
ticket_email | String | An email address to which the itinerary is expected to be delivered at.
booking | Object | A booking object, the `ID` must be kept in your side for future reference. The `status` will always evaluate to `UNPAID`.
rate | Object | A rate object.
contact | Object | A contact object for the customer

Upon hitting this API, the booking status will always evaluate to `UNPAID`.
If you hit this API for the second time, an `INTERR` will be raised.
