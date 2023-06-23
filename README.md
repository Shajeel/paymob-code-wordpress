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


<img width="1172" alt="Screenshot 2023-06-23 at 11 25 18 AM" src="https://github.com/Shajeel/paymob-code-wordpress/assets/20224168/099c8aa8-293f-4ad1-95ee-b29e5963793d">

**File:** class-wc-form-handler.php

**FilePath:** plugins/woocommerce/includes/class-wc-form-handler.php

**Line #:** 426

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
