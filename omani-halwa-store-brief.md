# تكليف: إعداد متجر «حلوى السَّبلة» على ووردبريس + WooCommerce + Elementor Pro

## السياق

أنت تعمل داخل لوحة تحكم ووردبريس لمتجر إلكتروني يبيع **الحلوى العمانية** (سوق عُمان فقط).

- الرابط: `https://salmon-gull-492742.hostingersite.com/wp-admin/` (دومين مؤقت من هوستنجر)
- الاستضافة: Hostinger (سيرفر LiteSpeed)
- الإضافات المنصّبة: WooCommerce، Elementor، Elementor Pro، Code Snippets، Joinchat، LiteSpeed Cache
- القالب المطلوب: **Hello Elementor** (+ Hello Elementor Child إن أمكن)
- اللغة: العربية (RTL)
- الهوية: عمانية فاخرة (بني التمر، النحاس، ذهبي الخنجر، الزعفران، البيج)

## قواعد يجب الالتزام بها

1. **لا تستخدم** «إنشاء موقع باستخدام AI» الخاص بهوستنجر، ولا أي قالب جاهز يستبدل Elementor.
2. صفحات **السلة والدفع** يجب أن تكون **كلاسيكية** (شورتكود)، وليست مبنية ببلوكات ووكومرس. كود الـ PHP أدناه لا يعمل على بلوك Checkout.
3. **لا تفعّل** في LiteSpeed Cache أي خيار من Minify / Combine CSS/JS / Delay JS أثناء البناء.
4. لا تثبّت إضافات إضافية غير المذكورة دون الرجوع لصاحب المتجر.
5. بوابة الدفع الإلكترونية **ستُضاف لاحقاً** من صاحب المتجر، فلا تتعامل معها. فعّل فقط «الدفع عند الاستلام» للتجربة.
6. بعد كل قسم، تحقّق أن الموقع ما زال يعمل (افتح الواجهة الأمامية).

---

## المهمة 1: التنظيف والإعدادات العامة

- احذف المحتوى التجريبي: صفحة «Sample Page» ومقالة «Hello World».
- حدّث كل الإضافات التي عليها تحديث.
- **الإعدادات ← عام**: لغة الموقع **العربية**، المنطقة الزمنية **Muscat** (مسقط).
- **المظهر ← قوالب**: فعّل **Hello Elementor**.
- عطّل (لا تحذف) إضافات هوستنجر الخاصة بالذكاء الاصطناعي والـ Onboarding إن وُجدت. **أبقِ LiteSpeed Cache مفعّلة.**

## المهمة 2: إعدادات WooCommerce

**WooCommerce ← الإعدادات ← عام**
- Selling location(s): **Sell to specific countries ← Oman**
- Shipping location(s): **Ship to specific countries ← Oman**
- Currency: **Omani rial (OMR)**
- Number of decimals: **3**

**الإعدادات ← الضريبة**: فعّل الضرائب، وأضف في Standard rates: الدولة `OM`، النسبة `5`، الاسم `ضريبة القيمة المضافة`.

**الإعدادات ← الشحن**
- في الخيارات: فعّل **Force shipping to the customer billing address**.
- مناطق الشحن: تُنشأ **بعد** تفعيل كود المهمة 4 (لأنه يضيف المحافظات). أنشئ منطقة لكل مجموعة محافظات:
  - مسقط ← سعر ثابت (Flat rate)
  - باقي المحافظات ← سعر ثابت
  - ظفار ومسندم ← سعر ثابت أعلى
  - **اترك الأسعار صفراً مؤقتاً واسأل صاحب المتجر عن الأسعار الفعلية.**

**الإعدادات ← الحسابات والخصوصية**: فعّل **السماح للعملاء بالطلب دون حساب**.

**الإعدادات ← المدفوعات**: فعّل **الدفع عند الاستلام** فقط.

**الإعدادات ← متقدم**: تأكد أن صفحات السلة والدفع وحسابي معيّنة.
- صفحة **الدفع**: إن كانت مبنية ببلوك Checkout احذفه وضع الشورتكود `[woocommerce_checkout]`.
- صفحة **السلة**: نفس الشيء بالشورتكود `[woocommerce_cart]`.

## المهمة 3: الأقسام والمنتج التجريبي

