## Search request

<table><tbody><tr><td>Base URL</td><td>/api/v1/hotels/search</td>
</tr><tr><td>Method</td><td>GET</td></tr></table>

Search parameters:

Name | Type | Required | Description
---- | ---- | ---- | ---- |
sorter | String | Y | Ordering of the return, currently only support `BUDGET`.
arrival_date | String | Y | Date of checkin
departure_date | String | Y | Date of checkout
city | String | Y | Name of the city
name | String | N | Name of the hotel
min_rating | Integer | Y | Minimal quality of hotels in the range of 1 to 5
max_rating | Integer | Y | Maximal quality of hotels in the range of 1 to 5
adults_count | Integer | Y | Number of adults occupying the room
children_count | Integer | N | Number of children occupying the room

### Search with children

When there are children (more than 0), age must be submitted in the format of
`child_age_n` whereby n is the index of the children ages.

Supposed that there are two children, then additional data must be
supplied as follow.

Name | Type | Required | Description
---- | ---- | ---- | ---- |
child_age_0 | Integer | Y | Age of the first children
child_age_1 | Integer | Y | Age of the second children

### Response

> Response with hotel results

```json
{
  "version": 1,
  "response": {
    "type": "HOTEL_SEARCH_RESULTS",
    "data": {
      "count": 1,
      "results": [{}],
      "sorter": [""],
      "session_id": "some-data",
      "amenities": [""]
    }
  }
}
```

If the hotel search can be performed without further clarification, a JSON object
with `response.type` key is set to `HOTEL_SEARCH_RESULTS`.

If a location clarification is needed to avoid ambiguities,
a document with `response.type` set to `HOTEL_ALTERNATIVE_LOCATIONS` is returned.

Response body:

Field name | Type | Description
---------- | ----- | ------
type | String | Type of documents returned, either `HOTEL_SEARCH_RESULTS` or `HOTEL_ALTERNATIVE_LOCATIONS`
data | Object | The result document
data.count | Integer | Number of hotels
data.results | Object[] | Each individual Hotel object
data.sorter | String[] | The available sorter
data.session_id | String | Use this for subsequent detail request and booking attempt.
data.amenities | String[] | Array of String of all possible amenities for filtering the hotel result

### Success response

On success response, Tripisco will return list of hotels inside `results` array
within `response.data`.

> Example of result data

```json
{
    "id": 572068,
    "view_url": "...",
    "thumbnail_url": "...",
    "name": "My Studio Hotel Surabaya - Backpacker",
    "location": "Jln. Sumatra 20 C Surabaya",
    "city": "Surabaya",
    "rating": 1,
    "value_adds": [],
    "amenities": [
      "Restaurant",
      "Breakfast",
      "Parking",
      "Free Parking"
    ],
    "rate": {
      "undiscounted": "Rp 131.900,00",
      "current": "Rp 99.173,00"
    },
    "small_allotment": false,
    "current_allotment": 29
}
```

Each of the `result` element from a given document consists of the following fields:

Field name | Type | Description
---------- | ----- | ------
id| String | Hotel ID
view_url | String | URL address of displaying this hotel in Tripisco's dashboard
thumbnail_url | String | URL for the image to be used as thumbnail
name | String | Name of the hotel
location | String | Address where the hotel can be found
city | String | City of the location
rating | String | Star rating scaling from 1 to 5
value_adds | String | Any value added from booking this hotel
amenities | String | Facilities at hotel's premise
rate.undiscounted | String | Original price
rate.current | String | Original price after discount, which is the final price
small_allotment | Boolean | Indication of limited offering
current_allotment | Integer | Number of free allotment

See the body response in detail at the section for the detail request.

### Search returning various locations

> Response asking location clarifications

```json
{
  "version": 1,
  "response": {
    "type": "HOTEL_ALTERNATIVE_LOCATIONS",
    "data": [
      {
        "id": "0275996B-B8AA-46AE-B1CA-DD4690FFAF0D",
        "city": "Kota",
        "country": "India"
      },
      {
        "id": "FE39D864-50E1-4CE4-84D4-D8FB1BB04801",
        "city": "Kota",
        "country": "Japan"
      }
    ]
  }
}
```

User may input ambiguous location name. On which,
Tripisco API will return a `HOTEL_ALTERNATIVE_LOCATIONS` response type
where implementer needs to display something for the user to select from,
to clarify the location he wanted to search.

The `data` body of `HOTEL_ALTERNATIVE_LOCATIONS` consist of the following fields:

Field name | Type | Description
---------- | ----- | ------
id | String | Location ID, use this to search next rather than user's provided input
city | String | The city name
country | String | Country name where the city is located
