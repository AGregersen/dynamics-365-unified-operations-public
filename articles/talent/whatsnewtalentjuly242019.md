---
# required metadata

title: What's new or changed in Dynamics 365 for Talent (July 23, 2019)
description: This topic describes features that are either new or changed in Microsoft Dynamics 365 for Talent.
author: Darinkramer
manager: AnnBe
ms.date: 7/23/2019
ms.topic: article
ms.prod: 
ms.service: dynamics-365-talent
ms.technology: 

# optional metadata

ms.search.form: 
# ROBOTS: 
audience: Application User
# ms.devlang: 
ms.reviewer: josaw
ms.search.scope: Talent
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: dkrame
ms.search.validFrom: 2019-07-23
ms.dyn365.ops.version: Talent

---
# "What's new or changed in Dynamics 365 for Talent (July 23, 2019)"

[!include [banner](includes/banner.md)]

This topic describes features that are either new or changed in Dynamics 365 for Talent.

## Changes in Attract

### PDF renderer for candidate documents
Attract users can now view candidate PDF attachments in the document viewer experience itself and do not have to download to view it anymore. 

### Signing up for Attract user research group 
As we plan new product capabilities or ship preview features, we are looking for our users to help inform our direction. Interested users can now sign up to be part of our user research group by using the sign-up link in our app.

## Changes in Onboard
This release includes minor bug fixes for Dynamics 365 Talent: Onboard.

## Changes in Core HR
Changes described in this section apply to build number 8.1.2395.

### Entity support for custom fields in Common Data Service 

With this release, Work calendar and Work calendar day now support custom fields in CDS.

### Restrict leave types in time-off requests

Organizations can offer many different types of leave to employees. However, it might not be appropriate for employees to submit time-off requests for some leave types. Those leave types might be managed by HR instead. In this release, you can configure which leave types employees can submit time-off requests for. 

## In preview

### Preview features are enabled only in sandbox instances

When you provision a new instance of Talent, you can specify whether the instance type is **Production** or **Sandbox**. Instances of the **Sandbox** type allow for early testing of new features. All existing Talent instances will be updated to the **Production** instance type. If you want one of your existing instances to be updated to the **Sandbox** instance type, contact [Support](https://docs.microsoft.com/dynamics365/unified-operations/talent/talent-support) to initiate the change request.

For more information about how changes are published, see [Provision Talent](https://docs.microsoft.com/dynamics365/unified-operations/talent/provisioning-talent).

### View extended information for performance in manager self-service

A new option will let managers view the performance of both their direct reports and their extended reports. Currently, line managers can assign and update performance goals and issue new reviews, which their employees co-manage. In addition, direct managers and their employees can maintain and update performance journals to help ensure that the performance review process goes smoothly. When this change is implemented, managers will be able to view and maintain performance-related information for their extended reports in addition to their direct reports. 

## Coming soon

### Region support for Canada and Southeast Asia

We are pleased to announce that Canada and Southeast Asia regions will be available for Microsoft Dynamics 365 for Talent soon. With this change, you can create environments in the Canadian and Asian regions and all Talent data will be maintained solely within those locations. You can create an environment in these new regions by selecting the location in the New Environment dialog and use that environment to provision Talent in LCS as described here [Provision Talent](https://docs.microsoft.com/en-us/dynamics365/unified-operations/talent/provisioning-talent).

Data migration of existing projects from other regions to the Canadian and Asian regions is not supported. Only new projects can be provisioned to the these new supported regions.