**منتجات ← التصنيفات**، أنشئ:

| الاسم | الاسم اللطيف (slug) | الوصف المختصر |
|---|---|---|
| الحلوى السلطانية | `sultani-halwa` | حلوى بالزعفران والهيل وماء الورد والمكسرات الفاخرة |
| حلوى الأصالة | `traditional-halwa` | حلوى بالتمر والدبس والسكر الأحمر على الطريقة التقليدية |
| هدايا السبلة | `gifts` | طقوم وصحون نحاسية وتوزيعات الأعراس والأعياد |

**منتجات ← السمات**: أنشئ سمة **الوزن** بالقيم: نصف كيلو، كيلو، كيلو ونص.

**منتج تجريبي**: «حلوى سلطانية بالزعفران»، النوع **منتج متغير**، في قسم الحلوى السلطانية، باستخدام سمة الوزن (مفعّلة للتنويعات)، وأنشئ التنويعات الثلاث بأسعار مؤقتة (مثلاً 3.500 / 6.500 / 9.500 ر.ع). صورة مؤقتة أي صورة.

## المهمة 4: كود تخصيص صفحة الدفع (Code Snippets)

**Snippets ← Add New**
- العنوان: `تخصيص صفحة الدفع - عُمان`
- الصق الكود التالي **بدون** سطر `<?php`
- اختر **Run snippet everywhere**
- **Save Changes and Activate**
- إن ظهر خطأ: لا تحاول إصلاحه بنفسك بتعديل الكود، انسخ رسالة الخطأ كاملة وأبلغ صاحب المتجر.

**ما يفعله**: محافظات عُمان، حذف الحقول غير الضرورية، التحقق من رقم الجوال العماني وحفظه بصيغة +968 (يقبل الأرقام العربية)، حقل تاريخ توصيل مفضّل، حقل رسالة إهداء، وعرضهما في لوحة الطلب وصفحة الشكر والإيميلات.

