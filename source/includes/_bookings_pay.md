## Payment

<table><tbody><tr><td>Base URL</td><td>/api/v1/books/pay</td>
</tr><tr><td>Method</td><td>POST</td></tr></table>

Booking that is not paid within one hour will automatically have the status
updated to `CANCELLED`.

Possible payment methods are:

1. Credit card
2. Wallet (deposited money)

### Credit card payment

There are
