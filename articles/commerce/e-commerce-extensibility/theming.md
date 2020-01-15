---
# required metadata

title: Theming overview
description: This topic presents an overview of online site theming in Microsoft Dynamics 365 Commerce.
author: samjarawan
manager: annbe
ms.date: 10/01/2019
ms.topic: article
ms.prod: 
ms.service: dynamics-365-commerce
ms.technology: 

# optional metadata

# ms.search.form: 
audience: Developer
# ms.devlang: 
ms.reviewer: v-chgri
ms.search.scope: Retail, Core, Operations
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: samjar
ms.search.validFrom: 2019-10-31
ms.dyn365.ops.version: Release 10.0.5

---
# Theming overview

[!include [banner](../includes/preview-banner.md)]
[!include [banner](../includes/banner.md)]

This topic presents an overview of online site theming in Microsoft Dynamics 365 Commerce.

## Overview

Dynamics 365 Commerce lets you apply a theme to your whole online site, individual templates, or individual pages.  For example, you might have a default theme that is set for the whole online site and also a campaign theme that is applied only to a subset of pages on the site. 

Theme's are made up of Sassy Cascading Style Sheets (SCSS) files to style your site and modules, and optionally may also contain module view and definition extensions allowing modules to render different views based on the theme selected. 

After a theme is created and uploaded to your production site, the site builder tool can be used to set the theme for the site. You can set the site's theme in a template, in a layout, or on a single page. When an online page is rendered, the appropriate theme is applied. Therefore, all the modules on that page have a consistent look and feel.  The site builder tool also allows addional CSS overrides to be uploaded to make changes on top of a selected theme if needed.

The following illustration shows how a theme is selected for a page in Dynamics 365 Commerce. Notice that the page container (**Default page**) is selected, and the **Theme** field for the page appears in the properties pane on the right.

![Theme selection](media/theming-1.png)

A theme can be set on the master page in a similar manner. In this case, the theme is applied to all pages that are derived from the master page. Note that if the **locked** property is turned off, individual pages can override the theme.

## Best practices

* There is no limit to the number of SCSS files that your theme can contain.
* Your theme entry point can import other SCSS files by using relative paths.
* Starter kit modules are built by using Bootstrap 4 classes. Therefore, we recommend that every theme include either Bootstrap 4 or Bootstrap 4 RTL as the  SCSS framework.
* If you want to take advantage of starter kit modules that are built by using Font Awesome glyph icons, **font-awesome** should be included in the SCSS file. The following example shows how to include **font-awesome** in a SCSS file:

```
$fa-font-path: 'https://use.fontawesome.com/releases/v5.2.0/webfonts' !default;
@import "bootstrap/scss/bootstrap";
...
```

## Consume SCSS files that are distributed by using Node Package Manager

Some dependencies, such as Bootstrap and Font Awesome, are distributed by using Node Package Manager (npm) packages. If these dependencies are used in your SCSS file, they must also be referenced in the packages.json file for your software development kit (SDK).

To meet this requirement, edit the **packages.json** file in the root folder of the SDK, and add references for the dependencies. In the following example, a reference has been added for the Bootstrap dependency.

```
"dependencies": {
    …
    "bootstrap": "^4.3.1",
    …
}
```

## Recommended structure for a custom theme

This section shows the recommended structure for any custom theme. 

Import or define the following items:

* Fonts and glyph icons
* Mixins and functions:

    * **Bootstrap:** Dependencies, excluding components and utilities
    * **Shared components:** Dependencies, excluding components and utilities
    * Custom theme mixins and functions

* Theme variables:

    * Custom theme variables
    * **Bootstrap:** Default theme variables (fallbacks)

* SCSS for components and modules:

    * **Shared components:** Components
    * Custom components and modules

* Utilities:

    * Bootstrap, shared component, and custom utilities

## Hooks for module theming

For every module, a class name is defined that matches the module name. In this way, any theme can target the module. This class name should be the first class name that is applied to the outermost element that is rendered by the React component. To allow for more granular theme options, developers can provide additional class names on elements or features of a module. In that way, custom themes can target those elements or features.

## Custom themes

Custom themes can be created using the Dynamics 365 online SDK and stored within the **/src/themes/** folder.  For more information see [Create a theme](create-theme.md).

## Additional resources

[Create a new theme](create-theme.md)

[Configure theme settings](configure-theme-settings.md)
