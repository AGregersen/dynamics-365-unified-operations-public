---
# required metadata

title: Installation steps for Retail channel components in an on-premises environment
description: This topic covers the installation steps for Retail channel components in an on-premises environment. 
author: jashanno
manager: AnnBe
ms.date: 12/17/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

# ms.search.form:  [Operations AOT form name to tie this topic to]
audience: IT Pro
# ms.devlang: 
ms.reviewer: sericks
ms.search.scope: Retail, Operations 
# ms.tgt_pltfrm: 
# ms.custom: [used by loc for topics migrated from the wiki]
ms.search.region: Global
# ms.search.industry: [retail
ms.author: jashanno
ms.search.validFrom: 2018-10-31
ms.dyn365.ops.version: 8.1.1
---

# Installation steps for Retail channel components in an on-premises environment

[!include[banner](../includes/banner.md)]

This topic covers the installation steps for Retail channel components in an on-premises environment.

## Overview

Retail channel functionality, in an on-premises environment, is enabled exclusively via use of Retail Store Scale Unit. For an overview of Retail Store Scale Unit, see [Retail Store Scale Unit](../../retail/dev-itpro/retail-store-system-begin.md). 

Unlike a cloud deployment, an on-premises environment does not enable seamless, high-availability deployment of Retail channel components via Lifecycle Services (LCS). The only way to use Retail channel components is by installing Retail Store Scale Unit.

## Prerequisites 

Before you can start installation of Retail channel components, you must first complete all prior installation steps for an on-premises environment. These steps are listed in [Set up and deploy on-premises environments (Platform update 12 and later)](setup-deploy-on-premises-pu12.md).  Further, version 8.1.1 must be installed for Retail to function fully.  It is recommended to update to version 8.1.2.

> [!Note]
> It is critical to ensure that a secure network, that is not publicly  accessible, is used to connect Retail Store Scale Unit (RSSU) to Retail headquarters. You must also restrict network access to Retail headquarters only to known RSSU devices via network filtering or other means.  This means that a firewall must exist and whitelisting is highly recommended.

## Installation steps

1.	On the previously created [file share](https://docs.microsoft.com/en-us/dynamics365/unified-operations/dev-itpro/deployment/setup-deploy-on-premises-pu12#setupfile), create a new folder called **selfservicepackages** on each AOS machine.
2.	On each AOS computer, run the following PowerShell script:

```powershell
.\RetailUpdateDatabase.ps1 -DatabaseServer '<Database server name for AOS database>' -DatabaseName '<Database name for AOS database>' -envName '<Environment name>' -RetailSelfServicePackages '<Local path of Retail self-service packages>’ -SendProductSupportTelemetryToMicrosoft
```
> [!NOTE]
> The parameters **-DatabaseServer** and **-DatabaseName** should be known based on the environment setup.
> The parameter **-envName** should be known based on creation when the environment is generated.
> The parameter **-RetailSelfServicePackages** is the full path location created in the first step (**selfservicepackages**).
> The parameter **-SendProductSupportTelemetryToMicrosoft** is a required value to enable telemetry to Microsoft.  This is critical to maximize support from Microsoft.
> This script will perform a variety of actions, including updating the Retail Service user and role and updating Retail registry keys.
  
3.	Download the binary update from LCS. For instructions, see [Get updates from Lifecycle Services (LCS)](../migration-upgrade/download-hotfix-lcs.md).
4.	Extract the zip file and copy all six self-service installers (AsyncServerConnectorServiceSetup.exe, RealtimeServiceAX63Setup.exe, HardwareStationSetup.exe, ModernPosSetup.exe, ModernPosSetupOffline.exe, and StoreSystemSetup.exe) into the folder **selfservicepackages** defined and created in step 1 in each of the AOS machines.
5.  Navigate to the ADFS machine, then to the InfrastructureScripts folder.  This is the same file directory where the previously run Retail PowerShell script was located (**RetailUpdateDatabase.ps1**).  Find the PowerShell script **Create-ADFSServerApplicationForRetail.ps1**.
6.  On the ADFS machine currently viewing, run this script in a new PowerShell window using the command **.\Create-ADFSServerApplicationForRetail -HostUrl 'https://ax.d365ffo.onprem.contoso.com'**, where the **HostUrl** value can be found in Service Fabric.  To find the **HostUrl** value, navigate to **Service Fabric** &gt; **Application fabric:/AXSF** &gt; **Details** &gt; **Aad_AADValidAudience**.
7.  Access the newly generated Server application from the **Application Groups** in AD FS Management.
8.  Edit the newly generated Server application and select to **Reset the Secret**.

> [!NOTE]
> It is an important security measure to run this script for each Retail Store Scale Unit.  This maximizes security and minimizes the workload if ever a security breach occurred. 
> 
> It is critical to keep this secret safe.  This secret should only ever be copied once and never stored on the system.  The Client ID and Secret generated will be used during the Retail Store Scale Unit installer, so it is required to be used at a later time.  You can always reset the secret again, but it must then be updated on any Retail Store Scale Unit that used the previous secret.

9.  Navigate to **Retail** &gt; **Headquarters setup** &gt; **Retail scheduler** &gt; **Connector for Microsoft Dynamics AX**.
10.  Select **Edit** on the Action pane.
11.  In the **Profile** field, enter the value **Default**.  If desired, enter a description in the **Description** field.

> [!NOTE]
> It is possible for the following fields in steps 12 through 14 to already have values.  If this is correct, it is correct to skip those steps and continue forward from there.  What is important is to have a selectable profile title (Default in this case).

12.  In the  **Web application name** field, enter the value **RetailCDXRealTimeService**.
13.  In the **Protocol** field, select the value **https**.
14.  In the **Common name** field, enter the value **AXServiceUser@contoso.com**.
15.  Select **Save** from the Action pane.
16.  In Retail headquarters, navigate to **Retail** &gt; **Headquarters setup** &gt; **Parameters** &gt; **Retail shared parameters**.
17.  Select the **Security** tab.
18.  Under the sub-heading **TRANSACTION SERVICE LEGACY PROPERTIES**, select the field **Real-time Service profile** and select the newly created **Default** value.
19.  Select the **Identity providers** tab.
20.  On the **Identity providers** FastTab, select **+Add**.
21.  In the new **Issuer** row, enter the new Identity provider value **https://sts.windows.net/** in the field.
22.  Select **Save** from the Action pane.
23.  Navigate to **Retail** &gt; **Headquarters setup** &gt; **Parameters** &gt; **Retail parameters**.
24.  On the **General** tab, select the **Initialize** link to configure seed data for Retail functionality.

> [!NOTE]
> The installers will not download from their relevant pages the first time a download is attempted.  This is due to the installers have only just been placed into the download location and the associated database values not yet existing.  In headquarters, when the **Download** functionality is attempted (Retail Store Scale Unit or Retail Modern POS, for example), an error will be shown and then an automated upload functionality will be initiated to allow the installers to be downloaded correctly the second time it is attempted (Allow one minute of time before attempting to download the installer again).

25.	Follow the installation steps for installing the Retail Store Scale Unit. For instructions, see [Configure and install Retail Store Scale Unit](../../retail/dev-itpro/retail-store-scale-unit-configuration-installation.md).  At multiple locations in this document there will be notes referencing changes to the instructions for an on-premises deployment.  It is important to take note.
