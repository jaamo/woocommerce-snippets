# WooCommerce Snippets

Random selection of WooCommerce snippets.

## Custom emails on status change

Trigger custom email when order status has changed.

```
add_action('woocommerce_order_status_changed', function ($order_id, $from_status, $to_status, $order) {

    if ($order->has_status( 'blocked' )) {

        // Getting all WC_emails objects
        $email_notifications = WC()->mailer()->get_emails();

        // Customize
        $email_notifications['WC_Email_Customer_Processing_Order']->heading = __('Your payment has been blocked', 'woocommerce');
        $email_notifications['WC_Email_Customer_Processing_Order']->subject = 'Your {site_title} processing Back order receipt from {order_date}';

        // Sending the customized email
        $email_notifications['WC_Email_Customer_Processing_Order']->trigger( $order_id );

    }

}, 10, 4);
```
