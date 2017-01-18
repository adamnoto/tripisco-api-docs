## Detail request

&nbsp; | &nbsp;
------ | ------
Base URL | api/v1/hotels/detail
Method | GET

This detail request API allows you to get more detail about the hotel in particular.

Detail request parameters:

Name | Type | Required | Description
---- | ---- | ---- | ---- |
arrival_date | String | Y | Date of checkin
departure_date | String | Y | Date of checkout
city | String | Y | Name of the city
session_id | String | Y | Session ID as returned since the search request
hotel_id | String | Y | Hotel ID which detail is requested

### Response

> Hotel detail response

```json
{
  "storage_id": "tsco88a_fa36ba5f-abcdef",
  "date": {
    "arrival": "02/02/2017",
    "departure": "02/09/2017",
    "arrivalText": "Thu, 02 Feb 2017",
    "departureText": "Thu, 09 Feb 2017"
  },
  "hotel": {
    "id": 572068,
    "view_url": null,
    "thumbnail_url": null,
    "name": "My Studio Hotel Surabaya - Backpacker",
    "location": "Jln. Sumatra 20 C",
    "city": "Surabaya",
    "rating": null,
    "value_adds": [],
    "amenities": [
      "Antar-jemput gratis ke kawasan sekitar",
      "Bar/lounge",
      "Wi-Fi gratis"
    ],
    "rate": {
      "undiscounted": null,
      "current": null
    },
    "small_allotment": null,
    "current_allotment": null,
    "description": "Hostel ini jaraknya ...",
    "checkin_instruction": "Ketahui Sebelum Anda ...",
    "check_in_time": "2:00 PM",
    "check_out_time": "12:00 PM",
    "area_info": [
      "Monumen Bambu Runcing - 0,6 km",
      "Balai Pemuda - 0,6 km",
      "Monumen Kapal Selam - 0,6 km"
    ],
    "images": [
      {
        "caption": "Featured Image",
        "url": "http://hotel.cdn.tripisco.com/...",
        "thumbnail_url": "http://hotel.cdn.tripisco.com/..."
      },
      {
        "caption": "Guestroom",
        "url": "http://hotel.cdn.tripisco.com/...",
        "thumbnail_url": "http://hotel.cdn.tripisco.com/..."
      },
    ],
    "rooms": [
      {
        "hotel_id": 572068,
        "name": "Asrama Umum, 1 tempat tidur single",
        "images": [
          "http://hotel.cdn.tripisco.com/...",
          "http://hotel.cdn.tripisco.com/...",
        ],
        "type_code": "201421658",
        "amenities": [
          "AC",
          "Air minum kemasan gratis",
          "Wi-Fi gratis"
        ],
        "rate": {
          "key": "eaef5b47-4a2b-4964-b6e0-9a6885d3f609-5212",
          "code": 207037461,
          "is_refundable": true,
          "require_guarantee": false,
          "require_deposit": true,
          "total": 840000,
          "currency": "IDR",
          "nightly": [
            99173,
            99173,
            99173,
            99173,
            99173,
            99173,
            99173
          ],
          "surcharge_total": 145789,
          "surcharges": [
            {
              "caption": "Tax Recovery Charges and Service Fees",
              "amount": "145789.00"
            }
          ]
        },
        "policy": {
          "cancellation": "Kami memahami ..."
        },
        "guest": {
          "min_age": 0,
          "adults_count": 1,
          "children_count": 0,
          "children_ages": []
        }
      }
    ]
  }
}
```

Field name | Type | Description
---------- | ----- | ------
storage_id | String | ID representing several data in Tripisco side, it must be send in subsequent request
date | Object | Date object
hotel | Object | Hotel object

### Hotel object

Hotel object have similar body with search request, but there are additional
fields as well. It is designed this way so that you would only have one `Hotel`
class at your side.

Those detail-only additional fields are:

Field name | Type | Description
---------- | ----- | ------
description | String | Description of the property
checkin_instruction | String | Instruction and regulation for checking into the property
check_in_time | String | Scheduled time of check-in
check_out_time | String | Scheduled time of check-out
area_info | String[] | Array of places of interest around the property
images | Object[] | Array of object for image consisting the URL, thumbnail and caption.
rooms | Object[] | Array of object representing each room available for booking

### Area info array

The area info is list of any places of interest nearby the hotel. It made of
string array.

### Image object

`images` data contains `image` object with the following fields:

Field name | Type | Description
---------- | ----- | ------
caption | String | Title of the image
url | String | URL of the full size of the image
thumbnail_url | String | A URL for the thumbnail version of the image

### Room object

`rooms` data contains `room` object with the following fields:

Field name | Type | Description
---------- | ----- | ------
hotel_id | String | The hotel ID of the room, must be the same with hotel ID of the hotel.
name | String | The room name
images | String[] | Array of images of the room
type_code | String | Code for the room
amenities | String[] | Facilities at the room
rate | Object | The rate object

### Rate object

`rate` object within `rooms` data contains the following fields:

Field name | Type | Description
---------- | ----- | ------
key | String | The key indicate parameters that leading to this rate
code | String | Indicating the whole rate code body
is_refundable | Boolean | Whether the customer later can ask for refund
require_guarantee | Boolean | Whether the customer will be charged for guarantee upon checking in
require_deposit | Boolean | Whether the customer will be charged for deposit fee upon checking in
total | Double | Total amount of money that will be charged
currency | String | The currency used for charging the customer
nightly | Double[] | Array of room rate per night stay, without tax
surcharge_total | Double | All additional charges
surcharges | Object[] | Detail of each surcharge
policy | Object | Contains `cancellation` field about the cancellation policy
guest | Object | Guest detail fields for the room
