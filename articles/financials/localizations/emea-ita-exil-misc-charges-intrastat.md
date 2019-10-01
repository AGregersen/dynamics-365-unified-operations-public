---
# required metadata

title: Miscellaneous charges per Kg in Intrastat declaration
description: Miscellaneous charges per Kg in Intrastat declaration.
author: ilkond
manager: AnnBe
ms.date: 27/08/2019
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

ms.search.form: 
audience: Application User
# ms.devlang: 
ms.reviewer: kfend
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
# ms.custom: 
ms.search.region: Italy
# ms.search.industry: 
ms.author: ilyako
ms.search.validFrom: 2019-11-29
ms.dyn365.ops.version: 10.0.7

---

# Miscellaneous charges per kilogram in Intrastat declaration

[!include [banner](../includes/banner.md)]

Intrastat is the system for collecting information and generating statistics about the trade of goods among countries/regions of the European Union (EU). For more information, see [Intrastat overview](https://docs.microsoft.com/en-us/dynamics365/unified-operations/financials/localizations/emea-intrastat).

Among other reporting elements Intrastat declaration contains information about miscellaneous charges that are usually calculated as a percentage on the invoice amount. In Italy miscellaneous charges are often calculated as the multiplication of the cost for each kilogram and goods weight in kilograms.

This topic explains how to enable, set up and use miscellaneous charges per kilogram for Intrastat declaration.

## Prerequisites

- The primary address of the legal entity must be in Italy.
- In the **Feature management** workspace, turn on the **Miscellaneous charges per kilogram in Intrastat declaration** feature. For more information, see [Feature management overview](../../fin-and-ops/get-started/feature-management/feature-management-overview.md).

## Set up miscellaneous charges per kilogram

In released products Master Data in **Foreign trade** FastTab, **Intrastat** section, in the field **Cost charges per kg** define charge amount per kilorgam.

![Cost charges per kg](media/emea-ita-exil-misc-charge-kg-pic1.jpg)

> [!NOTE]
> Make sure that products weight is defined in kilograms.

## Miscellaneous charges calculation

When transferring transactions to Intrastat declaration (for more information, see [Transfer transactions to the Intrastat](https://docs.microsoft.com/en-us/dynamics365/unified-operations/financials/localizations/tasks/transfer-transactions-intrastat)), **Statistical charges amount** will be calculated using the formula:

>*Statistical charges amount = Cost of each kilogram * Net weight (in kilograms)*

If **Chagres percentage** is also defined then both types of miscellaneous charges will be used in the calculation:

>*Statistical charges amount = (Invoice amount * Charges percentage) + (Cost of each kilogram * Net weight)*

![Charges amount](media/emea-ita-exil-misc-charge-kg-pic2.jpg)
