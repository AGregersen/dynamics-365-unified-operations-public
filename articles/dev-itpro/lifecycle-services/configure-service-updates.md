---
# required metadata

title: Configure service updates through Lifecycle Services (LCS)
description: This topic explains how to specify how and when you receive service updates for your environments.
author: manalidongre
manager: AnnBe
ms.date: 03/05/2019
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

# ms.search.form: 
# ROBOTS: 
audience: Developer, IT Pro
# ms.devlang: 
ms.reviewer: sericks
ms.search.scope: Operations
# ms.tgt_pltfrm: 
# ms.custom: 
ms.search.region: Global
# ms.search.industry: 
ms.author: manado
ms.search.validFrom: 2019-3-31 
ms.dyn365.ops.version: Platform update 24 

---

# Configure service updates through Lifecycle Services (LCS)

[!include [banner](../includes/banner.md)]

[!include [banner](../includes/coming-soon.md)]

In Microsoft Dynamics Lifecycle Services (LCS), you can specify how and when you receive service updates from Microsoft for your Microsoft Dynamics 365 for Finance and Operations environments.

> [!IMPORTANT]
> This feature is available only to customers who are using **Microsoft Dynamics 365 for Finance and Operations version 8.1 (October 2018) and later**, and who are **not** part of the [First release](../../fin-and-ops/get-started/public-preview-releases.md) program. Microsoft is working to make the feature available to First release customers and customers who use older versions of the product. 

Only users (customers or partners) who are assigned to the **Project owner** role in LCS can configure updates. Additionally, updates can be configured only for **implementation projects**.

Follow these steps to change your update settings.

> [!NOTE]
> These settings apply only to service updates. They have no effect on the operating system–level security updates that are applied to your environments every month.

1. In LCS, in your implementation project, open the **Project settings** page.

    This page has a new tab that is named **Update settings**.

2. On the **Update settings** tab, set the following configuration options as you require:

    - **Update environment** – Select an alternate sandbox environment that should be updated before the production update.

        By default, Microsoft first updates the Tier 2 Standard Acceptance Test (sandbox) environment that is included in the base offer. It then applies the update to the production environment. If you've purchased Tier 2 and higher sandbox add-on environments and want a different sandbox to be updated, you can use this field to change the default environment to an alternate environment.

        > [!IMPORTANT]
        > The environment that you select here will be updated seven calendar days before the update cadence that is selected for the production environment.

    - **Production environment update cadence** – Select a recurring cadence for updates to your production environment. The sandbox environment that is selected in the **Update environment** field will be updated seven calendar days before the selected cadence. The following options are available:

        - **Select the cadence** – Select whether to receive updates in the first, second, or third week of the month.
        - **Select one of the three time-zones** – Select the time zone that the production environment should be updated in: Eastern Time (UTC – 5), Hong Kong Time (UTC + 8), or Greenwich Mean Time (UTC + 0).
        - **Select a day of the week:** Select the day in the week when you want to receive updates.
        - **Select a time slot:** Select the time slot when you want to receive updates.

        > [!NOTE]
        > Currently, only a few options are available for the day of the week and time slot options. Microsoft will add more options soon, such as weekdays for customers.

    After you set the update environment and update cadence, Microsoft generates an update calendar for the next six months. This calendar shows exactly when the configured sandbox and production environments will be updated. Therefore, you will know when to expect each update. To view the calendar, select the **View update calendar** link under the **Production environment update cadence** options.

3. When you've finished setting the configuration options, select **Save**.

    > [!IMPORTANT]
    > After the settings are saved, you can change them at any time. However, if there is an ongoing rollout, the new settings won't be used to update the existing rollout timings. Instead, they will start to be used in the next rollout. An ongoing rollout is defined by the 14-day period between the date when the email notification about the update of the sandbox environment is sent and the date when the production environment is updated.

For more information about how to pause updates to configured sandbox and production environments, see [Pause service updates through Lifecycle Services (LCS)](pause-service-updates.md).

For more information about One Version and Microsoft-managed service updates, see [One Version service updates FAQ](../../fin-and-ops/get-started/one-version.md).
