# Overview
Ratings and Reviews on eCommerce website helps consumers (C2) directly to understand how a product is perceived by fellow consumers and make a purchase decision. eCommerce website is also a primary source for receiving ratings and reviews on a product. This document explains how to configure your eCommerce website and pages to show ratings and reviews.

## Site configuration  

There are some values like Ratings and Reviews Service endpoint, review text length etc. are configured at site level. The following explains on how to configure those values. 

	1. Go to ….. Tool
	2. Got to Site Setting 
	3. Configure Ratings and Reviews Service endpoint as https://<tenanteID>.rnr.ms/
	4. Configure Review text length value (maximum 1000 characters) 
	5. Configure Review Title max length (maximum 55 characters) 

Refer to the below screenshot for more details:

![eCommerce site settings - Ratings and Reviews ](media/rnr-eCommerce-site-appsettings.png)

![eCommerce site settings - Ratings and Reviews ](media/rnr-eCommerce-pdp-reviews-modules_design.png)
![eCommerce site settings - Ratings and Reviews ](media/rnr-eCommerce-pdp-reviews-modules.png)




## Product details - buy box configuration  

On product details page, rating summary is showed below the product title. Rating summary also can be a link to reviews section on the product details page. To make rating summary as a link to reviews list, use the following steps:  

	1. Go to product details page template 
	2. Go to Buy box container module settings
	3. Choose Product ratings module under Buy box, then check "Link the click to full reviews module"
	

Refer to the below screenshot for more details:
![eCommerce site settings - Ratings and Reviews ](media/rnr-eCommerce-buy-box-rating-summary.png)

##Ratings and review on product details page (PDP) 

Ratings summary is showed across the sites in the products placement lists, category lists, and search results etc. Ratings summary along with review list will be showed on product details page, also allows consumers to submit a rating and review on a product on product details pages.  There are multiple modules those needs to be configure to show ratings summary, write review, and reviews list on product details page as follows:

	1. Write review module 
	2. Product reviews list module 
	3. Ratings histogram  module 

Refer to the below screenshot for more details on how the ratings and reviews modules are structured on product details page :

![eCommerce site settings - Ratings and Reviews ](media/rnr-eCommerce-pdp-reviews-modules_design.png)

### Write review module 
Write review module allows users to sign-in, give a rating, and write a review on a product. The same module also allows users to edit the previously given rating and review.  This module is typically placed above the Reviews list and Rating histogram modules on product details page.



| Property name     | Values                                                       | Property Description                                         |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Name             | Write review                                                   | This is name of the "Write review" module|


### Product Reviews list module 
Product reviews module is used to display list of product’s reviews along with sort, filter, and pagination options. This module is typically placed on product details page.



| Property name     | Values                                                       | Property Description                                         |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| review shown on each page             | 10                                                   | Count of reviews to be showed in a pagination model. User will see next and previous buttons to paginate through the reviews. |




### Ratings histogram module 
Ratings histogram module shows ratings summary and histogram of a product’s rating. This module is typically placed above the Product Review List module on product details page.

This module has no additional configurations required, apart from adding it within the Reviews list module. 


Refer to the below screenshot for more details on how Template would look like with ratings and reviews modules on product details page:

![eCommerce site settings - Ratings and Reviews ](media/rnr-eCommerce-pdp-reviews-modules.png)

