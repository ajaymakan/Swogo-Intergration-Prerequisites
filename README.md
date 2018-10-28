# Swogo Intergration Prerequisites

## Page Integration

Swogo script has to be present on a preagreed list of pages. The minimum list of pages is:

- **Product Description/Details Page**
- **Basket/Cart Page**
- **Payment/Order Confirmation Page**

Swogo script has to be intereated on the page directly into the <HEAD> section of the page HTML.
Tag Manager integration is highly discouraged due to observable delays in the loading of the bundles due to Tag Manager script queueing. 
  
 !! Insert example 
  
## Page Identifiers
In order for the script to identify on which page it has been deployed it requires a specific JavaScript object that provides that information. 


**Wrapper object:**  `swogoDependencies` or `window.swogoDependencies`

**Page identifier function:** `swogoDependencies.getPage()` or `window.swogoDependencies.getPage()`

The function returns one of the following identifiers:
- `"pdp"` - product description page
- `"mobilePdp"` - product description page (if there is a a separate mobile website implementation. Responsive design does not count as separate mobile website)
- `"basket"` - Basket or Cart page, listing all product currently added to basket
- `"mobileBasket"` - Basket or Cart page, listing all product currently added to basket for mobile websites
- `"payment"` - Order confirmation page displaying successfull order/payment completion 
- `"mobilePayment"` - Order confirmation page for mobile website

Example:

Calling the following funciton:
`swogoDependencies.getPage()` 
on Product Details Page in the JavascritpConsole should return:
`"pdp"` 


SKU Identifiers

HTML DOM Containers

Add-to-cart Functionality

Tracking Pixel 
