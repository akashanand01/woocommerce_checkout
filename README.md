// Register new status
function register_order_shipped_order_status() {
register_post_status( 'wc-order-shipped', array(
'label'                     => 'Order Shipped',
'public'                    => true,
'show_in_admin_status_list' => true,
'show_in_admin_all_list'    => true,
'exclude_from_search'       => false,
'label_count'               => _n_noop( 'Order Shipped (%s)', 'Order Shipped (%s)' )
) );
}
// Add custom status to order status list
function add_order_shipped_to_order_statuses( $order_statuses ) {
$new_order_statuses = array();
foreach ( $order_statuses as $key => $status ) {
$new_order_statuses[ $key ] = $status;
if ( 'wc-on-hold' === $key ) {
$new_order_statuses['wc-order-shipped'] = 'Order Shipped';
}
}
return $new_order_statuses;
}
add_action( 'init', 'register_order_shipped_order_status' );
add_filter( 'wc_order_statuses', 'add_order_shipped_to_order_statuses' );
