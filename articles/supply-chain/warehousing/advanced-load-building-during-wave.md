---
# required metadata

title: Set up and use advanced wave load building
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

# Set up and use advanced wave load building

Advanced wave load building automatically assigns shipments to existing waves <!-- do we mean *existing loads*? --> during wave execution, which can help you create meaningful loads that represent trucks without requiring you to use the load-planning workbench. This is useful for businesses who want to use the concept of loads to track and plan the shipment of goods in a truck/trailer, but don't want to manually create these loads each day.

During wave processing, the system normally creates a new load for each shipment that doesn't have a load assigned, but with advanced wave load building, the system instead  assigns each unassigned shipment to an existing load (when an appropriate load exists) and only creates new loads when required. The advanced wave load building feature creates loads automatically based on criteria that you define. You'll set the system up as follows:

- Create *wave templates* that include the new `buildLoads` method, which enables advanced web load building for waves that use those templates.
- Set up *load-build templates*, each of which links to a specific wave template and method. These control which load (existing or new) the load lines being waved will be added to. You can choose to combine or separate shipments based on criteria such as load template, equipment, and other field values on the load line.
- Define *load mix groups* to control which items should and shouldn't be combined on a single load, and choose whether the restriction should produce a warning or an error. You can also choose whether or not to evaluate the volumetric restriction of the load template.

## Enable advanced wave load building on your system

Before you begin trying to set up or use advanced wave load building, you must make sure the feature is available on your system. Administrators can use the [feature management](../../fin-ops-core/fin-ops/get-started/feature-management/feature-management-overview.md) settings to check the feature status and enable it if needed. Here, the feature is listed listed as:

- **Module**: Warehouse management
- **Feature name**: Wave load building feature

<!-- KFM: Add this?: "If you don't see the feature listed here, then it may have become a standard part of the product since this documentation was written, in which case you can proceed with the remaining sections of this topic and all of the described features should be available to you." -->

## Set up advanced wave load building

### Regenerate your wave process methods

You may need to regenerate your wave process methods to make the load building method available. To do this:

1. Go to **Warehouse management** > **Setup** > **Waves** > **Wave process methods**.
2. Check whether **buildLoads** is present in the list. If it isn't, select **Regenerate methods** on the action bar to add it.

### Set up your wave templates

To take advantage of advanced wave load building, you must include the `buildLoads` method in each of your relevant [wave templates](tasks/configure-wave-processing.md) as follows:

