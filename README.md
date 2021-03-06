# angular-paypal-checkout
Angular 1.x directive for running PayPal's in-context checkout flow

![PayPal Checkout Button](https://www.paypalobjects.com/webstatic/en_US/i/buttons/checkout-logo-medium.png)

Demo here (need your server for it to go through flow): http://plnkr.co/edit/9kycqo2Dl879gQFoMdrP?p=preview

Your server should receive the client's request, communicate with PayPal, and return the `approval_url`.  For this directive, my server essentially does the following

    paypal.payment.createAsync dataObj
    .then (payment) ->
      approval_url = payment.links[1]
      res.send { href: approval_url.href }

But you can use a different format as needed.  The important thing is to **not** have the server redirect (as shown in PayPal docs), but simply return the url for the client to handle.

With that said, you can use the PayPal button like so:

    <paypal-checkout></paypal-checkout>

PayPal's docs aren't the best, but they may help with issues: https://developer.paypal.com/docs/classic/express-checkout/in-context/integration/
