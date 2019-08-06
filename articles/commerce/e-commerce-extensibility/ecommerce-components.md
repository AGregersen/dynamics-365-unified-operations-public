---
# required metadata

title: E-Commerce components
description: This topic contains a high-level summary of some frequently used e-Commerce configuration components that the e-Commerce software development kit (SDK) provides access to in Microsoft Dynamics 365 for Commerce.
author: SamJarawan
manager: annbe
ms.date: 08/30/2019
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 

# optional metadata

# ms.search.form: 
audience: Developer
# ms.devlang: 
ms.reviewer: josaw
ms.search.scope: Retail, Core, Operations
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: SamJar
ms.search.validFrom: 2019-08-30
ms.dyn365.ops.version: 

---
# E-Commerce components

This topic contains a high-level summary of some frequently used e-Commerce configuration components that the e-Commerce software development kit (SDK) provides access to in Microsoft Dynamics 365 for Commerce.

## Modules

Modules represent the core building blocks that make up an e-Commerce page. Here are some examples of modules:

- A feature module that is featured on a page, and that shows a product image and description, together with a "call-to-action" button that can be used to purchase the product or get more information about it
- A hero module that highlights a campaign or provides marketing information
- A header module that is made up of smaller module components, such as a search module, a sign-in module, and a navigation module

## Module configuration fields

Each module can expose configuration fields that are surfaced on the authoring page. The configuration fields are typically used for module settings or layout options. For example, you can use an image alignment field that lets the page author set the alignment to the left, center, or right inside the module. You can also use a title string to show a heading in a module.

The module code reads the field value and creates the appropriate HTML in the view. Multiple types of values are supported, such as Boolean values, numbers, strings, rich text, enumerators, images, and videos.

## Data actions

Data actions are used to get data and apply business logic to a module.

### Core data actions

The e-Commerce platform includes a set of data actions for performing typical actions, such as getting product data from the Dynamics 365 for Commerce database, or getting ratings and reviews information for a product. Core data actions can't be modified.

### Custom data actions

You can create custom data actions and use them in your modules. Custom data actions can be globally scoped so that they can be used across multiple modules or in a single module. Core data actions can call Dynamics 365 for Commerce proxy application programming interfaces (APIs), or any other service provider, to get retail data. Custom business logic can be applied as required or call any web service.

## Themes

Themes contain site Cascading Style Sheets (CSS) style definitions. They also let you add custom module CSS style definitions. You can set a site theme in the authoring tools. All pages will then use that theme by default. You can add additional themes and set them either on a master or shared template, or on a specific page. This capability is useful if you want to change the theme for a campaign or a temporary seasonal change. You can set the theme on the whole site or a subset of pages.

## Script injectors

The e-Commerce platform provides a built-in script injector module that makes it easy to inject scripts into the head, bodybegin, and so on, from the admin tool. Script injectors make it easy to add scripts such as third-party analytics. You might have advanced requirements to use custom script injector modules to inject custom HTML into your e-Commerce site.
