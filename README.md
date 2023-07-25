# paymob-code-wordpress

<img width="1161" alt="Screenshot 2023-06-23 at 10 32 13 AM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/52719dcd-39b5-4c8a-8525-e14846ee8720">

**File:** class-wc-checkout.php

**FilePath:** plugins/woocommerce/includes/class-wc-checkout.php

**Line #:** 438

**Code:**
```
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
```


<img width="1161" alt="Screenshot 2023-06-23 at 10 39 05 AM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/d69c5a2a-f2a5-4a33-8330-4d6533136cb9">

**File:** class-wc-checkout.php

**FilePath:** plugins/woocommerce/includes/class-wc-checkout.php

**Line #:** 959

**Code:**
```
    //installments custom code
    if($data['payment_method'] == 'accept-online-2'){
	if ( ! isset( $available_gateways['accept-online'] ) ) {
	    $errors->add( 'payment', __( 'Invalid payment method.', 'woocommerce' ) );
	} else {
	    if(!isset($_POST['installment-bank']) || !in_array($_POST['installment-bank'], ['Bank Alfalah', 'Faysal Bank'])){
		$errors->add( 'payment', __( 'Installment Bank Missing.', 'woocommerce' ) );
	    } else {
		if($_POST['installment-bank'] == 'Bank Alfalah' && (!isset($_POST['installment-cnic'])) || !$_POST['installment-cnic']){
		    $errors->add( 'payment', __( 'Installment Cnic Missing.', 'woocommerce' ) );
		}
	    }
	    if(!isset($_POST['installment-tenure']) || !in_array($_POST['installment-tenure'], ['3 Months', '6 Months', '9 Months', '12 Months'])){
		$errors->add( 'payment', __( 'Installment Tenure Missing.', 'woocommerce' ) );
	    }
	    $available_gateways['accept-online']->validate_fields();
	}
    } else {
	if (!isset($available_gateways[$data['payment_method']])) {
	    $errors->add('payment', __('Invalid payment method.', 'woocommerce'));
	} else {
	    $available_gateways[$data['payment_method']]->validate_fields();
	}
    }
    //installments custom code
```


<img width="1172" alt="Screenshot 2023-06-23 at 10 44 14 AM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/a08c28ad-624b-4c53-9074-bd682082b0cf">

**File:** class-wc-checkout.php

**FilePath:** plugins/woocommerce/includes/class-wc-checkout.php

**Line #:** 1309

**Code:**
```
    //installments custom code
    if($posted_data['payment_method'] == 'accept-online-2'){
	$this->process_order_payment( $order_id, 'accept-online' );
    } else {
	$this->process_order_payment($order_id, $posted_data['payment_method']);
    }
    //installments custom code
```


<img width="1172" alt="Screenshot 2023-06-23 at 10 46 52 AM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/1934128b-e61f-430c-88fe-e089fbc840df">

**File:** class-wc-ajax.php

**FilePath:** plugins/woocommerce/includes/class-wc-ajax.php

**Line #:** 331

**Code:**
```
//installments custom code
if($_POST['payment_method'] == 'accept-online-2'){
    WC()->session->set( 'chosen_payment_method', empty( 'accept-online' ) ? '' : wc_clean( wp_unslash( 'accept-online' ) ) );
}else {
    WC()->session->set('chosen_payment_method', empty($_POST['payment_method']) ? '' : wc_clean(wp_unslash($_POST['payment_method'])));
}
//installments custom code
```


<img width="1172" alt="Screenshot 2023-06-23 at 11 35 37 AM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/57c98e81-9807-4e49-a404-1099518e11c0">

**File:** class-wc-form-handler.php

**FilePath:** plugins/woocommerce/includes/class-wc-form-handler.php

**Line #:** 426, 437

**Code:**
```
//installments custom code
if($_POST['payment_method'] == 'accept-online-2'){
    $payment_method     = isset( $available_gateways[ 'accept-online' ] ) ? $available_gateways[ 'accept-online' ] : false;
}else {
    $payment_method = isset($available_gateways[$payment_method_id]) ? $available_gateways[$payment_method_id] : false;
}
//installments custom code
```
```
//installments custom code
if($_POST['payment_method'] == 'accept-online-2'){
    $order->set_payment_method('Installment (Credit Cards)');
}else {
    $order->set_payment_method($payment_method);
}
//installments custom code
```


<img width="1172" alt="Screenshot 2023-06-23 at 11 38 36 AM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/9246181b-79fc-464b-9e84-4aa375af3db8">

**File:** payment-method.php

**FilePath:** plugins/woocommerce/templates/checkout/payment-method.php

**Line #:** 31

**Code:**
```
    <?php if($gateway->id == 'accept-online-2') : ?>
	<div class="select-bank1">
	    <select class="form-control" style="margin: 10px 0;" name="installment-bank" required>
		<option value="">Select Bank</option>
		<option value="Bank Alfalah">Bank Alfalah</option>
	    </select>
	    <p>*Valid for credit card users only.</p>
	    <select class="form-control" style="margin: 10px 0;" name="installment-tenure" required>
		<option value="">Select Tenure</option>
		<option value="3 Months">3 Months</option>
		<option value="6 Months">6 Months</option>
		<option value="9 Months">9 Months</option>
		<option value="12 Months">12 Months</option>
	    </select>
	    <p>Bank Processing Fee: 3 Months: 5.5% + FED | 6 Months: 8% + FED | 9 Months: 10% + FED | 12 Months: 12% + FED</p>
	    <p style="color: red;">These charges will be shown one time in your credit cards's monthly statement.</p>
	    <div class="select-input"><label>Enter CNIC (Required by Bank)</label>
		<input autocomplete="off" type="text" name="installment-cnic">
	    </div>
	</div>
    <?php endif; ?>
```

<img width="1144" alt="Screenshot 2023-07-21 at 7 01 12 PM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/84a74d14-d890-445b-a759-28704e19c67f">

**File:** class-alg-wc-order-fees.php

**FilePath:** plugins/checkout-fees-for-woocommerce/includes/class-alg-wc-order-fees.php

**Line #:** 88

**Code:**
```
    if($payment_method == 'accept-online-2'){
	$payment_method = 'accept-online';
    }
```

<img width="1144" alt="Screenshot 2023-07-21 at 7 05 29 PM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/eb9438af-64a5-4cc2-bcfb-2895c735f118">

**File:** class-alg-wc-order-fees.php

**FilePath:** plugins/checkout-fees-for-woocommerce/includes/class-alg-wc-order-fees.php

**Line #:** 129

**Code:**
```
    if($payment_method == 'accept-online-2'){
	$payment_method = 'accept-online';
    }
```

<img width="1144" alt="Screenshot 2023-07-21 at 7 06 48 PM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/eb551096-30fc-4cb4-b1e9-7698e3e9d7af">

**File:** class-alg-wc-order-fees.php

**FilePath:** plugins/checkout-fees-for-woocommerce/includes/class-alg-wc-order-fees.php

**Line #:** 198

**Code:**
```
    if($payment_method == 'accept-online-2'){
	$payment_method = 'accept-online';
    }
```

<img width="1144" alt="Screenshot 2023-07-21 at 7 10 23 PM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/56cc9e21-f9d2-4e89-93ac-72fe010e4776">

**File:** class-alg-wc-checkout-fees.php

**FilePath:** plugins/checkout-fees-for-woocommerce/includes/class-alg-wc-checkout-fees.php

**Line #:** 401

**Code:**
```
    if($current_gateway == 'accept-online-2'){
	$current_gateway = 'accept-online';
    }
```
