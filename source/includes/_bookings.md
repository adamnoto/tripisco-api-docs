# Bookings

Booking APIs allow you to do this list listing a user's booking records,
make payment for the user's booking, and so on.

A booking has a status either one of:

Status | Description |
------ | ------------|
UNPAID | The booking is not yet paid.
PAID | The booking is successfully paid.
RESERVED | Between paid and reserved. The room is paid, but the itinerary ticket is not yet made.
PENDING | Payment is made but the supplier has not acknowledge the booking request. 
CANCELLED | The booking is cancelled due to out of time, customer using fraudulent card, etc.
ERROR | There was an error performing the booking, unrecoverable. Very rare to happen.
