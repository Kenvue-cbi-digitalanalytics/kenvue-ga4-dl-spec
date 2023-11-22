# Add Payment Info

Fire whenever a user submits their payment information. This event will fire _**AFTER**_ the user has successfully completed the "Add Payment Info" step and has done the following:

1. Payment info has populated all required payment fields.
2. The user has selected to move on to the next step (e.g. shipping info, order review, etc.).
3. The system has successfully verified the payment info and moves the user from the payment step to the following step.

Pairs with the following events:
- [Begin Checkout](../../events/ecommerce/begin_checkout.md)
- [Add Shipping Info](../../events/ecommerce/add_shipping_info.md)

## Javascript Code

```js
// When:
// User user submits payment information

// Code:
window.dataLayer = window.dataLayer || [];
dataLayer.push({ ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "add_payment_info",
  event_data: {
    identifier: "<identifier>", // REQUIRED | string | ex. uniquely_created_id, skin360_pwa_ntg_atc
    name: '<name>' // REQUIRED | string | ex. pdp_add_to_cart, skin360_pwa_ntg add_to_cart
},
  ecommerce: {
    coupon: "<coupon>", // contextual | string | ex. SUMMER_FUN | pattern: ^[A-Za-z0-9_]+$
    currency: "<currency>", // REQUIRED | string | ex. USD | pattern: ^[A-Z]{3}$ | min. 3, max. 3
    items: "<items>", // REQUIRED | array | ex. [{item_id: "test"}]	
    payment_method: "<payment_method>", // REQUIRED | string | ex. credit_card | pattern: ^[a-z_]+$
    value: "<value>" // REQUIRED | number | ex. 7.77 | pattern: ^\d\.\d\d$ | min. 0.00
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Pattern|Minimum Length|Maximum Length|Minimum
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|**identifier**|`string`|required|The wtb-event machine-readable name. This should be a unique value specific to this piece of content, if one exists. If one does not exist, this can also be populated with the same value as the <name>.|`contact`, `lead_generation`|`100`|
|**name**|`string`|required|The wtb-event human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the event with. It should be lowercase snake_case.|`contact`, `lead_generation`|`100`|
|coupon|string|contextual|The coupon name/code associated with the event. Event-level and item-level coupon parameters are independent.|`SUMMER_FUN`|||`100`|
|currency|string|required|Currency of the items associated with the event, in 3-letter ISO 4217 format.|`USD`|`^[A-Z]{3}$`|`3`|`3`|
|items|array of [items](../../schemas/item.md)|required|Populate with item objects that represent the product(s) currently in the cart during the checkout process.|`[{item_id: "test"}]`|
|payment_method|string|required|The chosen method of payment.|`credit_card`|||`100`|
|value|number|required|The monetary value of the event. Does not include currency sign.|`7.77`|`^\d\.\d\d$`||`100`|`0.00`|
