---
title: Form Complete
---

# Form Complete

Fire whenever a user successfully completes a form. 

This event is fired when form input is successfully received and processed. This is in contrast to [`form_error`](../../events/forms/form_error.md) which occurs when a submission is attempted but an error occurs and the form input is not received and processed.

!!! warning

    _**Do not**_ clear the page_data variable before setting user_login_state here as this is not a page view.

??? info "DO NOT populate user_id with a string value if unavailable"

    If the "user_id" is _**NOT**_ available, _**DO NOT**_ populate with an empty string (ex. "") or undefined as a string (ex. "undefined"). This value must _**ONLY**_ be populated with a valid user id. If this value is not available, then either _**DO NOT**_ include the parameter in the data layer push or populate with an undefined object (not a string).

## Javascript Code

```js
// When:
// User successfully completes a form and data is received and processed
// NOTE: Do not clear the page_data variable before setting user_login_state here. This is not a page view.

// Code:
window.dataLayer = window.dataLayer || [];
dataLayer.push({ event_data: null, user_data: null });  // Clear the previous event_data and user_data objects.
dataLayer.push({
  event: 'form_complete',
  event_data: {
    identifier: '<identifier>', // REQUIRED | string | ex. contact, lead_generation
    name: '<name>', // REQUIRED | string | ex. contact, lead_generation	
    type: '<type>' // REQUIRED | string | ex. contact, lead_generation	
  },
  page_data: {
    user_login_state: '<user_login_state>' // REQUIRED | string | authenticated or anonymous
  },
  user_data: {
    event_form_hashemail: '<HashedEmail>', // REQUIRED | string | ex. 21c27e7c7ddc7bd779679440526319aec9db0ff97535f59728f764e946979843
    event_form_custkey: '<SFMC_CustomerKey>', // optional | string | ex. 12345...
    user_id: '<user_id>', // optional | string | ex. 12345...
    user_type: '<user_type>' // optional | string | ex. new, returning, ...
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Maximum Length|
| --- | --- | --- | --- | --- | --- |
|**identifier**|`string`|required|The form machine-readable name. This should be a unique value specific to this piece of content, if one exists. If one does not exist, this can also be populated with the same value as the <name>.|`contact`, `lead_generation`|`100`|
|**name**|`string`|required|The form human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the form with. It should be lowercase snake_case.|`contact`, `lead_generation`|`100`|
|**type**|`string`|required|The form type. This will act as a filtering mechanism in reporting to enable analysts to view form droppoff funnels. It can also act as an internal aid in firing additional events if necessary. For instance, lead-generating forms require a `generate_lead` event to be fired alongside `form_complete`, and that could be written into the logic based upon this field.|`contact`, `lead_generation`|`100`|
|**user_login_state**|`string`|required|Set on all events with the authentication status of the current visitor.|`authenticated`, `anonymous`|`100`|
|**event_form_hashemail**|`string`|required|Hash (SHA256) of submitted user email.|`21c27e7c7ddc7bd779679440526319aec9db0ff97535f59728f764e946979843`|`100`|
|**event_form_custkey**|`string`|optional|This is the ID created by Salesforce Marketing Cloud (SFMC).|`12345...`|`100`|
|**user_id**|`string`|optional|ID of the user currently logged in to the site — should be included only, when submitting the form results in user authentication, or user was authenticated before submitting the form. This should only be populated with a valid user ID. This _**MUST NOT**_ be populated with any other string, ex. "undefined", "null". Using an undefined object is permitted.|`1234567890`|`100`|
|**user_type**|`string`|optional|Type of authenticated user. This should only be populated with a valid user type. This _**MUST NOT**_ be populated with any other string, ex. "undefined", "null". Using an undefined object is permitted.|`new`, `returning`|`100`|
