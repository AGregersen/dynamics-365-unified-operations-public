---
# required metadata

title: CSS override file uploads
description: This topic describes why, when, and how to use CSS override file uploads within the e-commerce authoring toolset.
author: Nick Holman
manager: Brendan Sullivan
ms.date: 11/20/2019
ms.topic: article
ms.prod: 
ms.service: dynamics-365-commerce
ms.technology: 

# optional metadata

ms.search.form:  
audience: Application User
# ms.devlang: 
ms.reviewer: josaw
ms.search.scope: 
# ms.tgt_pltfrm: 
# ms.custom: 
ms.search.region: Global
ms.search.industry: retail
ms.author: phinneyridge
ms.search.validFrom: 
ms.dyn365.ops.version: 

---
# CSS override file uploads

## Overview

Under normal circumstances, permanent site styles should be handled directly through a site's theme.  Themes are created using the SDK and deployed to your websites through LCS.  They provide the foundational CSS and style contracts for modules within any given page on your site.  Theme debugging capabilities and module interface contracts within the SDK help site developers create customizable and cohesive site design packages.  When these design packages are deployed to a site, they enable no-code Site Builder personas to focus on *content* creation, editing, and publishing.  

With the normal lifecycle of a theme in mind, there are specific scenarios when this dependency on developers to make quick style changes through the SDK and LCS deployment pipeline can be prohibitive.  Site prototypes or hotfixes can feel cumbersome if you don't have the SDK configured, or don't have time to wait for an LCS deployment.  This is where .CSS file override uploads can help.  Within the Site Builder tool, authenticated users can directly upload CSS files, preview them, and choose one to override their site's theme without the overhead of SDK or LCS deployment.   This override file can be as small as a single text style change, or if desired, a complete brand overhaul.  The caveats to this approach are this: 

a) only *one* override file can be active on a site at any one time (in other words, all active overrides must be present within a single file).

b) You can preview override changes in Site Builder.  But beyond this, there are no dedicated debugging features to identify bugs introduced by the override (in other words, you do not have the same toolset afforded within the SDK to validate module and authoring contracts).

With these caveats in mind, CSS file overrides can be a quick way to prototype a design or implement a hotfix before a full theme update and deployment.  In the section below, let's look at how to use this capability within Site Builder.

## Create your own CSS override file

You can use any IDE, text editor, or other tool to create your .CSS file.  A common approach is to use standard web debuggers in your browser to identify style selectors, properties, and values within your existing site.  Most browsers will let you change values and preview them within the debugger.  Once you have identified the changes you wish to make, you can save these overrides to your own .CSS file.   

## Upload your .CSS override file

To upload your .CSS file to your site, follow these steps:

1. Navigate to your site within Site Builder.

2. In the navigation pane on the left, select **Design**.

    >[!Note]
    >Depending on your Site Builder version, you may first need to expand **Settings** in the navigation panel to unhide **Design**.
    
3. If it is not already selected, select the **CSS override** tab at the top of the main design pane.
4. Click the **Upload CSS file** button under the **Available CSS overrides** view.

5. Choose a.CSS file from the file picker modal and click **Open**.

Your newly uploaded CSS file will appear as a card in the **Available CSS overrides** view.

## Preview a .CSS override file

To preview a .CSS override file before making it active on your live site, follow these steps:

1. In the **Design > CSS override > Available CSS overrides** view, find the card for the file you would like to preview.
2. Click the **Preview site** button on the desired card.
3. In the URL picker dialog that appears, choose a site URL that you would like to begin previewing with the override applied.
4. If there are multiple variants for the selected URL, choose the desired variant in the subsequent variant picker modal.
5. A new browser tab or window will open where you can validate your style overrides against your site.  This URL can be shared with other authenticated Site Builder users for review and feedback.

## Make a .CSS override active on your live site

After you have previewed your site with a style override file, you can set it active against your live site.  

>[!NOTE]
>Only one .CSS override file can be active on your site at a time.  Activating a new override will deactivate the previous one, so be sure that all necessary overrides are present in a single file.
To activate a .CSS override file, follow these steps:

1. In the **Design > CSS override > Available CSS overrides** view, find the card for the file you would like to activate.
2. Click the **Activate** button on the desired card.
3. This will immediately set the override active on your live site.

## Deactivate a .CSS override on your live site

To deactivate a .CSS override from your site, follow these steps:

1. In the **Design > CSS override > Active CSS override** view, find the active style override card that you wish to deactivate.
2. Click the **Deactivate** button on the active override card.
3. This will immediately deactivate the .CSS override for your site.

>[!TIP]
>On any of the .CSS cards, click the elipse (...) button to show additional controls. For quick modifications, the "Download" and "Replace" options are useful for quick modifications to an existing override file.
