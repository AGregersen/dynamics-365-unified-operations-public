---
# required metadata

title: Use cases for business events
description: This topic lists use cases for business events.
author: Sunil-Garg
manager: AnnBe
ms.date: 03/29/2019
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
# ms.custom: 
ms.search.region: Global
# ms.search.industry: 
ms.author: sunilg
ms.search.validFrom: Platform update 24
ms.dyn365.ops.version: 2019-02-28
---

# Use cases for business events

[!include[banner](../includes/banner.md)]

The following are potential uses cases for business events. This is by no means an exhaustive list of the potential use cases. It should also be noted that some of these use cases may not have been implemented yet either by Microsoft or other organizations. These are meant to provide ideas and help with understanding certain business events.

| **Use case**                         | **Value**  |
|----------------------------------------|----------|
| The procurement process frequently relies on manual intervention, so automating this process should increase procurement manager productivity.             | You can make the procurement process more efficient by alerting procurement managers when quotation requests are sent, allowing for prompt follow up and faster engagement. The goal is to have procurement managers follow up within three days and possibly create a Flow that automates this follow up. |
| Managers are not informed about newly created financial reports. As a result, managers might analyze and make decisions based on outdated data.          | You can make the reporting process more efficient by alerting managers when financial reports are sent, allowing for prompt follow up and faster engagement. The goal is to have managers follow up within three days and possibly create a Flow that automates this follow-up.                            |
| When a new customer is created, a credit limit check is needed. If something could automatically trigger an API that subscribes to a credit limit, and then check the website and import specific credit limit check fields, such as limit amount and rating. At the same time, an approval Flow needs to start so that the customer account can be used after approval from management. | This is required by many companies, especially in the retail area. This would be beneficial because partners develop customizations for this purpose.   |
| The month-end closing schedule is a simple list that does not allow automatic actions. If functionality could be created to inform a group of people about tasks that have been completed and verified as complete, then a different group of people could start working.    | Use real-life scenarios to enhance the currently static and difficult to use month-end closing workspace.  |
| If functionality could be created to trigger a flow when the status of a period is changed – either opened or closed.  | Users are not automatically informed when new periods are opened after the month-end close is completed and they are allowed to start recording transactions in the new period.                             |
| If you are using the supplier (vendor) collaboration workspace, there is no automated way to inform the supplier that a new record has been created or existing records have been updated. This is an issue with requests for quotation and purchase orders. This means that the supplier would need to review the supplier collaboration workspace in case there are issues. | Using business events, the supplier portal functionality will provide improved productivity and efficiency by removing the need for additional correspondence between the supplier and Finance and Operations. This is a true collaboration and will lead to supply chain efficiency. Without this functionality, the organization must follow up on all new requests or updates with phone calls or emails to the suppliers. This is improves the supplier collaboration workspace. |
| A quotation is placed for a personalized product. After the quotation is won this needs to become a real product. Requests are sent to a Data team (using PowerApps or Office) to create the item in Finance and Operations. After the item has been manually created, the item on the line is updated and the quote triggers the creation of a sales order. Currently, when the item is created, the approach is to wait for the data integrator to copy it to Common Data Service. Monitors are set to find new entries on Common Data Service and compare the unique references to any open numbers. Ideally, an item created business event exists which is extended so that it has the unique identifier. This event is then subscribed to (in Flow or PowerApps) and immediately updates the quote line. | Using business events, the business would be able to update the won quote with the new product when the new product is created. This removes possible delays, manual updates, and errors. |
| Shipment for sales orders starts in a different system to enable logistics balancing of third-party haulers, production of customs, and delivery documentation. This pushes the data to a major transport company. Upon picking or shipment of a sales order, the line details are the event that triggers the external system to analyze and determine the details of the utilized shipment. This pushing event depends on the ability for a business action to update Finance and Operations. This could be that the order is picked and then the shipment information pushed to Finance and Operations, or it is marked as shipped in Finance and Operations as it is pushed externally.  | This allows businesses with third-party transport companies to send shipping information to their vendors. This approach puts the responsibility of dispatch utilization on the external vendors and simplifies the setup in Finance and Operations. |
| Picking for sales orders can be performed in a different systems, whether it’s a separate internal warehousing system or a third-party location that is not part of Finance and Operations. Upon confirmation or picking of a sales order, the line details are the event that triggers the external system to analyze and determine the picking priority and utilization.  | This allows businesses with third-party warehouses to send the picking information to the system. This can also be used if the warehouse has automated picking machines that determine what is required. This approach puts the responsibility of prioritizing picking and utilization on the external system and simplifies the setup in Finance and Operations. |
| Scheduling batch jobs to process polling logic can put a lot of constraint on resources. To realize near real-time processing, it is compelling to schedule the batch to run as fast as it can in Finance and Operations, which typically ends up being every few minutes. These batch jobs are typically data import/export jobs that look for data to be processed. However, if data is not available the batch job processes empty cycles which can consume system resources.  | Using business events, the polling use case can be re-designed to be asynchronous if it is triggered by the business event. Data will be processed only when it is available. The business logic that makes the data available triggers the business event, which can then be used to start the data processing job/logic. This can save thousands of batch executions from running empty cycles and wasting system resources. |