1. Go to **Warehouse management** > **Setup** >  **Waves** > **Wave templates**.
1. Select a relevant wave template.<BR>(If you're working with the **USMF** legal-entity demo data, select the **62 Shipping Default** template.)
1. Select **Edit** on the action pane to put the page into edit mode.
1. In the **Methods** FastTab, select the **buildLoads** method from the **Remaining methods** table.
1. Select the right-pointing arrow button between the tables to move the **buildLoads** method to the **Selected Methods** table.
1. Assign a value in the **Wave step code** column for the **LoadBuild** method you just added to the **Selected Methods** table. You can choose any value you want, but take note of it because you'll need it later. More information: [Wave step codes](wave-step-codes.md)<BR>(If you're working with the **USMF** legal-entity demo data, you could enter "WSC2112", which is the value we'll show later in this topic.)

<!-- KFM: Anything more to say about how to pick a wave step code? -->

### Set up your load mix groups

Load mix groups establish rules for which types of items can be combined into a single load. You can set up as many load mix groups as you need, but to use this feature you must have at least one. To create a load mix group:
<!-- KFM: seems like we have no other documentation about load mix groups. Are these added by this feature? Should we say more about them here? -->

1. Go to **Warehouse management** > **Setup** >  **Load** > **Load mix groups**.
1. Select **New** on the action pane to create a new load group.
1. Enter a relevant name for your new group in the **Load mix group ID** field.<BR>(If you're working with the **USMF** legal-entity demo data, enter "TV".)
1. In the **Load mix group criteria** FastTab, select the **New** button to add a row here and then make settings in each column as needed for the new row.<BR>(If you're working with the **USMF** legal-entity demo data, select **TV&Video** in the **Item group** column.) <!-- KFM: We should add a sentence to explain what this will do, as we do later in this procedure. What are all these "code" columns for? -->
1. Select **Save** on the action pane to save your work.
1. In the **Load mix group constraints** FastTab, select **New** to create a new row here and then make settings in each column as needed. <BR>(If you're working with the **USMF** legal-entity demo data, select **CarAudio** in the **Item group** column and **Restrict** in the **Load build action** column. This will prevent items with an item group of **CarAudio** from being on the same load as items with an item group of **TV&Video**.) <!-- KFM: What are all these "code" columns for? -->
1. Continue working with these rules until you have added all the criteria and constraints you need for this load mix group.

### Set up your load build templates

You can set up as many load build templates as you need, but to use this feature you must have at least one. To create a load build template:
<!-- KFM: Again, it seems like we have no other documentation about load build templates. Are these added by this feature? Should we say more about them here? -->

1. Go to **Warehouse Management** > **Setup** >  **Load** > **Wave load building templates**.

1. Select **New** on the action pane to add a new row to the table here. Then make the  following settings for the new row:

    | Setting | Instructions | **USMF** legal-entity demo value |
    |--|--|--|
    | **Sequence** | <!-- KFM: What is this? --> | 1 |
    | **Load build template name** | Enter the name of the template you created or updated previously during this setup. <!-- KFM: Exact? Seems like I get no help --> | 62 Shipping Default <!-- KFM: Or just "62" --> |
    | **Wave step code** | Enter the code you chose for the LoadBuild method when you set up the wave template previously during this setup <!-- KFM: Exact? Looks like a drop-down but offers no values --> | WSC2112 |
    | **Load template ID** | The load template defines maximum weight and volume permitted for the entire load. Select the load template to use for any loads that are created.   <!-- Seems like we have no documentation about load templates. --> | Stnd Load Template |
    | **Equipment** | <!-- KFM: This setting is offered, but you didn't mention it. Should we? --> |  |
    | **Load mix group ID** | The mix group establishes rules for which types of items can can't be combined in a single load. Select one of the mix groups that you created previously during this setup. | TV |
    | **Use open loads** | Choose whether to allow existing loads to be used (any or none) | Any |
    | **Create loads** | Choose whether to create a new load if no existing loads match the criteria. <!-- KFM: Which criteria? What happens if this is "no" and we don't have a match? --> | Yes (selected) |
    | **Allow shipment line split** | Choose whether to allow a single line to be split across multiple loads if the full line exceeds the load capacity. <!-- KFM: What happens if this is "no" and we are over capacity? --> | No (unselected) |
    | **Validate volumetrics** | Choose whether to evaluate the volumetric limits of the specified load template. <!-- KFM: Does the load template do anythign if this is set to "no"? What happens if this is "yes" and the check fails? --> | No (unselected) |

1. Select **Edit query** on the action pane to open a flyout for editing the query.

1. Open the **Sorting** tab in the flyout and select the **Add** button to add a new row here. Configure the row to define the sorting rules you want to use, for example by entering the following: <!-- KFM: It's not clear to me what we are doing here. -->

    - **Table**: Load details
    - **Derived table**: Load details
    - **Field**: Order number
    - **Search direction**: Ascending

1. Select **OK** to save your changes and close the flyout.

1. In the **Break by** FastTab, set rules to control how your loads will be split up. You might typically use this to break on custom fields that have been extended onto the load line, such as Route, Tour, Run, etc. For example, to create one load per order number, select the **Break by** check box for the row with the following values:

    - **Reference table name**: Load details
    - **Reference field name**: Order number

## Example scenario

This scenario shows how the settings previously described in this topic will affect warehouse operations while processing a sales order. This scenario uses the **USMF** legal-entity demo data combined with other demo values provided in these setup instructions.

1. Go to **Sales and Marketing** > **Sales orders** >  **All sales orders**.
1. Select **New** on the action pane to open a flyout for creating a new sales order.
1. In the flyout, make the following settings:
    - On the **Customer** FastTab, set **Customer account** to "US-007".
    - On the **General** FastTab, set **Warehouse** to "62".
1. Select **OK** to create the sales order and close the flyout.
1. Your new sales order opens. It should include a new, empty line in the **Sales order lines** table. For this new line, set the **Item number** to "A0001" and the **Quantity** to "1".
1. Open the **Inventory** drop-down list at the top of the **Sales order lines** table and select **Reservation**. <!-- KFM: How do I "reserve inventory to the line" here, just edit the **Reservation** column? -->
1. Select the close (X) button in the upper-right corner to return to your sales order.
1. Open the **Warehouse** tab on the action pane and then select **Actions** > **Release to warehouse** here. The system creates a shipment and adds it to a new load because there is no existing load that contains load lines with this order number. <!-- KFM: Where is a good place to go to confirm this? -->
1. Return to the sales order you just set up. In the **Sales order lines** FastTab, select **Add line** to add another line to your sales order. This time add **Item number** "A0002" with a **Quantity** of "1". 
1. Reserve the line and release the order to the warehouse, as you did previously.  The system now creates a new shipment for the new line, but because you are using advanced wave load building, it adds that shipment and load line to the existing wave. Without this feature, a new load would have been created for the shipment.
1. Create a third line for the same sales order, this time for **Item number** "M9200" with a **Quantity** of "1". Reserve the line and release the order to the warehouse. As before, a new shipment is created, but because this item is from the **CarAudio** item group, it fails to pass the load mix group constraints we set up earlier and is therefore added to a new load. If a load mix group hadn't been specified on the load build template, then this shipment would have been added to the first load as well. <!-- KFM: It seems like I can't reserve this item (none in warehouse?). Does the demo data really support this example? -->
