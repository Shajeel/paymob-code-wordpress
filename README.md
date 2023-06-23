# paymob-code-wordpress

<img width="1161" alt="Screenshot 2023-06-23 at 10 32 13 AM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/52719dcd-39b5-4c8a-8525-e14846ee8720">

**File:** class-wc-checkout.php

**FilePath:** plugins/woocommerce/includes/class-wc-checkout.php
**Line #:** 438
**Code:**
//installments custom code
if($data['payment_method'] == 'accept-online-2'){
    $order->set_payment_method('Installment (Credit Cards)');
    $order->update_meta_data('installment_bank', $_POST['installment-bank']);
    $order->update_meta_data('installment_cnic', $_POST['installment-cnic']);
    $order->update_meta_data('installment_tenure', $_POST['installment-tenure']);
}else {
    $order->set_payment_method(isset($available_gateways[$data['payment_method']]) ? $available_gateways[$data['payment_method']] : $data['payment_method']);
}
//installments custom code

