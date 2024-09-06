# Kenvue DXP OneTrust Snippet
This document is a quick reference to implement the OneTrust snippet across all Kenvue brand, HCP and corporate sites. For any questions regarding this content please contact Analytics Team - ra-jx2-cbi-digital06@kenvue.com

## HTML Code For All Production Sites
Add the following snippet to every page inside the `<head>`, as high as possible — **it has to be fired before any other analytics snippets.** First part, so called default consent state tag, is required, for every single site. Second part, control script, has to be added only if cookie banner is required to be displayed on the page (ie. for EU, CH, UK, BR, SA, US, CA, JP and TH).

```html
<!-- Default consent tag -->
<script> 
  window.dataLayer = window.dataLayer || []; 
  function gtag(){dataLayer.push(arguments);}

  gtag('consent', 'default', {
        security_storage: "<SECURITY_STORAGE_DEFAULT_STATE>",
        functionality_storage: "<FUNCTIONALITY_STORAGE_DEFAULT_STATE>",
        analytics_storage: "<ANALYTICS_STORAGE_DEFAULT_STATE>",
        ad_storage: "<AD_STORAGE_DEFAULT_STATE>", 
        ad_user_data: "<AD_DATA_DEFAULT_STATE>",
        ad_personalization: "<AD_PERSONALIZATION_DEFAULT_STATE>",
        personalization_storage: "<PERSONALIZATION_STORAGE_DEFAULT_STATE>",
        wait_for_update: 500 
  }); 
</script>

<!-- OneTrust control script -->
<script src="https://cdn.cookielaw.org/scripttemplates/otSDKStub.js" data-document-language="true" type="text/javascript" charset="UTF-8" data-domain-script="<DOMAIN_ID>" ></script>
<script type="text/javascript">
function OptanonWrapper() { }
</script>
```

## Variable Definitions

|Field|Type|Value|
| --- | --- | --- |
|**SECURITY_STORAGE_DEFAULT_STATE**|`string`|Always "granted".|
|**FUNCTIONALITY_STORAGE_DEFAULT_STATE**|`string`|Always "granted".|
|**ANALYTICS_STORAGE_DEFAULT_STATE**|`string`|Determined by country domain. EU, CH, UK, BR, SA, US, CA, JP and TH — "denied". All other — "granted".|
|**AD_STORAGE_DEFAULT_STATE**|`string`|Determined by country domain. EU, CH, UK, BR, SA, US, CA, JP and TH — "denied". All other — "granted".|
|**AD_DATA_DEFAULT_STATE**|`string`|Determined by country domain. EU, CH, UK, BR, SA, US, CA, JP and TH — "denied". All other — "granted".|
|**AD_PERSONALIZATION_DEFAULT_STATE**|`string`|Determined by country domain. EU, CH, UK, BR, SA, US, CA, JP and TH — "denied". All other — "granted".|
|**PERSONALIZATION_STORAGE_DEFAULT_STATE**|`string`|Determined by country domain. EU, CH, UK, BR, SA, US, CA, JP and TH — "denied". All other — "granted".|
|**DOMAIN_ID**|`string`|OneTrust Domain ID generated in OneTrust admin panel.|
