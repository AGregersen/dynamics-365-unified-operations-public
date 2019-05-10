---
# required metadata

title: Abort an executing batch job
description: This topic provides information about how cancel an executing batch job in Microsoft Dynamics 365 for Finance and Operations.
author: hasaid
manager: AnnBe
ms.date: 05/08/2019
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 

# optional metadata

# ms.search.form: 
# ROBOTS: 
audience: IT Pro
# ms.devlang: 
ms.reviewer: kfend
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
ms.custom: 62333
ms.assetid: 6135bcf7-bf8f-42ae-b2c6-458f6538e6a4
ms.search.region: Global
# ms.search.industry: 
ms.author: hasaid
ms.search.validFrom: 2019-05-08
ms.dyn365.ops.version: Platform update 27

---

# Abort an executing batch job
[!include [banner](../includes/banner.md)]

[!include [banner](../includes/preview-banner.md)]

Sometimes canceling a batch job can take a long time if already executing tasks will take a long time to finish. The abort option provides a system administrator or batch job manager with the ability to abort already executing tasks for jobs which are in the process of being canceled. This provides a much faster mechanism to cancel a long running job which is impacting system usage elsewhere.

>[!NOTE]
> It is important to note that this feature should be used with caution. When you cancel a running process, it is an inherently unsafe action that can lead to data corruption, resulting in either orphaned or incomplete data. This action should only be used to mitigate other issues caused by the running tasks.

Complete the following steps to immediately cancel the running task.

1. Go to **System administration** \> **Inquiries** \> **Batch jobs**.
2. Select a batch job that has a **Status** of **Canceling**.
3. On the **Batch tasks** tab, select **Abort** on the task , and then click **OK**.

    ![Abort Batch Task](./media/batch-abort.PNG) 