```php
/**
 * متجر الحلوى العمانية - تخصيص صفحة الدفع الكلاسيكية
 */

/* 1) محافظات سلطنة عُمان */
add_filter( 'woocommerce_states', function ( $states ) {
	$states['OM'] = array(
		'MA' => 'مسقط',
		'BS' => 'شمال الباطنة',
		'BJ' => 'جنوب الباطنة',
		'DA' => 'الداخلية',
		'SS' => 'شمال الشرقية',
		'SJ' => 'جنوب الشرقية',
		'ZA' => 'الظاهرة',
		'BU' => 'البريمي',
		'WU' => 'الوسطى',
		'ZU' => 'ظفار',
		'MU' => 'مسندم',
	);
	return $states;
} );

/* 2) شكل العنوان في عُمان (يطبَّق أيضاً عبر جافاسكربت ووكومرس عند تحميل الصفحة) */
add_filter( 'woocommerce_get_country_locale', function ( $locale ) {
	$locale['OM'] = array_replace_recursive( $locale['OM'] ?? array(), array(
		'first_name' => array( 'label' => 'الاسم الكامل', 'priority' => 10 ),
		'state'      => array( 'label' => 'المحافظة', 'required' => true, 'priority' => 30 ),
		'city'       => array( 'label' => 'الولاية', 'required' => true, 'priority' => 40 ),
		'address_1'  => array(
			'label'       => 'العنوان',
			'placeholder' => 'المنطقة / الحي، رقم المنزل أو أقرب معلم',
			'priority'    => 50,
		),
		'postcode'   => array( 'required' => false, 'hidden' => true ),
	) );
	return $locale;
} );

/* 3) تبسيط الحقول */
add_filter( 'woocommerce_checkout_fields', function ( $fields ) {
	foreach ( array( 'billing_last_name', 'billing_company', 'billing_address_2', 'billing_postcode' ) as $key ) {
		unset( $fields['billing'][ $key ] );
	}

	$fields['billing']['billing_first_name']['label'] = 'الاسم الكامل';
	$fields['billing']['billing_first_name']['class'] = array( 'form-row-wide' );

	$fields['billing']['billing_phone'] = array_merge( $fields['billing']['billing_phone'] ?? array(), array(
		'type'              => 'tel',
		'label'             => 'رقم الجوال (واتساب)',
		'placeholder'       => '9XXXXXXX',
		'required'          => true,
		'priority'          => 20,
		'class'             => array( 'form-row-wide' ),
		'custom_attributes' => array( 'inputmode' => 'tel', 'dir' => 'ltr' ),
	) );

	// الإيميل اختياري: بدونه لن تصل للعميل رسائل تأكيد بالبريد.
	// ملاحظة: بعض بوابات الدفع تشترطه، راجعه عند تركيب البوابة.
	$fields['billing']['billing_email']['required'] = false;
	$fields['billing']['billing_email']['label']    = 'البريد الإلكتروني (اختياري)';
	$fields['billing']['billing_email']['priority'] = 60;

	if ( isset( $fields['order']['order_comments'] ) ) {
		$fields['order']['order_comments']['label']       = 'ملاحظات التوصيل';
		$fields['order']['order_comments']['placeholder'] = 'مثال: الاتصال قبل الوصول، أفضل وقت للتوصيل…';
	}
	return $fields;
} );

/* 4) رقم الجوال العماني */
function omh_latin_digits( $value ) {
	return strtr( (string) $value, array(
		'٠' => '0', '١' => '1', '٢' => '2', '٣' => '3', '٤' => '4',
		'٥' => '5', '٦' => '6', '٧' => '7', '٨' => '8', '٩' => '9',
		'۰' => '0', '۱' => '1', '۲' => '2', '۳' => '3', '۴' => '4',
		'۵' => '5', '۶' => '6', '۷' => '7', '۸' => '8', '۹' => '9',
	) );
}

function omh_normalize_om_phone( $phone ) {
	$digits = preg_replace( '/\D+/', '', omh_latin_digits( $phone ) );
	$digits = preg_replace( '/^(00968|968)/', '', $digits );
	return preg_match( '/^[79]\d{7}$/', $digits ) ? '+968' . $digits : false;
}

// تحويل الأرقام العربية قبل أن يقرأ ووكومرس البيانات ويتحقق منها.
add_action( 'woocommerce_checkout_process', function () {
	if ( isset( $_POST['billing_phone'] ) ) {
		$_POST['billing_phone'] = wc_clean( omh_latin_digits( wp_unslash( $_POST['billing_phone'] ) ) );
	}
} );

/* 5) حقلا تاريخ التوصيل ورسالة الإهداء */
function omh_delivery_window() {
	$tz = wp_timezone();
	return array(
		'min' => new DateTimeImmutable( 'tomorrow', $tz ),
		'max' => new DateTimeImmutable( 'today +30 days', $tz ),
	);
}

add_action( 'woocommerce_after_order_notes', function ( $checkout ) {
	$window = omh_delivery_window();

	woocommerce_form_field( 'omh_delivery_date', array(
		'type'              => 'date',
		'label'             => 'تاريخ التوصيل المفضّل',
		'class'             => array( 'form-row-wide' ),
		'custom_attributes' => array(
			'min' => $window['min']->format( 'Y-m-d' ),
			'max' => $window['max']->format( 'Y-m-d' ),
		),
	), $checkout->get_value( 'omh_delivery_date' ) );

	woocommerce_form_field( 'omh_gift_message', array(
		'type'        => 'textarea',
		'label'       => 'رسالة الإهداء (اختياري)',
		'placeholder' => 'تُكتب على بطاقة أنيقة ترافق طلبك',
		'maxlength'   => 200,
		'class'       => array( 'form-row-wide' ),
	), $checkout->get_value( 'omh_gift_message' ) );
} );

/* 6) التحقق */
add_action( 'woocommerce_after_checkout_validation', function ( $data, $errors ) {
	if ( ! empty( $data['billing_phone'] ) && false === omh_normalize_om_phone( $data['billing_phone'] ) ) {
		$errors->add( 'validation', 'يرجى إدخال رقم جوال عُماني صحيح مكوّن من 8 أرقام يبدأ بـ 9 أو 7.' );
	}

	$raw = isset( $_POST['omh_delivery_date'] ) ? wc_clean( wp_unslash( $_POST['omh_delivery_date'] ) ) : '';
	if ( '' !== $raw ) {
		$window = omh_delivery_window();
		$date   = DateTimeImmutable::createFromFormat( '!Y-m-d', $raw, wp_timezone() );
		if ( ! $date || $date < $window['min'] || $date > $window['max'] ) {
			$errors->add( 'validation', 'تاريخ التوصيل يجب أن يكون من الغد وحتى 30 يوماً.' );
		}
	}
}, 10, 2 );

/* 7) الحفظ في الطلب (متوافق مع HPOS) */
add_action( 'woocommerce_checkout_create_order', function ( $order ) {
	$phone = omh_normalize_om_phone( $order->get_billing_phone() );
	if ( $phone ) {
		$order->set_billing_phone( $phone );
	}

	$date = isset( $_POST['omh_delivery_date'] ) ? wc_clean( wp_unslash( $_POST['omh_delivery_date'] ) ) : '';
	if ( $date ) {
		$order->update_meta_data( '_omh_delivery_date', $date );
	}

	$gift = isset( $_POST['omh_gift_message'] ) ? sanitize_textarea_field( wp_unslash( $_POST['omh_gift_message'] ) ) : '';
	if ( $gift ) {
		$order->update_meta_data( '_omh_gift_message', mb_substr( $gift, 0, 200 ) );
	}
} );

/* 8) العرض: لوحة التحكم + صفحة الشكر + الإيميلات */
function omh_order_extras( $order ) {
	$extras = array();
	$date   = $order->get_meta( '_omh_delivery_date' );
	$gift   = $order->get_meta( '_omh_gift_message' );
	if ( $date ) {
		$extras['تاريخ التوصيل المفضّل'] = wp_date( 'l j F Y', strtotime( $date . ' 12:00 UTC' ) );
	}
	if ( $gift ) {
		$extras['رسالة الإهداء'] = $gift;
	}
	return $extras;
}

add_action( 'woocommerce_admin_order_data_after_billing_address', function ( $order ) {
	foreach ( omh_order_extras( $order ) as $label => $value ) {
		echo '<p><strong>' . esc_html( $label ) . ':</strong><br>' . nl2br( esc_html( $value ) ) . '</p>';
	}
} );

add_action( 'woocommerce_order_details_after_order_table', function ( $order ) {
	$extras = omh_order_extras( $order );
	if ( ! $extras ) {
		return;
	}
	echo '<section class="omh-order-extras">';
	foreach ( $extras as $label => $value ) {
		echo '<p><strong>' . esc_html( $label ) . ':</strong> ' . nl2br( esc_html( $value ) ) . '</p>';
	}
	echo '</section>';
} );

add_filter( 'woocommerce_email_order_meta_fields', function ( $fields, $sent_to_admin, $order ) {
	foreach ( omh_order_extras( $order ) as $label => $value ) {
		$fields[] = array( 'label' => $label, 'value' => esc_html( $value ) );
	}
	return $fields;
}, 10, 3 );

/* 9) لمسات وسرعة */
add_filter( 'woocommerce_order_button_text', function () {
	return 'تأكيد الطلب';
} );

// سكربت قوة كلمة المرور ثقيل، ولا داعي له إذا كان إنشاء الحساب من صفحة الدفع معطّلاً.
add_action( 'wp_enqueue_scripts', function () {
	if ( is_checkout() && 'yes' !== get_option( 'woocommerce_enable_signup_and_login_from_checkout' ) ) {
		wp_dequeue_script( 'wc-password-strength-meter' );
	}
}, 100 );
```

