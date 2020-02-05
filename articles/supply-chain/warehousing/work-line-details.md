---
# required metadata

title: Work line details
description: Advanced wave load building automatically assigns shipments to existing waves during wave execution, which can help you create meaningful loads that represent trucks without requiring you to use the load-planning workbench.
author: mirzaab
manager: AnnBe
ms.date: 02/01/2020
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

# ms.search.form:  [Operations AOT form name to tie this topic to]
audience: Application User
# ms.devlang: 
ms.reviewer: kamaybac
ms.search.scope:  Retail, Core, Operations
# ms.tgt_pltfrm: 
# ms.custom: [used by loc for topics migrated from the wiki]
ms.search.region: Global
# ms.search.industry: [leave blank for most, retail, public sector]
ms.author: mirzaab
ms.search.validFrom: 2020-02-01
ms.dyn365.ops.version: Release 10.0.8
---

# Work line details

The **Work line details** page shows a comprehensive, sortable, and filterable list of the individual work lines in your system. It provides all the information needed to get a complete overview of the work being planned and executed in the warehouse. You can easily switch between viewing all work lines or only the open work lines. Details provided for each line include: work status, item number, location, work quantity, load ID, shipment ID, and more.

## Enable the location directive inventory picking aging feature

Before you can use this feature, it must be enabled on your system. Administrators can use the [feature management](../../fin-ops-core/fin-ops/get-started/feature-management/feature-management-overview.md) settings to check the feature status and enable it if needed. Here, the feature is listed as:

- **Module** - Warehouse management
- **Feature name** - Work line details

## Open and use the Work line details page

To view the list or work line details, go to **Warehouse management > Work > Work line details**. From here you can do the following:

- Use the **Filter** field to search for lines having a specific value for any available parameter (including many parameters that aren't shown as columns in the table)
- Use the **Show closed** check box to choose to show or hide closed lines
- Select **Display dimensions** to open the **Dimensions display** pane, where you can choose to show or hide various dimension columns in the table.
- Select any column heading to to open a menu where you can choose to sort or filter the list by values in that column
- Select a work line and then select **Change location** to change the location for that work line (which will override the location directive setup)
- Select a work line and then select **Cancel work line** to open a pane where you can partially or fully reduce the quantity of that work line
- Adjust quantities <!-- KAMAYBAC: seems like we can only reduce quantities. Is that right? If so, the above point covers this. -->
- View transactions behind any work line  <!-- KAMAYBAC: What does this mean? How do we do this? -->

## Try out the feature

This section provides a three-part example of how to work with work line details.

<!-- KAMAYBAC: I think we should consider removing this demo. It seems hard to set up, and doesn't really show anything that isn't already easy to understand in the list provided above. Though the extra details about what happens when changing quantities should be clarified and kept.  -->

### Enable sample data

To work through this demo using the sample records and values specified here, you must be on a system with the standard [demo data](../../fin-ops-core/dev-itpro/deployment/deploy-demo-environment.md) installed, and you must select the **USMF** legal entity before you begin.

You can also use this demo as guidance for how to use this feature when working on a production system, but then you must then substitute your own values, and you may be missing some types of required records that would otherwise be provided by the standard demo data.

### Make sure the demo setup includes enough available inventory

If you are working with **USMF** demo data, then start by making sure your system is set up with enough inventory at each relevant pick location. This demo expects that you have the following inventory available:

- **Item M9200** - 45 ea. (or more)
- **Item M9202** - 10 ea. (or more)

To confirm that you have enough inventory available and make adjustments as needed:

1. Go to **Warehouse management > Setup > Location directives** and find out which picking locations are used for sales order picking at warehouse 51 (see also [Control warehouse work by using work templates and location directives](control-warehouse-location-directives.md)). <!-- KAMAYBAC: What am I looking for here? How can I use this? -->
1. Check the inventory levels at the relevant locations. <!-- where/how do I do this? Can we give a link? -->
1. Adjust inventory as required. You can create manual movements, use replenishment, or apply any other flow as needed to adjust the inventory. <!-- where/how do I do this? Can we give a link? -->

### Part 1: Create picking work

Before you start creating work, make sure that your warehouse is set up to respond to work requests as expected. <!-- where/how do I do this? Can we give a link?-->

Create some picking work by doing the following:

1. Go to **Accounts receivable > Orders > All sales orders**.
1. Select **New** to open the **Create sales order** pane.
1. In the **Create sales order** pane, make the following settings:
    - On the **Customer** FastTab, set **Customer account** to "US-001".
    - On the **General** FastTab, set **Warehouse** to "51".
1. Select **OK** to create the sales order and close the pane.
1. Your new sales order opens. It includes a new, empty row in the **Sales order lines** table. For this order line, set **Item number** to "M9200", **Quantity** to "20" and **Unit** to "ea".
1. Select the new order line, open the **Inventory** drop-down list and select **Reservation**.
1. The **Reservation** page opens. Select **Reserve lot** to reserve your selected line's full quantity in the warehouse.
1. Close the **Reservation** page to return to your sales order.
1. Open the **Warehouse** tab and select **Release to warehouse**. The system creates a shipment, adds it to a new load, and creates the required work.
1. Create a second sales order for the same **Customer account** and **Warehouse** as before. Add the following two order lines to this order:
    - Line 1: **Item number** "M9200", **Quantity** "25", **Unit** "ea"
    - Line 2: **Item number** "M9202", **Quantity** "10", **Unit** "ea"
1. As you did previously, reserve the inventory for each of these two order lines (one at a time) and then release the order to warehouse.

### Part 2: Change the location for a work line

Navigate to _Warehouse management_ - _Work_ - _Work line details_ and open the form.

Select a work line and click on &#39;Change location&#39; in the action bar. Enter the new location that should be associated with the work line. If the location you selected has available inventory (for a pick) or if it matches the location type validation (for a put), the location on the work line will be updated.

### Part 3: Cancel a work line

Navigate to _Warehouse management_ - _Work_ - _Work line details_ and open the form.

Select a work line and click on &#39;Cancel work line&#39; in the action bar. Cancel full quantity for this example but be aware that you can also cancel only part of the quantity.

Note that the first Pick work line has been cancelled.

Let&#39;s continue with this example and cancel only a partial quantity of the second pick line. Select the second line on the Work line details form and press &#39;Cancel work line&#39;. In the new screen, specify qty 7ea.

Now, the new line will have qty 3, as we have cancelled 7ea (10ea - 7ea).

Note that only the Work created quantity field on the matching Load line will be changed as a result. The user must take other measures to remove the obsolete quantity from the load line, otherwise it won&#39;t be possible to be ship confirmed (unless under delivery is set up correctly).
