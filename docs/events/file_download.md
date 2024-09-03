# File Download

These events will be automatically detected and fired for any link clicked by the user that leads to a file.

In case it does not happen — link to a file has to be tagged with a Javascript code, described below.

## Javascript Code

```js
// When:
// User clicks a non anchor tag used for a file download, i.e. <button>

// Code
window.dataLayer = window.dataLayer || [];
dataLayer.push({ event_data: null });  // Clear the previous event_data object.
dataLayer.push({
  event: "file_download",
  event_data: {
    identifier: '<identifier>', // REQUIRED | string | ex. uniquely_created_id
    name: '<name>', // REQUIRED | string | ex. Learn More, How it works, Ingredients, Connect
    component_ancestry: "<component_ancestry>", // contextual | string | string - delimeted (~) | ex. hero~product carousel
    link_classes: "<link_classes>", // REQUIRED | string | ex. button-red 
    link_id: "<link_id>", // REQUIRED | string | ex. submit-button
    link_text: "<link_text>", // REQUIRED | string | ex. click here
    link_url: "<link_url>", // REQUIRED | string | ex. https://www.example.com/form
    link_hostname: "<link_hostname>", // REQUIRED | string | ex. https://www.example.com
    navigation_ancestry: "<navigation_ancestry>", // contextual | string - delimeted (~) | ex. about~our ceo
    outbound: "<outbound>", // contextual | boolean | ex. false
    region_ancestry: "<region_ancestry>", // contextual | string - delimeted (~) | ex. header~navigation
    protocol: "<type>" // REQUIRED | string | ex. http, https, mailto, tel
    file_extension: "<file_extension>", // recommended | string | ex. pdf
    file_name: "<file_name>", // recommended | string | ex. example.pdf
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Maximum Length|
| --- | --- | --- | --- | --- | --- |
|**identifier**|`string`|required|The wtb-event machine-readable name. This should be a unique value specific to this piece of content, if one exists. If one does not exist, this can also be populated with the same value as the <name>.|`contact`, `lead_generation`|`100`|
|**name**|`string`|required|The wtb-event human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the event with. It should be lowercase snake_case.|`contact`, `lead_generation`|`100`|
|**component_ancestry**|`string`|contextual|A delimited string showing all components in the ancestry of the link clicked|`hero~product carousel`|`100`|
|**link_classes**|`string`|required|The list of HTML/CSS classes applied to the link.|`button-red`|`100`|
|**link_id**|`string`|required|The HTML/CSS ID of the link.|`submit-button`|`100`|
|**link_text**|`string`|required|The full text of the link.|`click here`|`100`|
|**link_url**|`string`|required|The full URL of the link.|`https://www.example.com/form`|`100`|
|**link_hostname**|`string`|required|The hostname of the link.|`https://www.example.com`|`100`|
|**navigation_ancestry**|`string`|contextual|A delimited string showing all navigation items in the ancestry of link clicked in a multi-tiered menu|`about~our leadership~our CEO`|`100`|
|**outbound**|`boolean`|contextual|Does the link point to a different domain?|`false`|`100`|
|**region_ancestry**|`string`|contextual|A delimited string showing all regions in the ancestry of the link clicked|`header~navigation`|`100`|
|**protocol**|`string`|required|Records the type of link that was clicked. The type here refers to what comes before the :// on the link itself. Useful for identifying http links that should be https, as well as reporting on mailto, tel, and other alternate link types|`http`, `https`, `tel`, `mailto`|`100`|
|**file_extension**|`string`|recommended|The file extension of the file being downloaded.|`pdf`|`100`|
|**file_name**|`string`|recommended|The filename of the file being downloaded.|`drug_facts.pdf`|`100`|
