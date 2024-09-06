# Kenvue DXP GTM Code
This document is a quick reference to implement the GTM Container across all Kenvue Brand/DTC and HCP sites. For any questions regarding this content please contact Analytics Team - ra-jx2-cbi-digital06@kenvue.com

## HTML Code For All Production Sites
Add the following snippet to every page inside the `<head>` as high as possible:

```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-WSPHT2V');</script>
<!-- End Google Tag Manager -->
```

If possible, add this snippet just inside the opening `<body>` tag:

```html
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-WSPHT2V"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
```

## HTML Code For All Non-Production Sites
Add the following snippet to every page inside the `<head>` as high as possible:

```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl+ '&gtm_auth=7DwgpYUaj4gvAHugt88AzA&gtm_preview=env-3&gtm_cookies_win=x';f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-WSPHT2V');</script>
<!-- End Google Tag Manager -->
```

If possible, add this snippet just inside the opening `<body>` tag:

```html
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-WSPHT2V&gtm_auth=7DwgpYUaj4gvAHugt88AzA&gtm_preview=env-3&gtm_cookies_win=x"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
```


!!! note
    The `noscript` tag is optional and primarily used for site ownership validation through Google Search Console (there are other ways of validating site ownership).
    If a user has JS turned off in the browser, the data layer will not work. The only GTM tags available through the iframe-loaded GTM container are custom image tags.
    [More on the GTM noscript tag](https://www.analyticsmania.com/post/google-tag-manager-noscript/)
