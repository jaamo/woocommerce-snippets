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

## Allowed countries

Get list of allowed countries

```
$wc_countries = new WC_Countries();
$allowed_countries = $wc_countries->get_allowed_countries();
```

## Allowed countries

Use WooCommerce & MaxMind GeoIP database to locate customer

```
$geo_location = WC_Geolocation::geolocate_ip();
$country = $geo_location['country'];
```

## Get cart & customer from session

```
WC()->cart->get_customer()->set_shipping_country($country);
WC()->cart->get_customer();
```

## Get cart & customer from session

```
// WC_Order
$order = wc_get_order($order_id);
foreach ( $order->get_items() as $item_id => $item ) {
    // WC_Order_Item

    // $item->get_name()
    // $item->get_product_id()
    // $item->get_total()
    // $item->get_quantity()

}
```
