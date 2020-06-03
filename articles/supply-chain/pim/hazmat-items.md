---
# required metadata

title: Hazardous materials in products, orders, shipments, and loads
description: This topic describes how to set hazardous material properties on release products, how to set stock limits on hazardous items, and how to include hazardous materials in a sales order, shipment, or load.
author: dasani-madipalli
manager: tfehr
ms.date: 06/10/2020
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

# ms.search.form:  [Operations AOT form name to tie this topic to]
audience: Application User
# ms.devlang: 
ms.reviewer: kamaybac
ms.search.scope:  Core, Operations
# ms.tgt_pltfrm: 
# ms.custom: [used by loc for topics migrated from the wiki]
ms.search.region: Global
# ms.search.industry: [leave blank for most, retail, public sector]
ms.author: damadipa
ms.search.validFrom: 2020-06-10
ms.dyn365.ops.version: Release 10.0.11
---

# Hazardous materials in products, orders, shipments, and loads

[!include [banner](../includes/banner.md)]

This topic describes how to set hazardous material properties on release products, how to set stock limits on hazardous items, and how to include hazardous materials in a sales order, shipment, or load.

## Set hazardous material specifications for products

Once you have defined a hazardous materials regulation and set up the related reference codes (as described in [Set up hazardous materials](hazmat-setup.md)), you can relate this information to released items. The shipping text for shipping documents will be drawn from the released item hazardous materials information.

As part of associating a released item with a hazardous material, you must specify the regulation code and the material. There could be different regulation codes associated with an item depending on various modes of transport, and you can associate multiple regulations and material codes to each item.

To set up a released product as a hazardous material:

1. Go to **Product Information Management \> Products \> Released Products**.

1. Select or create a product to open its **Released product details** page.

1. Expand the **Manage inventory** FastTab and set **Hazardous material** to **Yes**. This flag identifies the item as a dangerous good and is used when printing shipping documentation.

1. On the Action Pane, open the **Manage inventory** tab and, in the **Compliance** group, select **Item hazardous material**.

1. Fill out the **Item hazardous materials** page for your selected item using the settings described in the following subsections.

### Item hazardous materials header

The following table describes the settings available at the top of the **Item hazardous materials** page.

| **Setting** | **Description** |
| --- | --- |
| **Item number** | This is the released product you are working with. |
| **Regulation code** | Select the hazardous material regulation that applies for this product. The regulation defines how the printed shipping text is created for an item and the associated the delivery methods. Once assigned, the code can't be edited on this page. However, you can assign a new regulation code by selecting the **New** button. |
| **Material code** | Select the hazardous material code that applies for the current product (optional). The material code provides a template with default values for many of the other settings on this page. When you select a code, all its hazardous materials specifications are copied to the current product. The system shows a dialog box asking the user to confirm if they want to default the item material data from material code. |
| **Group code** | Select the hazardous material classification group code that applies for the current product (optional). As with the **Material code**, this setting copies hazardous materials specifications to the current product. The system shows a dialog box asking the user to confirm if they want to default item class group data from group code. |

<a name="hazmat-description"></a>

### Descriptions FastTab

The following table describes the settings available on the **Descriptions** FastTab.

| **Setting** | Description |
| --- | --- |
| **Proper shipping name** | Enter the standard description for the material as specified by the applicable regulation. |
| **Technical name** | Select the common or generic name for the material that may have been established for your company. |
| **N.O.S.** | Mark this as a not-otherwise-specific (N.O.S.) name for the item. N.O.S. shipping names cover groups of similar chemicals and materials with particular end uses that aren't specifically listed by name in the hazmat table. <!-- KFM: A better description is needed here. -->  |

### Item ship text translation FastTab

The **Item ship text translation** FastTab shows a table that displays shipping print text for one or more languages.

