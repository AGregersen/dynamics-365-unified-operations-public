---
# required metadata

title: Author a header module
description: This topic describes what a header module is and how to author a header module in Dynamics 365 for Commerce.
author: AnupamaR
manager: annbe
ms.date: 08/30/2019
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 

# optional metadata

# ms.search.form: 
audience: Consumer
# ms.devlang: 
ms.reviewer: josaw
ms.search.scope: Retail, Core, Operations
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: AnupamaR
ms.search.validFrom: 2019-08-30
ms.dyn365.ops.version: 
---

# Author a header module

A header module is a special container that is used for hosting all the modules that will be displayed on the page header. For example, it can include your site logo, links to the navigation hierarchy, links to other pages on the site, the search bar, and more. 

The header module will be optimized depending on the device the site is being used on, either desktop or mobile. For example, the navigation bar will collapse into a "hamburger menu" in mobile view port.

## Properties of a header

The header module supports the heading and width property, similar to generic containers. 

The header container has multiple slots, including informational message, navigation menu, logo, search bar, cCart icon, wishlist icon, and account information. Each slot supports a specific set of modules.

## Modules available in a header

The following modules can be used in the header.

- **Navigation menu**: The navigation menu item represents the channel navigation hierarchy and other static navigation links. The channel navigation hierarchy can be configured in headquarters (HQ). The configured item will appear as a header navigation. In addition, static navigation links can be configured and relative links to other pages on the e-Commerce site can be provided. The header itself can be aligned left, right, or center. 

- **Cart icon**: The cart icon is a special icon representing the cart, shown on the header to indicate the number of items in the cart. A link to the cart page should be provided with the cart icon so the user can be redirected to the page when they interact with the icon.

- **Wishlist icon**: The wishlist icon is a special icon shown on the header to indicate the number of items a customer has added to their wishlist. A link to the wishlist page should be provided with this icon so the user can be redirected to the page when they interact with the icon.

- **Sign-in module**: The sign-in module is shown on the header to allow the user to sign in or sign up for an account. If the user is already signed in, the module can be configured to show links to the account page, order history, or another page.

- **Logo module**: This module shows the logo that represents the retailer and brand. It is an image with a link. The link is typically programmed to redirect to the home page, so the user has a quick way to navigate back to the home page from any page on the site.

- **Alert**: An alert is used to show an inline message on the header that applies to all pages on the site. For example, an alert may be a message such as “Annual sale ends in 2 days”. 

- **Search bar**: The search bar allows the user to enter search terms to search for products. The module must be configured with the search page URL, which is the URL to the search results page. The query string parameter should be provided--the default value is “q”. The search bar has an auto-suggest slot where the auto-suggest module should be added. 

- **Auto suggest**: The auto suggest module shows the auto suggest results. The results can be textual or immersive. Textual results show only the list of matching product names. Immersive results display the product name, price, and image, in-line for matching products. You can configure the number of results to be shown in auto suggest.

## Author a header

To author a header module, do the following.

1. Create a page fragment with a header module.
1. Populate the header module slots with the respective modules,
1. Update the settings for each module.
1. Save the page fragment. 
1. Check in the page and publish.

To ensure every page renders the header, do the following on every page template created for the site. 

1. Add the header fragment to the header in the main slot of the default page.
1. Save the template. 
3. Check in the template and publish.


