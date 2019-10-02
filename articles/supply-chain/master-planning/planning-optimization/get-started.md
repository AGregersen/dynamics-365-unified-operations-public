---
# required metadata

title: Get started
description: Get started with Planning Optimization. 
author: ChristianRytt
manager: AnnBe
ms.date: 2019-09-06
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

ms.search.form: ReqCreatePlanWorkspace
# ROBOTS: 
audience: Application User
# ms.devlang: 
ms.reviewer: josaw
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid: 
ms.search.region: Global
ms.search.industry: Manufacturing
ms.author: crytt
ms.search.validFrom: 2019-09-06
ms.dyn365.ops.version: AX 10.0.5

---

[!include [banner](../includes/preview-banner.md)]

[Terms and conditions for the preview](http://go.microsoft.com/fwlink/?linkid=2015274)

# Get started

In order to use Planning Optimization you have to install the Planning Optimization Add-in for Dynamics 365 Supply Chain Management from your LCS project and enable the use of Planning Optimization from the Supply Chain Management UI.

As of now Planning Optimization does not support all features that are available in the built-in Supply Chain Management planning engine. Due to this it is important to evaluate if the available feature set in Planning Optimization covers the requirements. To ensure that this evaluations happens, Planning Optimization is not enabled in LCS by default.

Long term, Planning Optimization is expected to replace the existing built-in Supply Chain Management planning engine.

It is strongly recommended to evaluate results from the Planning Optimization fit analysis before enabling Planning Optimization. Read more about Planning Optimization fit analysis [link] .

### What is the license impact

If your license allow you to run master planning there is no additional license needed to start using Planning Optimization.

### LCS

In order to use Planning Optimization you have to install the Planning Optimization Add-in for Dynamics 365 Supply Chain Management from your LCS project.

- From Lifecycle Services open the LCS project
- Expand the **Environment add-ins** tab and click **Install a new add-in**
- Select **Planning Optimization**
- Follow the installation guide and agree to terms and conditions
- Click **Install**

### Planning Optimization integration

From the **Master Planning** > **Setup** > **Planning Optimization integration** > **Integration parameters** you control if Planning Optimization Add-in for Dynamics 365 Supply Chain Management should be used for master planning.

**Note:** The use of Planning Optimization impacts the master planning result and features depending on master planning.

**Connection status**

Connection status show the current status of the connection to the Planning Optimization service. The following table show the possible status values.

| Connection status | Description | Possible to enable Use Planning Optimization |
| --- | --- | --- |
| **Connected** | Connection is established between the Planning Optimization service and Supply Chain Management. | Yes |
| **Enabling connection** | A request to enable the connection to the Planning Optimization service is currently in progress. | No |
| **Disconnected** | There is no connection to the Planning Optimization service. Connection can be enabled from LCS as described earlier on this page. | No |
| **Disabling connection** | A request to disable the connection to the Planning Optimization service is currently in progress. | No |
| **Getting status** | System is waiting for status from the Planning Optimization service. | No |

**Use Planning Optimization**

This option is used to control the planning engine used for master planning

**Yes** - Planning Optimization is used for master planning.

**No** - The build-in Supply Chain Management planning engine is used for master planning.

**Note:** If existing planning batch jobs created for the built-nn Supply Chain Management planning engine are triggered when **Use Planning Optimization** is set to **Yes** these will fail, as the build-in Finance and Operations planning engine is disabled.

#### Setup integration with the Planning Optimization

With Planning Optimization preview enabled master planning is done using the Planning Optimization Add-in for Finance and Operations. This impacts the master planning result and features depending on master planning.
