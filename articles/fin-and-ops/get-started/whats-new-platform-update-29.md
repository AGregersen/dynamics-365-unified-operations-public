---
# required metadata

title: Preview features in Dynamics 365 for Finance and Operations platform update 29 (September 2019)
description: This topic describes features that are in preview in Dynamics 365 for Finance and Operations platform update 29. 
author: tonyafehr
manager: AnnBe
ms.date: 07/31/2019
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
ms.assetid:
ms.search.region: Global
# ms.search.industry: 
ms.author: tfehr
ms.search.validFrom: 2019-09-30
ms.dyn365.ops.version: Platform update 29

---
# Preview features in Dynamics 365 for Finance and Operations platform update 29 (October 2019)

[!include [banner](../includes/banner.md)]
[!include [banner](../includes/preview-banner.md)]

This topic describes features that are new or changed in Dynamics 365 for Finance and Operations platform update 29. This version has a build number of 7.0.XXXX. For more information about Platform update 29, see [Additional resources](whats-new-platform-update-28.md#additional-resources).


## Feature management
The Feature management experience provides a workspace where you can view a list of features that have been delivered in each release. In Platform update 29, additional features have been added, including:
- Enable all features that are not enabled.
- Automatically enable all features after an update.
- Do not allow a feature to be enabled based on a condition, such as an existing config key is turned on.
- Add a button called **Check for updates** that manually searches for new features and adds them to the list of features.

For more information, see [Feature management overivew](feature-management/feature-management-overview.md).

## Data management job history clean up
[Job history clean-up functionality](../../dev-itpro/data-entities/data-import-export-job.md#job-history-clean-up-available-in-platform-update-29-and-later) in Data management must be used to schedule a periodic cleanup of the execution history. This functionality is a step up to the existing staging table clean-up functionality which is now deprecated.

## Business events catalog security
[Role-based security](../../dev-itpro/business-events/home-page.md#role-based-security-for-business-events) can be now applied to individual business events in the business event catalog. Once this security is enabled and configured, users will be able to only view and subscribe to business events to which thier role(s) have access. This security applies to integration scenarios like Microsoft Flow, as well.

## Attachment recovery
An attachment recovery feature has been added that provides a recycle bin for record attachments. For a configured period of time after deletion, users and administrators can recover deleted attachments using the new deleted attachments forms. For more details, see [Configure document management](../../fin-and-ops/organization-administration/configure-document-management.md).

## Session idle timeout
The session idle timeout is the amount of time a user can be inactive before the user's session times out and is closed. With Platform update 29, the web browser session timeout setting is exposed in the UI, and is optimized for a default value of 30 minutes instead of 60 minutes. You can still change and set the value up to 60 minutes, but that might cause an extra load on the system. For more information, see [Set the session idle timeout](../../dev-itpro/sysadmin/session-idle-timeout.md).

## Visual refresh of the web client to align with the Fluent design language
As part of the Dynamics 365 app-wide effort, Finance and Operations will be incrementally working towards a visual refresh of the web client to more closely align controls and pages with the Microsoft Fluent design language. An initial set of changes are included in Platform update 29. See the corresponding [Visual refresh of the web client to align with the Fluent design language](https://docs.microsoft.com/dynamics365-release-plan/2019wave2/dynamics365-finance-operations/visual-refresh-web-client-align-fluent-design-language) topic in the Release plan for more details.

## (Preview) Saved views 
Saved views are now available in Preview! This feature represents a significant enhancement to the personalization subsystem, and allows users to have multiple named sets of personalizations per page. For list pages, these views can also contain filters. Management of personalizations is also substantially easier with views, as views can be published to security roles. See [Saved views](saved-views.md) for more information, including details on how to enable this feature in developer environments, as well as the [Build forms that fully utilize saved views](../../dev-itpro/user-interface/understanding-saved-views.md) topic. Note that this preview feature will continue to evolve and change until it becomes generally available. 

## (Preview) New grid control
The [new grid control](https://docs.microsoft.com/dynamics365-release-plan/2019wave2/dynamics365-finance-operations/user-productivity-new-grid) is now available in Preview! This new grid serves as a replacement for the existing grid control and boasts faster rendering, smoother scrolling, easier navigation in the grid, and drag-and-drop column reordering. The new grid also allows for grand totals at the bottom of numeric columns in tabular grids in a footer that can be enabled using the right-click context menu from column headers. Once enabled, all tabular and list grids will automatically switch to use the new grid, unless the page has a grid with a non-React extensible control, in which case the existing grid control will be used on that page. Note that this preview feature will continue to evolve and change until it becomes generally available.

To try out the new grid control, simply add &debug=reactGrid into the URL of your developer environment. Note that flighting will prevent the feature from being operational in other environments.  

## Workflow work item notifications in the action center 
Users can now opt-in to receive notifications in the Action Center by toggling on **Settings** > **User options** > **Workflow** > **Notifications** > **Send notifications to Action Center**. When enabled, the user will receive a notification for each new work item that is assigned to them.

## Workflows can now support reset
Workflows can now support reset from the Workflow History form by optionally implementing the **WorkflowIRecallUnrecoverable** interface. The vendor invoice workflow has used this interface to allow unrecoverable vendor invoice workflows to be recalled and placed in a cancelled state.

## Workflow deletion will confirm business event subscription deletions
When business event subscriptions associated with the workflow are found, a confirmation dialog will provide a list of any related business event subscriptions so that the user is fully aware of the effects of deleting the workflow.

## Improved payloads for workflow business events
Standard workflow context has been added to the payloads for all Workflow Business Events including owner, orginator, and last note.

## Flow templates for workflow work item
Flow templates have been created to provide a useful starting point for building Flows that faciliate work item completion. See [Workflow Business Events]](../../fin-and-ops/dev-itpro/business-events/business-events-workflow.md) for more information.

## Extensibility enhancements
The following enhanced extensibility capabilities have been added in Platform update 29:

- Enable extension of WorkflowApproval properties, WorkflowTask properties, and addition of WorkflowOutcomes into a WorkflowTask (Ref# 198831).
- Enable event triggering for fields on forms that come from table field groups (Ref# 247364).
- Enable the use of the FormObservable attribute in class declarations (Ref# 198797).
- Add model name to extension default naming to reduce conflicts (Ref# 300468).
- Enable use of extension table fields in form datasources and security privileges (Ref# 315634).
- Custom privilege for a standard form control should consider needed permission property value set on extension form (Ref# 313650).
- Allow table display methods added via extension to be used as lookup methods (Ref# 243486).
- Enable display methods to be added to Form Datasources via extension (Ref# 256004).

## Additional resources

### Platform update 29 bug fixes
For information about the bug fixes included in each of the updates that are part of Platform update 29, sign in to Lifecycle Services (LCS) and view this [KB article](https://fix.lcs.dynamics.com).

### Dynamics 365: 2019 release wave 2 plan
Wondering about upcoming and recently released capabilities in any of our business apps or platform?

Check out the [Dynamics 365: 2019 release wave 2 plan](https://docs.microsoft.com/dynamics365-release-plan/2019wave2/). We've captured all the details, end to end, top to bottom, in a single document that you can use for planning.

### Removed and deprecated features
The [Removed or deprecated features](../../dev-itpro/migration-upgrade/deprecated-features.md) topic describes features that have been removed or deprecated for Dynamics 365 for Finance and Operations.

- A *removed* feature is no longer available in the product.
- A *deprecated* feature is not in active development and may be removed in a future update.

Before any feature is removed from the product, the deprecation notice will be announced in the [Removed or deprecated features](../../dev-itpro/migration-upgrade/deprecated-features.md) topic 12 months prior to the removal.

For breaking changes that only affect compilation time, but are binary compatible with sandbox and production environments, the deprecation time will be less than 12 months. Typically, these are functional updates that need to be made to the compiler.
