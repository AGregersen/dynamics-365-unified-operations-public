---
# required metadata

title: Feature management overview
description: This topic describes the Feature management feature and how you can use it.
author: mikefalkner
manager: AnnBe
ms.date: 03/21/2019
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

# ms.search.form:  [Operations AOT form name to tie this topic to]
audience: IT Pro, Application user
# ms.devlang: 
ms.reviewer: sericks
ms.search.scope: Operations, Core
# ms.tgt_pltfrm: 
# ms.custom: [used by loc for topics migrated from the wiki]
ms.search.region: Global 
# ms.search.industry: [leave blank for most, retail, public sector]
ms.author: mfalkner
ms.search.validFrom: [month/year of release that feature was introduced in, in format yyyy-mm-dd]
ms.dyn365.ops.version: 10.0.2
---

# Feature management overview

[!include[banner](../../includes/banner.md)]

Features are added and updated in every release of Microsoft Dynamics 365 for Finance and Operations. The Feature management experience provides a workspace where you can view a list of features that have been delivered in each release. By default, new features are turned off. You can use the workspace to turn them on and view the documentation for them.

## The Feature management workspace

You can open the **Feature management** workspace from the **Workspaces** menu. When you select the workspace icon, you will see a page that shows a list of features for all releases that are supported by the Feature management experience. Over time, Microsoft will enhance the Feature management experience so that it includes additional functionality to help you manage features.

The feature list includes the following information:

- **Feature name** – A description of the feature that was added.
- **Enabled status** – A symbol indicates whether a feature has been enabled (check mark), is not enabled (blank), has been scheduled to be enabled (clock), or is mandatory enabled (lock). The setting that is shown here is used for all legal entities. Note that even when a feature has been turned on, it's still controlled by security. Therefore, the feature will be available only to users who have access to it, based on their security role. It will also be available only for legal entities that the user has access to.
- **Enable date** – The date when the feature was turned on or will be turned on if the date is a future date.
- **Feature added** – The date when the feature was added to your environment. This date is automatically entered when you update your environment during the monthly release cycles.
- **Module** – The module that is affected by the new feature.

When you select a feature, additional information appears in the details pane to the right of the feature list. At the top of the pane, you will see the feature name, the date when the feature was added, the module that is affected by the feature, and a **Learn more** link. Select this link to view the documentation for the feature. If documentation isn't available, you will be taken to a temporary page. The details pane also includes a **Comments** field where you can add your own comments about the feature.

The **Feature management** workspace also contains several tabs with a list of features in it. 
- **New** - show all features that have been added since the last monthly update. If you have skipped any monthly updates, it will contain all of the new features since the last time you updated. The newest features appear at the top of the list. The total number of new features is also shown in a tile at the top of the page.
- **Not enabled** - show all features that have not been enabled. The newest features appear at the top of the list. The total number of new features is also shown in a tile at the top of the page.
- **Scheduled** - show all features that have been scheduled to be enabled on a future date. The features that have the earliest scheduled date will appear at the top of the list. The total number of new features is also shown in a tile at the top of the page.
- **All** - show all features. The newest features appear at the top of the list.


## Enable a feature

If a feature hasn't been enabled, an **Enable** button appears in the details pane. You can use this button to enable the feature.

1. Select the feature that you want to enable, and then, in the details pane, select **Enable**.
2. A slider appears, where you can specify the date on which the feature should be enabled. By default, this date is set to the current date.
3. Select **Enable** to enable the feature.

Some features can't be enabled after you enable them. If the feature that you are attempting to enable can't be disabled, you receive a warning. At this point, you can cancel the operation and leave the feature disabled. However, if you decide to enabled the feature, you won't be able to enable it later.

After the feature is enabled, a message appears below the **Learn more** link in the details pane. This message either states that the feature was enabled or indicates when the feature will be enabled in the future. If you use a future date, the feature will show up in the **Scheduled** list. This message will appear every time that you select the feature in the feature list. 

## Reschedule a feature

If a feature has been enabled in the future, a **Reschedule** button appears in the details pane. You can use this button to change the **Enable date** to a different date.

1. Select a scheduled feature that you want to reshedule, and then, in the details pane, select **Reschedule**.
2. A slider appears, where you can specify the date on which the feature should be enabled. 
3. Select **Reschedule** to reschedule the feature.

## Disable a feature

If a feature has already been enabled, a **Disable** button appears in the details pane. You can use this button to disable the feature. The **Disable** button isn't available if the feature can't be disabled after it is enabled.

- Select the feature that you want to turn off, and then, in the details pane, select **Disable**.

    A dialog box appears, and the date when the feature was set to be enabled is deleted.

After the feature is disabled, a message appears below the **Learn more** link in the details pane. This message states that the feature hasn't yet been enabled and it will appear in the **Not enabled** list. The message will appear every time that you select the feature in the feature list.

## Features that must be enabled

A critical feature may be delivered that must be enabled automatically when you do an update. It will be enabled automatically on the **Enable date**. If the **Enable date** is in the future, you can override the date by changing the **Enable date** to an earlier date so that it takes effect on an earlier date. You cannot move the date farther into the future than the original enable date that was shown when the feature was added.

For features that must be enabled, a message will appear below the **Learn more** link in the details pane. This message will state that the feature was enabled or will be enabled automatically on the **Enable date**. It will appear every time that you select the feature in the feature list.

## Assigning roles

The **Feature management** workspace can be opened by system admins, and by users who are assigned to the **Feature manager** or **Feature viewer** roles that were created to support the Feature management experience. Users in the **Feature manager** role can turn any feature on and off. They can also update the comments section for the feature. Users in the **Feature viewer** role can only view the **Feature management** workspace. They can't turn features on and off.

The **Feature manager** and **Feature viewer** roles don't override the existing security that a user has. The role just controls access to turning features on and off. It doesn't provide access to the features themselves.
