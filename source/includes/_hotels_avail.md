## Availability request

Call the availability request when displaying the booking form in your app,
It helps ensure the room availability as well as locking the price from
fluctuating.

<table><tbody><tr><td>Base URL</td><td>/api/v1/hotels/available</td>
</tr><tr><td>Method</td><td>GET</td></tr></table>

Data from this call have to be displayed on the booking form. Those
data are:

- Hotel name, and its location
- The check-in and check-out date
- Rate name
- Bed type
- Detail of the rates per night
- Total of nightly rates
- Detail of the surcharges
- Total of surcharge
- Detail of additional hotel fees
- Total of hotel fees
- All total chargeable rate
- Indication if refundable
- Indication if require deposit
- The guest detail (minimum age, how many adults and children)

Availability request parameters:

Name | Type | Required | Description
---- | ----- | ----- | -----
storage_id | String | Y | Storage ID help ensure the request body is not tempered
room_bed_type | String | Y | Type of the bed, from the key associated to `bed_types`
rate_code | String | Y | Rate code of the room in question, from field 'rate.code’
room_type_code | String | Y | Type code of the room in question, from field `type_code`

All of the parameters needed above is available since the detail request.

### Availability response

> Hotel availability response

```json
{
  "version": 1,
  "response": {
    "bed_type_id": "13",
    "bed_type_description": "1 double",
    "hotel": {
      "id": "572068",
      "name": "My Studio Hotel Surabaya - Backpacker",
      "location": {
        "address1": "Jln. Sumatra 20 C",
        "city": "Surabaya",
        "country_code": "ID"
      }
    },
    "date": {
      "arrival": "02/02/2017",
      "departure": "02/09/2017",
      "arrival_text": "Thu, 02 Feb 2017",
      "departure_text": "Thu, 09 Feb 2017"
    },
    "rate": {
      "name": "Asrama Umum, 1 tempat tidur double",
      "currency_code": "IDR",
      "nightly_rate_total": 1157016,
      "nightly_rates": [
        165288,
        165288,
        165288,
        165288,
        165288,
        165288,
        165288
      ],
      "nightly_dates": [
        "February  2, 2017",
        "February  3, 2017",
        "February  4, 2017",
        "February  5, 2017",
        "February  6, 2017",
        "February  7, 2017",
        "February  8, 2017"
      ],
      "refundable": true,
      "require_deposit": true,
      "require_guarantee": false,
      "surcharge_total": 242977,
      "surcharges": [
        {
          "caption": "Tax Recovery Charges and Service Fees",
          "amount": "242977.00"
        }
      ],
      "hotel_fees": [],
      "hotel_fees_total": 0,
      "total": 1399993
    },
    "guest": {
      "min_age": 0,
      "adults_count": 2,
      "children_count": 0,
      "children_ages": []
    }
  }
}
```

Hotel availability may raise `NOTAVL` error if the hotel being checked is no
longer offering room. `NOTAVL` can also occur if you send an old/outdated request.
Otherwise, a success response is given.

Field name | Type | Description
---------- | ---- | ------------
bed_type_id | String | ID of the bed selection
bed_type_description | String | Bed name
hotel | Object | Hotel object with minimal, essential data
date | Object | The date object
rate | Object | The rate object
guest | Object | The guest object

### `rate` object

Field name | Type | Description
---------- | ---- | ------------
name | String | The room name
currency_code | String | ISO-4217 code to represent the currency the amount is represented
nightly_rate_total | Double | Summary of rate per night, without tax
nightly_rates | Double[] | Array of rates per night since check-in to the day before check-out
nightly_dates | String[] | Date of each chargable nightly rate
refundable | Boolean | Indicating if the booking can be refunded
require_deposit | Boolean | Indicating if deposit at the hotel is needed upon check-in, and can be returned upon check-out according to the check-in terms
require_guarantee | Boolean | If the hotel will deduct amount when customer cannot check-in at the given time, or cancelling after the cancellation deadline
surcharge_total | Double | Total of all taxes and service related charges
surcharges | Object[] | Array with object to give detail of each charge
hotel_fees | Float[] | Detail of additional fees that will be charged upon check-in, the fees will not be part of the booking price
hotel_fees_total | Float | Total of hotel fees the customer will be charged upon check-in, the fees will not be part of the booking price
total | Float | Total amount of chargeable fee so that a booking itinerary can be made
