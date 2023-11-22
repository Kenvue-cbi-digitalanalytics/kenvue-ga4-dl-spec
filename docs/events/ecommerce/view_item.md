# View Item

Fire whenever a user visits a product detail page/screen.

This event is to fire when a user is presented with a _**HIGHLY DETAILED**_ page/screen, which includes (but is not limited to):
- A web Page
- after clicking "more details" on an item and an on-page window opens up and displays a product detail screen overlaying the previous screen

If a page/screen is providing the user with detailed information, the user can add a product to their cart, and navigate to their cart with a product added, then it is highly likely that this page/screen is a product detail page/screen

## Javascript Code

```js
// When:
// User visits a product detail page

// Code:
window.dataLayer = window.dataLayer || [];
dataLayer.push({ event_data: null, ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "view_item",
  event_data: {
    identifier: "<identifier>", // REQUIRED | string | ex. uniquely_created_id, skin360_pwa_ntg_atc
    name: '<name>' // REQUIRED | string | ex. pdp_add_to_cart, skin360_pwa_ntg add_to_cart
},
  ecommerce: {
    currency: "<currency>", // REQUIRED | string | ex. USD | pattern: ^[A-Z]{3}$ | min. 3, max. 3
    items: "<items>", // REQUIRED | array | ex. [{item_id: "test"}]
    value: "<value>" // REQUIRED | number | ex. 7.77 | pattern: ^\d\.\d\d$ | min. 0.00
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Pattern|Minimum Length|Maximum Length|Minimum|
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|**identifier**|`string`|required|The wtb-event machine-readable name. This should be a unique value specific to this piece of content, if one exists. If one does not exist, this can also be populated with the same value as the <name>.|`contact`, `lead_generation`|||`100`|
|**name**|`string`|required|The wtb-event human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the event with. It should be lowercase snake_case.|`contact`, `lead_generation`|||`100`|
|currency|string|recommended|Currency of the items associated with the event, in 3-letter ISO 4217 format.|`USD`|`^[A-Z]{3}$`|`3`|`3`|
|items|array of [items](../../schemas/item.md)|required|Populate with item objects that represent the product viewed.|`[{item_id: "test"}]`
|value|number|recommended|The monetary value of the event. Does not include currency sign.|`7.77`|`^\d\.\d\d$`||`100`|`0.00`|
