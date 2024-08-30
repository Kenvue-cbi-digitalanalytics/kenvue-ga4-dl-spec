---
title: Form Error
---

# Form Error

Fire whenever a user unsuccessfully completes a form. 

This is in contrast to [`form_complete`](../../events/forms/form_error.md) which occurs when a submission succeeds.

## Javascript Code

```js
// When:
// User unsuccessfully completes a form and data is not received or processed

// Code:
window.dataLayer = window.dataLayer || [];
dataLayer.push({ event_data: null });  // Clear the previous event_data object.
dataLayer.push({
  event: 'form_error',
  event_data: {
    identifier: '<identifier>', // REQUIRED | string | ex. contact, lead_generation
    name: '<name>', // REQUIRED | string | ex. contact, lead_generation	
    type: '<type>', // REQUIRED | string | ex. contact, lead_generation	
    error_message: '<error_message>' // REQUIRED | string | ex. Phone number should follow the format (xxx) xxx-xxxx
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Maximum Length|
| --- | --- | --- | --- | --- | --- |
|**identifier**|`string`|required|The form machine-readable name. This should be a unique value specific to this piece of content, if one exists. If one does not exist, this can also be populated with the same value as the <name>.|`contact`, `lead_generation`|`100`|
|**name**|`string`|required|The form human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the form with. It should be lowercase snake_case.|`contact`, `lead_generation`|`100`|
|**type**|`string`|required|The form type. This will act as a filtering mechanism in reporting to enable analysts to view form droppoff funnels. It can also act as an internal aid in firing additional events if necessary. For instance, lead-generating forms require a `generate_lead` event to be fired alongside `form_complete`, and that could be written into the logic based upon this field.|`contact`, `lead_generation`|`100`|
|**error_message**|`string`|required|The specific error that has occurred. It should include rejected field name(s).|`Phone number should follow the format (xxx) xxx-xxxx`|`100`|
