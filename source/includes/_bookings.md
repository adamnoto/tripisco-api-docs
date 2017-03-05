# Bookings

Booking APIs allow you to do this list listing a user's booking records,
make payment for the user's booking, and so on.

A booking has a status either one of:

Status | Description |
------ | ------------|
UNPAID | The booking is not yet paid.
PAID | The booking is successfully paid, but no ticket is issued yet.
RESERVED | Booking is paid, and the ticket is already issued.
PENDING | Payment is made but the supplier has not acknowledge the booking request. 
CANCELLED | The booking is cancelled due to out of time, customer using fraudulent card, etc.
ERROR | There was an error performing the booking, unrecoverable. Very rare to happen.

The `PAID` status essentially waiting the hotel partner to acknowledge the booking.
It doesn't take a long time for the booking to be `RESERVED`. In fact,
most of the time the `PAID` status is unnoticable.
