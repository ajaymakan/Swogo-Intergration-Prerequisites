# Swogo Intergration Prerequisites

## Page Integration

Swogo script has to be present on a preagreed list of pages. The minimum list of pages is:

- **Product Description/Details Page**
- **Cross sell (OPTIONAL - If we’re going to display popup bundles on this page )**
- **Basket/Cart Page**
- **Payment/Order Confirmation Page**

In certain cases where there is a dedicated mobile website which differs from the standard desktop implementation, Swogo script should be additionally deployed to its relevant pages.

Swogo script has to be intereated on the page directly into the <HEAD> section of the page HTML.
Tag Manager integration is highly discouraged due to observable delays in the loading of the bundles due to Tag Manager script queueing. 
  
 !! Insert example 
  
  
## HTML DOM Containers
In order to isolate functionality and prevent attaching Swogo bundles to dynamic elements on the page Swogo bundles require dedicated DIV elements on the page. The elements should comply with the follwing format:

**Tag Name**: `DIV`

**Class name**: `“swogo-box”`

**ID names**: `"swogo-bundle-0"`, `"swogo-bundle-1"`, …

The index number after `swogo-bundle` should be assigned depending on the total number of containers on the page. (The number of containers depends on the number of the different positions we display bundles. Default for one bundle on the page is `swogo-bundle-0` ). The indexing is such that the lower the container is on the page the higher the incremental index number (top-down / incremental index numbers / start from 0).

**Note**

If the container is generated dynamicly, it will follow the same naming conventions outlined above.

This bundle will be triggered on an event where the container is passed to the swogo script by the client.
  
  
## Page Identifiers
In order for the script to identify on which page it has been deployed it requires a specific JavaScript object that provides that information. 

**The function should be implemented on all pages listed in "Page Integration" **

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


<<< IMAGE HERE swogoDependencies-getPage.png


## SKU Identifiers

Easily accessible JavasScript SKU (product ID) identifiers list is required in order to provide relevant cross-sell bundles.

**The function should be implemented on all pages listed in "Page Integration"**

The functionality should be provided in a similar to the previous point implementation:

`swogoDependencies.getSkus();`

and should return the following array of SKUs of Object type:

```
[ 
    {
      “sku”:”string”,
      “price”:number,
      “quantity”:number,
      “title”:”string”,
      “secondarySKU”:”string” //(optional)
      // … (more attributes optional)
    }, 
    { ... },
...
]
```

**Behaviour**

On **PDP**, **Mobile PDP** and **Cross-sell** pages the function should return the SKU of the main item displayed. 
We expect to receive only one element in the array.

`[{...}]`  - main item details


On **Basket**, **Mobile Basket** the function below should return the details of the products currently contained/listed in the basket/cart

`swogoDependencies.getBasketSkus();`

`[{...},{...},{...}]` - items added to basket


and on **Payment Confirmation** pages the function should return the details of the products that have been bought

`swogoDependencies.getPaidSkus();`

`[{...},{...},{...}]` - items succesfully paid for


## Add-to-cart Functionality

Swogo bundles enables the buyer with one-click-buy funcitonality. We provide add-to-cart buttons which push all products from a selected bundle to the cart. To do this and provide robust and maintainable implementation Swogo script requires an add to cart function which allows:
1. adding products to basket based on provided SKU, additional SKUs and quantity. 
2. Ability to add multiple items to the basket. 
3. The function should be available on all pages where swogo script is present.
4. Callback that allows Swogo to act and update the client on completion of the action.
5. The function sould be freely accessible from our script and belog to `window` directly
6. The funciton name should preferably be called `addToCart` and take the following parameter format:

```
addToCart(
    [
       {
	         sku:””,   
	         additionalSKUs:[],
	         quantity:number
       },
       {...},
       ... 
    ],
    callback(error, data)
);`

```
**callback** - call callback on completion of the add-to-cart execution returning standard parameters:

**error** - failed

**data** - success confirmation  


## Conclusion 

TBA

