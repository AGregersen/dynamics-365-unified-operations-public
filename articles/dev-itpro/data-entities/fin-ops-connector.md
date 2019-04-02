---
# required metadata

title: Finance and Operations Connector
description: This topic provides information about the Finance and Operations Connector for Microsoft Flow and Logic Apps.
author: Sunil-Garg
manager: AnnBe
ms.date: 03/31/2019
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

# ms.search.form:  [Operations AOT form name to tie this topic to]
audience: IT Pro
# ms.devlang: 
ms.reviewer: sericks
ms.search.scope: Operations, Core
# ms.custom: [used by loc for topics migrated from the wiki]
ms.search.region: Global for most topics. Set Country/Region name for localizations
# ms.search.industry: 
ms.author: sunilg
ms.search.validFrom:
ms.dyn365.ops.version: 2019-02-28
---

# Finance and Operations Connector

[!include[banner](../includes/banner.md)]
[!include[banner](../includes/preview-banner.md)]

The Dynamics 365 for Finance and Operations connector allows Microsoft Flow, PowerApps, Data Integrator, and Logic Apps to integrate with an instance of Dynamics 365 for Finance and Operations. An integration can use the available actions to affect a create, update, or delete operation in the target instance. 

## Prerequisites
We recommend that you read the following topics as a prerequisite to familiarize yourself with connectors before proceeding further

- [Connectors](https://docs.microsoft.com/en-us/connectors/) 
- [Data management package REST API](https://docs.microsoft.com/en-us/dynamics365/unified-operations/dev-itpro/data-entities/data-management-api?toc=/fin-and-ops/toc.json)
- [Open Data Protocol (OData)](https://docs.microsoft.com/en-us/dynamics365/unified-operations/dev-itpro/data-entities/odata?toc=/fin-and-ops/toc.json) 
- [Recurring integrations](https://docs.microsoft.com/en-us/dynamics365/unified-operations/dev-itpro/data-entities/recurring-integrations?toc=/fin-and-ops/toc.json) 

## Triggers
Business events in Finance and Operations are exposed via the trigger *When a business event occurs*. This is explained in detail in the documentation about [Business events in Microsoft Flow](https://docs.microsoft.com/en-us/dynamics365/unified-operations/dev-itpro/business-events/business-events-flow). Business events are explained in detail in the documentation about [Business events](https://docs.microsoft.com/en-us/dynamics365/unified-operations/dev-itpro/business-events/home-page).

## Actions

This section describes the actions that are available in the Dynamics 365 for Finance and Operations connector.

**Get a record**

This action can be used to fetch a record for a specific data entity from the target instance of Finance and Operations.

*Instance* refers to the URL of the target instance of Dynamics 365 for Finance and Operations to which the connector must connect. The expected value is to enter the URL without the ‘https://’ prefix or choose one from the drop-down menu. This lists of all the Finance and Operations environments that are deployed in the Azure Active Directory tenant for the user account that was used to sign in to the specific client like Microsoft Flow, PowerApps, or Logic App.

*Entity name* refers to the data entity in Finance and Operations from which the record must be fetched. The drop-down menu shows the list of data entities from the target environment.

*Object ID* refers to the primary keys fields that must be specified to uniquely identify the record that must be fetched. The following syntax must be followed to specify the keys.

**Create a record**

This action can be used to create data records for a data entity.

*Instance* refers to the URL of the target instance of Dynamics 365 for Finance and Operations to which the connector must connect. The syntax for this value is to enter the URL without the ‘https://’ prefix or choose one from the drop- menu. This lists of all the Finance and Operations environments that are deployed in the Azure Active Directory tenant for the user account that was used to sign in to the specific client like Microsoft Flow, PowerApps, or Logic App.

*Entity name* refers to the data entity in Finance and Operations in which the record must be created. The dropdown menu shows the list of data entities from the target environment.

Based on the selected data entity, the list of fields displayed will be vary.

**Update a record**

This action can be used to update an existing data record for a data entity. The usage is the same as the create a record action.

**Delete a record**

This action can be used to delete an existing data record for a data entity. The usage is the same as the get a record action.

**Execute action**

This action can be used to invoke methods on a data entity to perform a business action.

*Instance* refers to the URL of the target instance of Dynamics 365 for Finance and Operations to which the connector must connect. The syntax for this value is to enter the URL without the ‘https://’ prefix or choose one from the drop- menu. This lists of all the Finance and Operations environments that are deployed in the Azure Active Directory tenant for the user account that was used to sign in to the specific client like Microsoft Flow, PowerApps, or Logic App.

*Action* refers to the method on the data entity that must be executed in Finance and Operations. Based on the selected method, the list of fields displayed will be vary. These fields represent the parameters for the selected method.

**Get list of entities**

This action can be used to get the list of entities for further use in the app that is being developed.

*Instance* refers to the URL of the target instance of Dynamics 365 for Finance and Operations to which the connector must connect. The syntax for this value is to enter the URL without the ‘https://’ prefix or choose one from the drop- menu. This lists of all the Finance and Operations environments that are deployed in the Azure Active Directory tenant for the user account that was used to sign in to the specific client like Microsoft Flow, PowerApps, or Logic App.