| **Column** | **Description** |
| --- | --- |
| **Language** | Shows the language code for the shipping print text used by each row. For example, **en-us** indicates US English. |
| **Shipping print text** | Shows the text defined for the language indicated in each row. |

To create or edit translation, select **Translations** at the top of the table to open **Text translations** page. Then do one of the following:

- To edit an existing translation, select a target language from the **Language** drop-down list and edit the translated text in the **Translated text** column as needed.
- To add a new translation, open the **Add** drop-down list on the Action Pane. Then select the language you wish to add and then enter the translated text in the **Translated text** column.

<a name="material-management"></a>

### Material management FastTab

The following table describes the settings available on the **Material management** FastTab.

| **Setting** | **Description** |
| --- | --- |
| **Class** | Select the hazardous material class that this product belongs to, as defined by the regulation that you are conforming to. Note you must select both a class and a division. |
| **Description** | Displays the description defined for the class selected in the **Class** field (read only). |
| **Division** | Select the hazardous material division that this product belongs to, as defined by the regulation that you are conforming to. The division is a subset of the class. You must assign both a division and class to each product that includes hazardous materials. |
| **Identification** | Select the hazardous material identification code, which is typically based on a United Nations (UN) standard. |
| **Packing group** | Select the packing group that applies for the current item. |
| **Description** | Displays the description defined for the group selected in the **Packing group** field (read only). |
| **Packing Descriptions** | Select the applicable packing description code, which references a description of how the product must be packed. |
| **Hazardous material labels** | Select a code that references the applicable dangerous goods label that should be applied to the product. |
| **Limited quantity** | <!-- KFM: Final description needed from Lachlan -->  |
| **Quantity** | Enter the maximum quantity (in the specified **Unit**) of this product that will be permitted per shipment if you enable the **Limited quantity** option. |
| **Multiplier** | <!-- KFM: Final description needed from Lachlan -->  |
| **Unit** | Select the unit of measure that applies to the specified **Quantity**. This will default to the inventory unit for the item. The quantity limit and hazardous points calculations will convert from this unit to the shipping units as needed based on the conversion rates established in your system. |

### Transport information FastTab

The following table describes the settings available on the **Transport information** FastTab.

| **Setting** | Description |
| --- | --- |
| **Transport category** | Select the related transport category. |
| **Tunnel Code** | Select the related tunnel restriction code for this item. |
| **Hazardous material stowage** | Select the reference code used for sea freight stowage handling when this item is shipped by sea freight |
| **Aircraft type** | Select the aircraft restriction that applies for this material when shipped by air freight. |
| **Packing - cargo aircraft only** | Based on the **Aircraft type**, select the packing instructions code that applies when the product can only be shipped by cargo aircraft. |
| **Packing - passenger and cargo aircraft** | Based on the **Aircraft type**, select the packing instructions code that applies when the product is shipped by either cargo or passenger aircraft. |
| **IATA Star** | A reference to the International Air Transport Association (IATA) dangerous goods list for reference information. <!-- KFM: A better description is needed here. -->  |
| **Emergence response** | Select the code that references instructions for how to handle the material in an emergency. |

### Environmental information FastTab

The following table describes the settings available on the **Environmental information** FastTab.

| **Setting** | Description |
| --- | --- |
| **Environmentally dangerous** | Set this to **Yes** to indicate that this product is environmentally dangerous. Use for your own reporting purposes. |
| **Marine pollutant** | Set this to **Yes** to indicate that this product is a marine pollutant. Use for your own reporting purposes. |

<a name="stock-limits"></a>

## Set stock limits for hazardous products

For safety reasons, you may need to limit the total amount of a given product that can be stocked at a single location. To set stock limits for a released product:

1. Go to **Product information management \> Products \> Released products**.

1. Select a product to open its **Released product details** page.

1. On the Action Pane, open the **Manage inventory** tab and, in the **Compliance** group, select **Reporting details**.

1. Set values for the **Hazardous stock limit** and **Hazardous warning limit** fields, as they apply to your selected product.

