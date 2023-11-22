# View Item List

Fire whenever a user sees multiple product links in a list that forward the user to the product detail page. 

This event should also be fired for the "Filter By Group" component when the list is initially displayed, or when a user applies a facet (but only when that component contains one or more products).

## HTML Data Attributes

```html
<a href="<link_url>"
  data-layer-event="view_item_list"
  data-layer-identifier="<identifier>"
  data-layer-name="<name>"
  data-layer-facets="<facets>"
  data-layer-list_type="<list_type>"
  data-layer-list_type="<item_list_id>"
  data-layer-list_type="<item_list_name>"
  data-layer-search_term="<search_term>"
  data-layer-search_type="<search_type>"
>
```

## Javascript Code

```js
// When:
// User sees multiple product links in a list that forward to a product detail page
// 'Filter By Group' component list is initially displayed or updated after a facet is applied, but only for products

// Code:
window.dataLayer = window.dataLayer || [];
dataLayer.push({ event_data: null, ecommerce: null });  // Clear the previous ecommerce object.
dataLayer.push({
  event: "view_item_list",
  event_data: {
    identifier: "<identifier>", // REQUIRED | string | ex. uniquely_created_id, skin360_pwa_ntg_atc
    name: '<name>' // REQUIRED | string | ex. pdp_add_to_cart, skin360_pwa_ntg add_to_cart
},
  ecommerce: {
    facets: "<facets>", // contextual | string - double delimited (:)(~) | ex. category:skin_health~featured_as:best_seller	
    items: "<items>", // REQUIRED | array | ex. [{item_id: "070501110485", item_name: "Neutrogena Hydro Boost Gel-Cream"}]	
    item_list_id: "<item_list_id>", // REQUIRED | string | ex. 12345abcde12345
    item_list_name: "<item_list_name>", // REQUIRED | string | ex. filter_by_group, recommended_products, recently_viewed_products
    list_type: "<list_type>", // REQUIRED | string | ex. cards, search_results	
    search_term: "<search_term>", // contextual | string | ex. sunscreen
    search_type: "<search_type>", // contextual | string | ex. site, filter_by_group
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Maximum Length|
| --- | --- | --- | --- | --- | --- |
|**identifier**|`string`|required|The wtb-event machine-readable name. This should be a unique value specific to this piece of content, if one exists. If one does not exist, this can also be populated with the same value as the <name>.|`contact`, `lead_generation`|`100`|
|**name**|`string`|required|The wtb-event human-readable name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the event with. It should be lowercase snake_case.|`contact`, `lead_generation`|`100`|
|facets|delimited string|contextual|A double-delimited string of key/value pairs representing the refinements that were applied if this list is displayed using the "Filter By Group" component.|`category:skin_health\~skin_concern:acne\ ~featured_as:best_seller`|`100`|
|items|array of [items](../../schemas/item.md)|required|Populate with item objects that represent each product in the list.|`[{item_id: "test"}]`
|item_list_id|string|required|The computer-readable machine name of the list the item showed up in. Use UUID provided by the component if no more specific ID is available.|`12345abcde12345`|`100`|
|item_list_name|string|required|The human-readable name of the list the item showed up in. If one is not available, populate with numerical index of which list this is on the page (1-indexed). For `filter_by_group` component, use that value.|`filter_by_group, recommended_products, recently_viewed_products, search_results`|`100`|
|list_type|string|required|The type of list the item was found in.|`cards, search_results`|`100`|
|search_term|string|contextual|The final search term submitted after any correction has been performed. Only set if the `list_type` is `search_results`.|`sunscreen`|`100`|
|search_type|string|contextual|The type of search performed. Only set if the `list_type` is `search_results`.|`site, filter_by_group`|`100`|
