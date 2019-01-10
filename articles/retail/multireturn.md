---
# required metadata

title: Return items across multiple customer orders and invoices
description: This topic describes the functionality enabling returns across multiple customer orders and invoices in Microsoft Dynamics 365 for Retail.
author: josaw1
manager: AnnBe
ms.date: 1/08/2019
ms.topic: index-page
ms.prod: 
ms.service: dynamics-365-retail
ms.technology: 

# optional metadata

# ms.search.form: 
# ROBOTS: 
audience: Application User
# ms.devlang: 
ms.reviewer: josaw
ms.search.scope: Core, Operations, Retail
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid: ed0f77f7-3609-4330-bebd-ca3134575216
ms.search.region: global
ms.search.industry: Retail
ms.author: josaw
ms.search.validFrom: 2019-01-15
ms.dyn365.ops.version: 10.0

---
# Return items across multiple customer orders and invoices

In Dynamics 365 for Retail, returns can now be made across multiple orders and invoices, whereas in previous releases, 
returns could only be processed by a single invoice at a time. 


## Configure Retail to support returns across multiple customer order and invoices

1. Go to **Retail parameters \> Customer orders**.
1. Turn on the **Enable returns for multiple orders** parameter. 

## Process returns

Once the parameter is turned on and the changes are synchronized to the stores, the cashier in the store can select multiple sales orders for a customer for their return.

When the orders are selected, a list of all the returnable products across all the invoices for the orders will some up. The cashier can then select the products to return. A single return order will be created for all the selected products.
