---
# required metadata

title: What's new or changed in Dynamics 365 for Finance and Operations version 8.1.2 (December 2018)
description: This topic describes features that are either new or changed in Dynamics 365 for Finance and Operations version 8.1.2. This version was released in December 2018.
author: tonyafehr
manager: AnnBe
ms.date: 12/11/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-platform
ms.technology: 

# optional metadata

# ms.search.form: 
# ROBOTS: 
audience: Developer, IT Pro
# ms.devlang: 
ms.reviewer: tfehr
ms.search.scope:  Operations
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid: b364a31d-52de-45c5-b698-64c5262c592a
ms.search.region: Global
# ms.search.industry: 
ms.author: tfehr
ms.search.validFrom: 2018-11-02 
ms.dyn365.ops.version: Release 8.1.2

---
# What's new or changed in Dynamics 365 for Finance and Operations version 8.1.2 (December 2018)

[!include [banner](../includes/banner.md)]
[!include [banner](../includes/preview-banner.md)]

This topic describes features that are either new or changed in Microsoft Dynamics 365 for Finance and Operations version 8.1.2. This version was released in December 2018 and has a build number of 8.1.195.

To learn about the new features and changes in the latest releases of Microsoft Dynamics 365 for Retail, see [What's new or changed in Dynamics 365 for Retail](https://docs.microsoft.com/en-us/dynamics365/unified-operations/retail/get-started/whats-new).

### Dynamics 365 October '18 release notes
Wondering about upcoming and recently released capabilities in any of our business apps or platform? 

[Check out the October '18 release notes](https://go.microsoft.com/fwlink/?linkid=870424). We've captured all the details, end to end, top to bottom, in a single document that you can use for planning. 

## Bug fixes
For information about the bug fixes included in each of the updates that are part of Platform update 22, sign in to Lifecycle Services (LCS) and view the [KB article](https://go.microsoft.com/fwlink/?linkid=2037783).

## Platform update 22
Microsoft Dynamics 365 for Finance and Operations version 8.1.2 includes Platform update 22. To learn more about Platform update 22, see 
[What's new or changed in Dynamics 365 for Finance and Operations platform update 22 (November 2018)](whats-new-platform-update-22.md).

## Extensibility enhancements
In this release of Finance and Operations, numerous extensibility enhancements have been made to support extensibility including enhancements to enumerations, metadata, and methods. For detailed information, see [Extensibility changes in Dynamics 365 for Finance and Operations version 8.1.2](../../dev-itpro/extensibility/extensibility-changes-812.md).

## Derived dimension values
This release includes functionality that lets you prevent changes to derived dimension values and override existing dimension values with derived dimension values. For more information, see [Financial dimensions](../../financials/general-ledger/financial-dimensions.md).

## Intrastat format changes for Belgium
This release includes changes to the XML Intrastat format for Belgium that applies to reporting for 2019. To apply the new format, you need to import the following version (or a later version) of the ER configuration from the LCS shared asset library: Intrastat (BE).version.2.6.xml. For more information about how to import configurations, see [Import a configuration from Lifecycle Services](../../dev-itpro/analytics/tasks/er-import-configuration-lifecycle-services.md). 

## Russian-specific features
This release includes the following features specific for Russia:

### Third-party miscellaneous charges for Russia
- Inclusion into cost of purchased goods (allocation to invoices lines from other vendors). 
- Redrawing to other parties. 
- Re-allocation to other expense accounts.

### Bailment for Russia

**Accounting at Bailee side**
 - Accounting of inventory receipt for bailment as required by law and generation of primary form MX-1. 
 - Accounting of inventory return from bailment and generation of primary form MX-3. 
 - Bailment costs calculation from Bailee side.
 
 **Accounting at Owner side**
 - Accounting of inventory transfer to bailment and inventory return from bailment on Goods Owner side under bailment service contract.

### Goods in transit for Russia

**Sales to customer with postponed passing of property**
 - Post sales invoice with postponed property transfer. This means that customer debts are not posted, all outgoing taxes are posted, and items are transferred to transit warehouse. 
 - Register passing of property with posting debts and items sale from transit warehouse.

**Goods in transit from vendor**
 - Register goods in transit from vendor by special posting profile with Item type "purchased items en route". 
 - Creating Act of inventory holdings en route (INV-6).

### Optional posting of transfer orders to GL
Option to post or not post transactions to General ledger when posting a transfer order.

### Profit tax registers for assets
The following tax registers are available:
 - **Goods cost calculation**
 - **FA object information** 
 - **IA object information** 
 - **FA depreciation** 
 - **IA depreciation** 
 - **FA/IA sale**
 - **Depreciation bonus recovery**

### Sales, purchase books, additional sheets, invoice-factures journal in electronic format
In this release, you can review electronic formats of sales, purchase books, additional sheet,s and factures journals that are configured with Electronic reporting. 

To apply the new formats, you need to import the following or higher versions of the ER configurations from the LCS shared asset library:  
 - VAT declaration model (RU).version.46
 - VAT declaration model mapping (RU).version.46.70
 - Purchase book format.version.46.13
 - Sales book format.version.46.13
 - Purchase book additional sheet format.version.46.9
 - Sales book additional sheet format.version.46.13
 - Factures journal format.version.46.4
 
For more information, see [Import a configuration from Lifecycle Services](../../dev-itpro/analytics/tasks/er-import-configuration-lifecycle-services.md). 

These configuration versions are released as public preview and will be updated based on feedback received. Use them to learn how electronic formats of sales, purchase books, additional sheets, and factures journals are configured with Electronic reporting. Do not use these configurations as base configurations for derived customized configurations in a live environment.

For more information, see [Sales books, purchase books, and invoice-factures journals](../../financials/localizations/rus-sales-books-purchase-books).