## المهمة 5: إعدادات Elementor

**Elementor ← الإعدادات**
- عام: فعّل **Disable Default Colors** و **Disable Default Fonts**.
- Features: تأكد أن **Flexbox Container** مفعّل.
- Performance/Features: فعّل **Load Google Fonts Locally** وأي خيار Optimized / Improved asset loading / Lazy load background images إن وُجد.

**Elementor Pro**: فعّل الترخيص من **Elementor ← License** (يحتاج حساب صاحب المتجر؛ إن لم يكن متاحاً اتركه وأبلغ).

**Site Settings** (افتح أي صفحة بـ Elementor ← القائمة ☰ ← Site Settings):

Global Colors:

| الاسم | الكود |
|---|---|
| بني التمر (Primary) | `#4A2C1D` |
| نحاسي (Secondary) | `#B87333` |
| ذهبي (Accent) | `#C9A24B` |
| زعفراني | `#E0A526` |
| بيج كريمي (خلفية) | `#F7F1E5` |
| بيج داكن | `#C8B48A` |
| نص | `#2B1A12` |

Global Fonts:
- Primary و Secondary: **Amiri** وزن 700
- Text: **Tajawal** وزن 400
- Accent: **Tajawal** وزن 700

Layout: Content Width = **1200px**

Custom CSS (الصقه في Site Settings ← Custom CSS):

