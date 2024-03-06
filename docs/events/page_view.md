# Page View

Fire whenever a user loads in a new page, whether that is done synchronously or asynchronously.

This event should be the first pushed into the data layer on each page. Given many 3rd party scripts push events to the data layer, this event push should be placed in the page `<head>` and should be the first `<script>` tag on the page to ensure it is the first event.

???+ note "Page Views and Virtual Page Views are now the same in GA4"

    There is no longer a concept of virtual page view, so this event should be fired whenever a virtual page view would have been fired in the past, such as when a new screen is loaded asynchronously within an angular, react, or vue app/embed.

## Javascript Code

```js
// When:
// User loads a new page (synchronously or asynchronously)
// Should be the first push into dataLayer, placed in the <head> and ideally first <script> on page.

// Code
window.dataLayer = window.dataLayer || [];
dataLayer.push({ event_data: null, page_data: null, user_data: null });  // Clear the previous attributes.
dataLayer.push({
  event: 'page_view',
  event_data: {
    name: '<name>', // REQUIRED | string | ex. page_view, add_to_cart, purchase
    identifier: "<identifier>" // REQUIRED | string
},
  page_data: {
    page_id: '<page_id>', // REQUIRED | string
    page_name: '<page_name>', // REQUIRED | string
    page_type: '<page_type>', // REQUIRED | string | ex. home, product category, product detail, article page
    page_category: '<category>', // contextual | string
    page_referrer: '<page_referrer>', // REQUIRED | string
    site_brand: '<site_brand>', // REQUIRED | string | ex. Neutrogena, OGX, Bebe
    site_country: '<site_country>', // REQUIRED | string | ex. US, DE, AU
    site_franchise: '<site_franchise>', // REQUIRED | string | ex. Essential Health, Skin Health
    site_region: '<site_region>', // REQUIRED | string | ex. US, EMEA, APAC
    user_login_state: '<user_login_state>' // REQUIRED | string | authenticated or anonymous
  },
  user_data: {
    user_id: '<user_id>' // REQUIRED, if user is logged in, can be omitted otherwise | string
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Max Len|How to test?|
| --- | --- | --- | --- | --- | --- | --- |
|**name**|`string`|required|The human-readable event name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the event with. It should be lowercase snake_case.|`page_view, add_to_cart, purchase`|`100`|Value not null or empty. Length within limit.|
|**identifier**|`string`|required|The machine-readable event identifier. This should be a unique value specific to this piece of content, if one exists. If one does not exist, this can also be populated with the same value as the name param.||`100`|Value not null or empty. Length within limit.|
|**page_id**|`string`|required|A durable identifier for a page that will enable measurement over time despite the page URL, title, etc changing. Generally sourced from the site content management system.||`100`|Value not null or empty. Length within limit.|
|**page_name**|`string`|required|A unique name for this page independent of page title. Google does not tend to use custom page names, but it's a mainstay in Adobe and therefore is included here for compatibility as well as for its usefulness generally.||`100`|Value not null or empty. Length within limit.|
|**page_type**|`string`|required|Used for grouping pages (or screens) into high level types. Most often aligns with page taxonomy or content type for base page.|`home, product category, product detail, article page`|`100`|[List of available values](https://docs.google.com/spreadsheets/d/1laiSuNBb7Y5ZCh7dJpM2T9tF0sR14bPI1wOy_PA9ma8/edit?usp=sharing)|
|**page_category**|`string`|contextual|Used for grouping pages (or screens) into categories based on their content.||`100`|Optional param. No need to test.|
|**page_referrer**|`string`|required|Prior page viewed - for SPA portions of the site, this most likely will not be document.referrer and might need to be pulled from the prior history state or some other stored value to provide more accurate context.|`https://www.neutrogena.com/`|`100`|Value is an empty string — or a valid URL address.|
|**site_brand**|`string`|required|Brand the site is associated with.|`Neutrogena, OGX, Bebe`|`100`|[List of available values](https://docs.google.com/spreadsheets/d/1laiSuNBb7Y5ZCh7dJpM2T9tF0sR14bPI1wOy_PA9ma8/edit?usp=sharing)|
|**site_country**|`string`|required|Country the site is associated with. It must follow this [ISO Standard ==> Alpha-2-Codes](https://www.iso.org/iso-3166-country-codes.html) — and consist of capital letters only.|`US, DE, AU`|`2`|Value is a valid 2-letter country ISO code.|
|**site_franchise**|`string`|required|Franchise the site is associated with.|`Essential Health, Skin Health`|`100`|[List of available values](https://docs.google.com/spreadsheets/d/1laiSuNBb7Y5ZCh7dJpM2T9tF0sR14bPI1wOy_PA9ma8/edit?usp=sharing)|
|**site_region**|`string`|required|Region the site is associated with.|`US, EMEA, APAC`|`100`|[List of available values](https://docs.google.com/spreadsheets/d/1laiSuNBb7Y5ZCh7dJpM2T9tF0sR14bPI1wOy_PA9ma8/edit?usp=sharing)|
|**user_login_state**|`string`|required|Set on all events with the authentication status of the current visitor.|`authenticated, anonymous`|`100`|Value is either *authenticated* or *anonymous*|
|**user_id**|`string`|contextual|ID of the user currently logged in to the site, if the site offers authentication and the user is authenticated.||`100`|Test only if user is authenticated (ie. user_login_state is *authenticated*) — then, must be not null or empty, length within limit.|
