---
title: Subscribe
---

# Subscribe

Fire whenever a user subscribes to an email or product.

## Javascript Code

```js
// When:
// User subscribes to an email or product

// Code:
window.dataLayer = window.dataLayer || [];
dataLayer.push({ event_data: null });  // Clear the previous event_data object.
dataLayer.push({
  event: 'subscribe',
  event_data: {
    identifier: '<identifier>', // REQUIRED | string | ex. neutrogena_newsletter_123, jnj_promos_123
    name: '<name>', // REQUIRED | string | ex. neutrogena_newsletter, jnj_promos
    type: '<type>', // REQUIRED | string | ex. newsletter, promos
    method: '<method>' // REQUIRED | string | ex. email
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Maximum Length|
| --- | --- | --- | --- | --- | --- |
|**identifier**|`string`|required|The subscription machine-readable name. This should be a unique value specific to this subscription, if one exists. If one does not exist, this can also be populated with the same value as the `name`.|`neutrogena_newsletter_123`, `jnj_promos_123`|`100`|
|**name**|`string`|required|The subscription human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the subscription with. It should be lowercase snake_case.|`neutrogena_newsletter`, `jnj_promos`|`100`|
|**type**|`string`|required|The subscription type. This will act as a filtering mechanism in reporting to enable analysts to view subscription dropoff funnels. It can also act as an internal aid in firing additional events if necessary. For instance, lead-generating subscriptions require a `generate_lead` event to be fired alongside `form_complete`, and that could be written into the logic based upon this field.|`newsletter`, `promos`|`100`|
|**method**|`string`|required|The channel through which the subscription is delivered. This is usually email, but can also be product.|`email`,`product`|`100`|