The **Hazardous material stock limit report** page lets you monitor the stock levels of the hazardous materials in your warehouse locations to make sure they remain under the established, safe limits established here. For details, see [Hazardous material stock limit report](hazmat-reports.md#stock-limit-report).

## Sales order transactions with hazardous materials

To include a product classified as a hazardous material on a sales order, you must associate the relevant shipping carrier to the sales order. To do this, open the sales order, expand the **Delivery** FastTab, and set the **Shipping carrier** and **Carrier service** as needed.

The shipping carrier is also associated with the mode of delivery, so you must ensure that this information aligns with the hazardous material regulation. This means that the mode of delivery specified on the hazardous material regulation must match the specifications on the sales order header. This connects the regulation, shipping carrier, and service with the shipment lines used on a sales order.

Once a sales order is finalized and ready to be shipped, it can be released to warehouse to indicate the transfer between sales to warehouse operations.

## Shipments with hazardous materials

### View hazardous material scores for each shipment line

When viewing **Shipment details**, you can see the hazardous materials points values calculated for each of the load lines included in that shipment. To view the scores:

1. Go to **Warehouse management \> Shipments \> All shipments**.

1. Select a shipment to open its **Shipment details** page.

1. Inspect the lines in the **Load lines** FastTab, where you can see the scores in the following columns:

    - **Hazardous material points**: This calculation is based on the products that are marked as hazardous material in the released product setup. It will take the quantity on the load line and reference to the multiplier on the released product [material management setup](#material-management).
    - **Limited quantity net weight:** This calculation is based on the products that are marked as hazardous material in the released product setup. It will take the quantity on each load line and reference the weight on the released product [material management setup](#material-management) if this item is marked as limited quantity.

### Check for compatibility among hazardous materials included in a shipment

To check whether all the hazardous materials included in a shipment are suitable to be shipped together:

1. Go to **Warehouse management \> Shipments \> All shipments**.

1. Select a shipment to open its **Shipment details** page.

1. On the Action Pane, open the **Shipments** tab and, in the **Actions** group, select **Compatibility check**.

1. The system returns a message to inform you of the results of the check.

The system evaluates compatibility by checking the compatibility group assigned to each product included in the shipment. For more information, see [Hazardous material compatibility groups](#_Hazardous_material_compatibility).

## Loads with hazardous materials

### View hazardous material scores for each load line

When viewing **Load details**, you can see the hazardous materials points values calculated for each of the load lines included in that load. To view the scores:

1. Go to **Warehouse management \> Shipments \> All loads**.

1. Select a load to open its **Load details** page. (You can also open load details by selecting a link from a related shipment.)

1. In the **Load** FastTab, you can review the total scores for entire load by inspecting the following fields:

    - **Hazardous material points total**: This calculation is based on the products that are marked as hazardous material in the released product setup. It will take the quantity on the load line and reference to the multiplier on the released product [material management setup](#material-management).
    - **Limited quantity net weight:** This calculation is based on the products that are marked as hazardous material in the released product setup. It will take the quantity on the load lines and reference the weight on the released product [material management setup](#material-management) if this item is marked as limited quantity.

1. To review the scores for each individual line, go to the **Load lines** FastTab, which provides values for each line similar to those described for the previous step.

### Check for compatibility among hazardous materials included in a load

To check whether all the hazardous materials included in a load are suitable to be shipped together:

1. Go to **Warehouse management \> Shipments \> All loads**.

1. Select a shipment to open its **Load details** page. (You can also open load details by selecting a link from a related shipment.)

1. On the Action Pane, open the **Loads** tab and, in the **Actions** group, select **Compatibility check**.

1. The system returns a message to inform you of the results of the check.

The system evaluates compatibility by checking the compatibility group assigned to each product included in the load. For more information, see [Hazardous material compatibility groups](hazmat-setup.md#compatibility-groups).