```css
:root{
  --om-date:#4A2C1D; --om-copper:#B87333; --om-gold:#C9A24B;
  --om-saffron:#E0A526; --om-cream:#F7F1E5; --om-sand:#C8B48A;
  --om-ink:#2B1A12;
  --om-radius:14px;
  --om-shadow:0 10px 30px rgba(74,44,29,.12);
  --om-gold-grad:linear-gradient(135deg,#E0B85C 0%,#C9A24B 45%,#B87333 100%);
}
body{background:var(--om-cream);color:var(--om-ink);font-family:"Tajawal",sans-serif;}
h1,h2,h3,.elementor-heading-title{font-family:"Amiri",serif;color:var(--om-date);}

/* زر ذهبي/نحاسي موحّد */
.elementor-button,
.woocommerce a.button,.woocommerce button.button{
  background:var(--om-gold-grad)!important;color:#fff!important;
  border:0;border-radius:var(--om-radius);font-weight:700;
  box-shadow:0 6px 18px rgba(184,115,51,.35);
  transition:transform .2s ease,box-shadow .2s ease;
}
.elementor-button:hover,
.woocommerce a.button:hover,.woocommerce button.button:hover{
  transform:translateY(-2px);box-shadow:0 10px 24px rgba(184,115,51,.45);
}
```

## المهمة 6: Joinchat (زر واتساب للمحادثة فقط)

**الإعدادات ← Joinchat**
- رقم الجوال: **اطلبه من صاحب المتجر** (صيغة `968XXXXXXXX`)
- رسالة الترحيب: `هلا وغلا 🌿 تبي تستفسر عن حلوى أو عندك طلب خاص؟ نخدمك على الواتساب`
- الرسالة الافتراضية: `السلام عليكم، عندي استفسار عن: {TITLE}`
- مكان الزر: **يسار (Left)**
- تأخير الظهور: 5 ثوانٍ
- الإخفاء: في صفحة **الدفع (Checkout)**

## المهمة 7: الاختبار (إلزامي)

1. افتح صفحة المنتج التجريبي، اختر وزناً، أضفه للسلة، ثم اذهب للدفع.
2. تأكد أن حقول الدفع بالترتيب: الاسم الكامل، الجوال، المحافظة (قائمة بـ 11 محافظة)، الولاية، العنوان، البريد (اختياري). ولا يظهر حقل الدولة ولا الرمز البريدي.
3. جرّب الجوال: `91234567` و `+968 9123 4567` و `٩١٢٣٤٥٦٧` يجب أن تُقبل وتُحفظ `+96891234567`. و `12345` يجب أن يُرفض برسالة خطأ.
4. تاريخ التوصيل: اليوم يُرفض، وبعد يومين يُقبل.
5. أكمل طلباً بالدفع عند الاستلام، وتأكد أن صفحة الشكر تعرض التاريخ ورسالة الإهداء.
6. افتح الطلب من **WooCommerce ← الطلبات** وتأكد ظهور الجوال بصيغة +968 والتاريخ ورسالة الإهداء.
7. احذف الطلب التجريبي بعد التأكد.

## التقرير المطلوب في النهاية

أرسل لصاحب المتجر قائمة بكل مهمة: ✅ تمت / ⚠️ تمت جزئياً (مع السبب) / ❌ لم تتم (مع السبب)، ونتائج اختبارات المهمة 7، وأي رسائل خطأ ظهرت بنصها، والأشياء التي تحتاج قراره (أسعار الشحن، رقم الواتساب، ترخيص Elementor Pro).

**الخطوة التالية بعد هذا التكليف (لا تبدأ بها الآن):** بناء الهيدر والفوتر في Elementor ← Theme Builder.
