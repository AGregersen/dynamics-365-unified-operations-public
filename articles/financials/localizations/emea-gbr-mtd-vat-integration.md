---
# required metadata

title: Prepare Finance and Operations for integration with MTD for VAT (United Kingdom)
description: This topic walks you through the process of setting up Microsoft Dynamics 365 Finance and Operations for Making Tax Digital (MTD) for value-added tax (VAT) in the United Kingdom.
author: ShylaThompson
manager: AnnBe
ms.date: 04/02/2019
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

# ms.search.form: 
# ROBOTS: 
audience: Application User
# ms.devlang: 
ms.reviewer: shylaw
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
# ms.custom: 
ms.search.region: United Kingdom
# ms.search.industry: 
ms.author: mrolecki
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0

---

# Prepare Finance and Operations for integration with MTD for VAT (United Kingdom)

[!include [banner](../includes/banner.md)]
[!include [preview-banner](../includes/preview-banner.md)]

This topic walks you through the process of setting up Microsoft Dynamics 365 Finance and Operations for Making Tax Digital (MTD) for value-added tax (VAT) in the United Kingdom (UK).

## Making Tax Digital – VAT statement submission

On July 13, 2017, the Financial Secretary to the Treasury and Paymaster General in the UK announced that MTD for VAT will take effect on April 1, 2019.

MTD introduces an obligation for VAT-registered businesses to keep their records digitally (for VAT purposes only) and to provide VAT return information to Her Majesty's Revenue and Customs (HMRC) through software that is functionally compatible with MTD. Starting April 1, 2019, MTD for VAT will be mandatory for businesses that have turnover that exceeds the VAT registration threshold (currently £85,000). For VAT-registered businesses that have turnover that is below the VAT registration threshold, MTD for VAT will remain voluntary until 2020 at the earliest.

VAT returns will have to be submitted to HMRC by using software that is compatible with MTD. They can no longer be submitted by using the HMRC portal.

In the UK, VAT returns are filed either quarterly or monthly. The deadline for submitting the return online and paying HMRC is one calendar month and seven days after the end of the VAT period.

As HMRC states on the official website, the current amendment process will stay in place for VAT:

- If the net value of the errors on the VAT return is less than £10,000, the company will amend those errors on the next VAT return.
- If the net value of the errors exceeds £10,000, the company must complete the VAT 652 form, which is available on the GOV.UK website.

For more information about MTD for VAT, see [Making Tax Digital for VAT: legislation overview](https://www.gov.uk/government/consultations/making-tax-digital-reforms-affecting-businesses/making-tax-digital-for-vat-legislation-overview).

Software that is compatible with MTD must support the following requirements:

- Keep the required records in a digital form.
- Preserve those records in digital form for up to six years.
- Create a VAT return from the digital records that are held in functionally compatible software, and digitally provide this information to HMRC.
- Provide VAT data to HMRC on a voluntary basis.
- Receive, via the MTD for VAT application programming interface (API) platform, information from HMRC about a relevant entity's compliance with obligations under the regulations.

As HMRC mentions in Making Tax Digital for Business VAT Guide for Vendors, users must sign up for the MTD service for VAT, even if they have already signed up to use the MTD service for income tax. For more information about how to get ready for MTD, see [Making Tax Digital: how VAT businesses and other VAT entities can get ready](https://www.gov.uk/government/publications/making-tax-digital-how-vat-businesses-and-other-vat-entities-can-get-ready).

The solution that supports the MTD for VAT requirements in Finance and Operations is based on the Electronic messages functionality. This functionality provides a flexible approach for setting up and supporting reporting processes. The setup package for MTD for VAT for the UK covers the following scope of interoperation to help companies in the UK meet their VAT obligations:

- **Retrieve VAT obligations (Mandatory)** – Users can initiate a request to HMRC to obtain their company's VAT obligations for a specific period. For each user's request, HMRC will post information about the company's VAT obligations, as that information is defined in the company's profile on the HMRC side. VAT obligations contain information about the VAT period, the due date for submission, and the status of the obligation. This information will be reflected in Finance and Operations.
- **Submit VAT return for period (Mandatory)** – The system collects information about VAT returns. The information that is collected is based on the sales tax payment transactions that have been posted in the system via the sales tax settlement process, with respect to the VAT obligations that are registered in the system. After this information is collected, a VAT return report in JavaScript Object Notation (JSON) format is generated. The user will submit this report to HMRC. The HMRC response to the submission will be reflected in Finance and Operations.
- **Retrieve VAT liabilities (Optional)** – Users can initiate a request to HMRC to obtain their company's VAT liabilities for a specific period. In response to each user's request, HMRC will post information about the company's VAT liabilities, as that information is defined in the company's profile on the HMRC side. This information will be stored in Finance and Operations as an attachment to the related electronic message. This attachment will be in JSON format.
- **Retrieve VAT payments (Optional)** – Users can initiate a request to HMRC to obtain their company's VAT payments for a specific period. In response to each user's request, HMRC will post information about the company's VAT payments, as that information is defined in the company's profile on the HMRC side. This information will be stored in Finance and Operations as an attachment to the related electronic message. This attachment will be in JSON format.

The setup package for MTD for VAT for the UK doesn't cover the View VAT Return endpoint that might be required. However, the Electronic messages functionality lets you set up and support this endpoint.

When a company is signed up for the MTD service for VAT in HMRC, it should complete the following tasks in Finance and Operations. These tasks will prepare Finance and Operations to interoperate with the HMRC web service to retrieve VAT obligations and submit VAT returns.

> [!div class="checklist"]
> * Import and set up Electronic reporting (ER) configurations.
> * Set up application-specific parameters.
> * Import a package of data entities that include a predefined electronic message setup.
> * Set up General ledger parameters.
> * Define a sales tax settlement period.
> * Set up security roles for electronic message processing.
> * Set up security roles to access the token of the web application.
> * Initialize the web application for interoperation with HMRC.
> * Obtain an authorization code for the sandbox environment (for testing purposes only).
> * Obtain an authorization code for the production environment.
> * Obtain an access token.

## Import and set up ER configurations

To prepare Finance and Operations to interoperate with MTD for VAT, you must import the following ER configurations.

| Number | ER configuration name                       | Type                                 | Description |
|--------|---------------------------------------------|--------------------------------------|-------------|
| 1      | **Tax declaration model**                   | **Model**                            | A generic model for different tax declarations |
| 2      | Tax declaration model mapping               | Model mapping                        | A generic model mapping for VAT declarations |
| 3      | VAT Declaration JSON (UK)                   | Format (exporting)                   | A VAT return in JSON format for submission to HMRC |
| 4      | VAT Declaration Excel (UK)                  | Format (exporting)                   | The **VAT 100** report (a declaration in Microsoft Excel format) |
| 5      | MTD VAT interoperation (UK)                 | Format (exporting)                   | A format that is used to create a URL path for HMRC endpoints and to request a test user. |
| 6      | MTD VAT importing model mapping (UK)        | Model mapping (importing)            | The importing model mapping for VAT obligations |
| 7      | MTD VAT obligations importing JSON (UK)     | Format (importing)                   | The format for importing VAT obligations that are retrieved from HMRC |
| 8      | **Electronic Messages framework model**     | **Model**                            | The model for the Electronic messages framework |
| 9      | MTD VAT model mapping (UK)                  | Model mapping (exporting, importing) | A model mapping that supports interoperation for MTD for VAT for the UK |
| 10     | MTD VAT return response importing JSON (UK) | Format (importing)                   | The importing ER format used for response that is received from HMRC for the VAT declaration submission and import it into an electronic message. |
| 11     | MTD VAT web request headers format (UK)     | Format (exporting)                   | A format that is used to create request header parameters for the HTTPS request |
| 12     | MTD VAT authorization format (UK)           | Format (exporting)                   | The request header parameters for the authorization code and access token |
| 13     | MTD VAT import token format (UK)            | Format (importing)                   | The ER format used for importing of access token that is received from HMRC into the database. |

> [!NOTE]
> After all the ER configurations from the preceding table are imported, set the **Default for model mapping** option to **Yes** for the following configurations:
>
> - Tax declaration model mapping
> - MTD VAT model mapping (UK)
>
> ![Default for model mapping option](media/emea-gbr-default-for-model-mapping-parameter.png)

For more information about how to download ER configurations from Microsoft Dynamics Lifecycle Services (LCS), see [Download Electronic reporting configurations from Lifecycle Services](https://docs.microsoft.com/dynamics365/unified-operations/dev-itpro/analytics/download-electronic-reporting-configuration-lcs).

## Set up application-specific parameters

Nine boxes on the VAT declaration for the UK must contain values that are calculated based on tax transactions selected depending on a set of criteria such as the transaction direction, tax code, country or region code of the tax code, and tax type (item or service). Application-specific parameters let users influence the collection of tax transactions that must be considered for calculation of reporting value in each box. For the VAT declaration, there is a **ReportFieldLookup** application-specific parameter. The following result values are available for this parameter:

- VATDue
- VATDueEC
- ECSupplies
- VATReclaimed
- Other

For each value, users can define a set of sales tax codes together with a classifier that is associated with the direction of the tax transaction and the credit note identifier. The following table provides a definition of this classifier.

| Classifier value                | Condition |
|---------------------------------|-----------|
| PurchaseCreditNote              | <ul><li>Credit note</li><li>Tax direction = Sales tax receivable</li></ul> |
| Purchase                        | <ul><li>Not credit note</li><li>Tax direction = Sales tax receivable</li></ul> |
| SalesCreditNote                 | <ul><li>Credit note</li><li>Tax direction = Sales tax payable</li></ul> |
| Sales                           | <ul><li>Not credit note</li><li>Tax direction = Sales tax payable</li></ul> |
| PurchaseExemptCreditNote        | <ul><li>Credit note</li><li>Tax direction = Tax-free purchase</li></ul> |
| PurchaseExempt                  | <ul><li>Not credit note</li><li>Tax direction = Tax-free purchase</li></ul> |
| SalesExemptCreditNote           | <ul><li>Credit note</li><li>Tax direction = Tax-free sales</li></ul> |
| SaleExempt                      | <ul><li>Not credit note</li><li>Tax direction = Tax-free sales</li></ul> |
| UseTaxCreditNote                | <ul><li>Credit note</li><li>Tax direction = Use tax</li></ul> |
| UseTax                          | <ul><li>Not credit note</li><li>Tax direction = Use tax</li></ul> |
| PurchaseReverseChargeCreditNote | <ul><li>Credit note</li><li>Tax direction = Sales tax receivable</li><li>ReverseCharge\_W = Yes</li></ul> |
| PurchaseReverseCharge           | <ul><li>Not credit note</li><li>Tax direction = Sales tax receivable</li><li>ReverseCharge\_W = Yes</li></ul> |
| SalesReverseChargeCreditNote    | <ul><li>Credit note</li><li>Tax direction = Sales tax payable</li><li>ReverseCharge\_W = Yes</li></ul> |
| SalesReverseCharge              | <ul><li>Not credit note</li><li>Tax direction = Sales tax payable</li><li>ReverseCharge\_W = Yes</li></ul> |

Before you start to use the **VAT Declaration JSON (UK)** and **VAT Declaration Excel (UK)** formats, you must set up the **ReportFieldLookup** application-specific parameter. You can download an example of this setup from the Shared asset library in LCS. In the Shared asset library, select the **Data package** asset type, find the **UK MTD VAT ReportFieldLookup v1.xml** file in the list of data package files, and download it.

To set up the **ReportFieldLookup** application-specific parameter in the system, open the **Electronic reporting** workspace, and select the **VAT Declaration JSON (UK)** format in the configuration tree. Then, on the Action Pane, on the **Configurations** tab, in the **Application specific parameters** group, select **Setup**, and select the version of the format that you want to use. If you want to use the example of this setup, select **Import** on the Action Pane, and select the file that you previously downloaded. If you want to manually define conditions, select **ReportFieldLookup** on **Lookups** FastTab, and define criteria on the **Conditions** FastTab. The example file can also be used as a starting point for setting up conditions. When the setup of conditions is completed, change the value of the **State** field to **Completed**, save your changes, and close the page.

> [!IMPORTANT]
> We recommend that you set up the **Other** value as the last condition in the list. This value isn't used in **VAT Declaration JSON (UK)** format but must be set up **"Not blank"** for both columns of criteria.

You can easily export the setup of application-specific parameters from one version of a report and import it into another version. You can also export the setup from one report and import it into another, provided that both reports have the same structure of lookup fields. When your setup is ready, export it, and then import it into the **VAT Declaration Excel (UK)** format.

## Import a package of data entities that includes a predefined electronic message setup

The process of setting up the Electronic messages functionality for MTD for VAT has many steps. Because the names of some predefined entities are used in the ER configurations, it's important that you use a set of predefined values that is delivered in a package of data entities for the related tables.

In [LCS](https://lcs.dynamics.com/v2), go to the Shared asset library, and select the **Data package** asset type. Find **UK MTD-VAT setup.zip** in the list of data package files, and download it to your computer.

After the UK MTD-VAT setup.zip file is downloaded, open Finance and Operations, select the company that you will interoperate with HMRC from, and then go to **Workspaces** \> **Data management**.

You must now import data from the UK MTD-VAT setup.zip file into the selected company. In the **Data management** workspace, select **Import**, and set the **Source data format** field to **Package**. Select **Upload and add**, select the **UK MTD-VAT setup.zip** file on your computer, and upload it.

![Upload and add button](media/emea-gbr-mtd-vat-add-file.png)

For more information, see [Data management](../../dev-itpro/data-entities/data-entities-data-packages.md?toc=/fin-and-ops/toc.json).

> [!NOTE]
> Some records in the data entities in the package include a link to ER configurations. It's important that ER configurations be imported into Finance and Operations before you start to import the data entities package.

The **UK MTD-VAT setup** package provides a setup for two sets of processing that can be used independently:

- **UK MTD VAT returns** – For interoperation with the **production** HMRC web service
- **UK MTD VAT TEST** – For interoperation with the **sandbox** HMRC web service

The **UK MTD-VAT setup** package also provides a setup for two web applications that are used to interoperate with HMRC web services:

- **Dynamics 365 for Finance and Operations** – For interoperation with the **production** HMRC web service
- **Sandbox HMRC** – For interoperation with the **sandbox** HMRC web service

For more information about the predefined setup that is included in the data entities in the package for MTD for VAT, see [Appendix 1: Electronic messages setup for MTD for VAT](#appendix-1-electronic-messages-setup-for-mtd-for-vat) later in this topic. 

## Set up General ledger parameters

On the **General ledger parameters** page, you must set up the following parameters:

- Number sequences
- VAT statement format mapping

### Number sequences

To work with the Electronic messages functionality, you must define related number sequences. Go to **Tax** \> **Setup** \> **General ledger parameters**, and then, on the **Number sequences** tab, set up two number sequences:

- Message
- Message item

### VAT statement format mapping

Finance and Operations lets you generate a paper format of **VAT 100 report** by using the **Report sales tax for settlement period** dialog box (**Tax** \> **Declarations** \> **Sales tax** \> **Report sales tax for settlement period**). Alternatively, you can generate the statement for a selected sales tax payment transaction directly from the **Sales tax payments** page (**Tax** \> **Inquiries and reports** \> **Sales tax inquiries** \> **Sales tax payments**). In both cases, the **VAT 100** report is generated in Microsoft SQL Server Reporting Services (SSRS) format.

To generate the **VAT 100** report in Excel format instead of SSRS format, you must define an ER format on the **General ledger parameters** page. Go to **Tax** \> **Setup** \> **General ledger parameters**, and then, on the **Sales tax** tab, in the **Tax options** section, in the **VAT statement format mapping** field, select **VAT Declaration Excel (UK)**.

If you leave the **VAT statement format mapping** field blank, the **VAT 100** report is generated in SSRS format.

## Define a sales tax settlement period

Electronic message processing that is defined for MTD for VAT in the UK MTD-VAT setup.zip file is company-agnostic. Therefore, it can be implemented in any legal entity in Finance and Operations.

Both the **UK MTD VAT returns** processing (for production) and the **UK MTD VAT TEST** processing (for sandbox) let you collect sales tax payment transactions in the legal entity. You can then generate a VAT return in JSON or Excel format, for either production purposes or testing purposes. The collection of sales tax payment transactions is implemented via the **Populate VAT return records** action of the **Populate record** type. To correctly collect sales tax payment transactions, you must define a sales tax settlement period for the **Populate VAT return records** action. Go to **Tax** \> **Setup** \> **Electronic messages** \> **Populate records actions**, and select the **Populate VAT return records** action. On the **Datasource setup** FastTab, select the **VAT payment** record, and then select **Edit query**. For the **Settlement period** field of the **Sales tax payments** table, define the sales tax settlement period when tax transactions from the selected legal entity must be reported to HMRC.

![Sales tax inquiry](media/emea-gbr-sales-tax-inquiry.png)

If you don't set the **Settlement period** field, all tax transactions from the selected legal entity will be considered for reporting to MTD for VAT.

## Set up security roles for electronic message processing

Different groups of users might require access to different electronic message processing (**UK MTD VAT TEST** or **UK MTD VAT return**). You can limit access to each type of processing, based on security groups that are defined in the system.

To limit access to the **UK MTD VAT TEST** processing, go to **Tax** \> **Setup** \> **Electronic messages** \> **Electronic message processing**. Select the **UK MTD VAT TEST** processing, and add the security groups that must work with this processing for testing purposes. If no security group is defined for the processing, only a system admin can see the processing on the **Electronic messages** page.

To limit access to the **UK MTD VAT returns** processing (production processing), go to **Tax** \> **Setup** \> **Electronic messages** \> **Electronic message processing**. Select the **UK MTD VAT returns** processing, and add the security groups that must work with this processing for real-life interoperation with the production HMRC environment. If no security group is defined for the processing, only a system admin can see the processing on the **Electronic messages** page.

## Set up security roles for the access token of the web application

When an access token to each HMRC web application (production and sandbox) is retrieved from HMRC, it's stored in the system database in encrypted format. The access token must be used whenever a request of any type will be addressed to HMRC. For security reasons, access to the access token must be limited to security groups that must address requests to HMRC. If users who aren't in one of those security groups try to address a request to HMRC, a message notifies them that they aren't allowed to interoperate via the selected web application.

To set up security groups that must have access to HMRC's access token for MTD for VAT, go to **Tax** \> **Setup** \> **Electronic messages** \> **Web applications**. Select the web application to define security groups for, and then add those security group on the **Security roles** FastTab.

If security roles aren't defined for a web application, only a system admin can interoperate via the selected web application.

## Initialize the web application for interoperation with HMRC

Each web application on the HMRC side has three parameters that uniquely identify it:

- **Client ID** – The unique identifier of the web application.
- **Client secret** – The secret passphrase that is used to authorize the web application.
- **Server token** – The secret token that is used to authorize the web application when requests are made to any application-restricted endpoint.

These parameters are used when requests are addressed to HMRC. They must be filled in before you start the authorization process for a web application.

For the sandbox application, you can manually obtain these parameters from the **Manage credentials** section of your sandbox application on the HMRC portal. Copy the parameters, and then, on the **Web applications** page in Finance and Operations (**Tax** \> **Setup** \> **Electronic messages** \> **Web applications**), select the **Sandbox HMRC** web application, and paste the parameters into the appropriate fields in the **Authorization parameters** section on the **General** FastTab.

For the production application (**Dynamics 365 for Finance and Operations**), these parameters are delivered via the package of data entities and stored in the system in encrypted format. When you import predefined setup of Electronic messages functionality for MTD for VAT these parameters will be imported as well, no additional manual actions are needed, once imported, the production application is ready for authorization (obtain an authorization code and access token).

## Obtain an authorization code for sandbox 

HMRC lets you register as a developer on [HMRC Developer Hub](https://developer.service.hmrc.gov.uk/developer/registration) and access the sandbox environment for testing purposes. When you're registered as a developer, you can use the **UK MTD VAT TEST** processing to try to interoperate with the HMRC sandbox environment. However, you must first get test user credentials:

- **User ID** – The name that is used to access HMRC while an authorization code is being requested.
- **Password** – The password that is used to access HMRC while an authorization code is being requested.
- **VRN** – The testing VAT registration number (VRN) that is used during testing interoperation with the HMRC sandbox.

These three parameters must be used together.

To get test user credentials, go to **Tax** \> **Inquires and reports** \> **Electronic messages** \> **Electronic messages**, select **UK MTD VAT TEST**, and then select **New** on the **Messages** FastTab. Select the **Create test user request** action, and then select **OK**. A new electronic message is created. You don't have to fill in any fields of this electronic message to create a test user request. Select **Generate report** on the **Messages** FastTab, and then select **OK** to confirm that you want to send a test user request to HMRC. (A **Generate test user request** action is initialized together with the **Send test user request** action.)

The response from HMRC will be attached to the electronic message as an attachment in JSON format. To open it, select the electronic message, and then select the **Attachments** button (paper clip symbol) in the upper-right corner of the page. On the **Attachments** page for the selected electronic message, select the last **TestUserInfo.txt** file, and then select **Open** on the Action Pane. In the opened file, you will find **userID**, **password** and **VRN** fields, and their respective values.

Update the **Tax exempt number** value of the legal entity that you're working in with the **VRN** value that you obtained from HMRC. Don't change this value while you're working with the sandbox web application unless you get new test user credentials.

After the **Tax exempt number** value of the legal entity that you're working in is updated, you can proceed with authorization in HMRC. Two steps must be done before your system is authorized to interoperate with HMRC:

- Get an authorization code.
- Get an access token.

To get an authorization code, go to **Tax** \> **Setup** \> **Electronic messages** \> **Web applications**, select the web application that you want to authorize for (**Sandbox HMRC**), and select **Get authorization code**. Select **OK** to confirm that you want to initialize the authorization process. On the **Electronic reporting parameters** page, set the **Scope** field. The following values are allowed by HMRC:

- read:vat
- write:vat
- read:vat write:vat

We recommend that you enter **read:vat write:vat** in this field, because the same application must be used for both GET and POST HTTPS requests to the web service. Select **OK** to address the authorization request to HMRC. You're redirected to the HMRC portal for authorization. On the **Sign in** page, enter values that are related to the **userID** and **password** value from the response that you received when you got test user credentials. The next page will show the authorization code that was granted by HMRC. Copy it to the clipboard, and move on to getting an access token. The authorization code is valid for only 10 minutes. You must retrieve the access token during this time. If you don't retrieve the access token within 10 minutes, and the authorization code expires, you can get a new authorization code by using the same test user credentials. Alternatively, you can get a new test user.

## Obtain an authorization code for production

When a company is ready to interoperate in real life with MTD for VAT, it must create an HMRC online account and link it to the Finance and Operations application by selecting **Microsoft Dynamics 365 for Finance and Operations** as the software. The company will then receive credentials that are linked to its VAT registration number:

- **User ID** – The name that is used to access HMRC while an authorization code is being requested.
- **Password** – The password that is used to access HMRC while an authorization code is being requested

After the company has user credentials, an authorization process can be initialized. Two steps must be done before your system is ready to interoperate with HMRC:

- Get an authorization code.
- Get an access token.

To get an authorization code from HMRC, go to **Tax** \> **Setup** \> **Electronic messages** \> **Web applications**, select the web application that you want to authorize for (**Dynamics 365 for Finance and Operations**), and select **Get authorization code**. Select **OK** to confirm that you want to initialize the authorization process. On the **Electronic report parameters** page, set the **Scope** field. The following values are allowed by HMRC:

- read:vat
- write:vat
- read:vat write:vat

We recommend that you enter **read:vat write:vat** in this field, because the same application must be used for both GET and POST HTTPS requests to the web service. Select **OK** to address the authorization request to HMRC. You're redirected to the HMRC portal for authorization. On the **Sign in** page, enter the **User ID** and **Password** values that HMRC granted when the HMRC online account was created. The next page will show the authorization code. Copy it to the clipboard, and move on to getting an access token. The authorization code is valid for only 10 minutes. You must retrieve the access token during this time. If you don't retrieve the access token within 10 minutes and the authorization code expires, you may get a new authorization code.

## Obtain an access token

Initialize retrieval of an access token within 10 minutes from the moment when an authorization code is generated by HMRC.

Go to **Tax** \> **Setup** \> **Electronic messages** \> **Web applications**, select the web application that you want to authorize for (**Sandbox HMRC** for testing purposes or **Dynamics 365 for Finance and Operations** for production). On the **Web applications** page, select **Obtain access token** on the Action Pane to request an access token from HMRC. Paste the authorization code that you copied to the clipboard from the HMRC portal earlier, and then select **OK**. The access token request is sent to HMRC, and the access token will be automatically saved in Finance and Operations from HMRC's response. You can't review the token from the user interface. However, the **Access token will expire in** field shows the validity period of the access toke.

Each access token is valid for four hours from the moment when it's created by HMRC. To receive a new access token, you don't have to renew an authorization code. You just have to refresh the access token. To manually initiate a refresh of an access token, on the **Web applications** page, select **Refresh access token** on the Action Pane. A refresh access token request is sent to HMRC, and a new access token will be automatically saved in the system from HMRC's response.

You don't have to manually refresh an access token every four hours or before you start to interoperate with HMRC. During interoperation with HMRC, the process of refreshing the access token is automatically initialized and is hidden from user.

## Retrieve VAT obligations from HMRC

After the web application is initialized and authorized, the system is ready to interoperate with HMRC.

Go to **Tax** \> **Inquires and reports** \> **Electronic messages** \> **Electronic messages**, and select either the **UK MTD VAT TEST** processing (for testing purposes) or the **UK MTD VAT returns** processing (for real-life interoperation with the production HMRC web application). The page shows information about VAT obligations and returns, and is used for interoperation with the HMRC web service. Select **New** on **Messages** FastTab, select the **Create VAT obligation request** action, and then select **OK**. A new electronic message is created and has a status of **New obligation request**. Fill in the following fields.

| Field       | Description |
|-------------|-------------|
| From date   | This field is mandatory for an electronic message that retrieves VAT obligations. It defines the start date of the period for which to get information about VAT obligations from HMRC. |
| To date     | This field is mandatory for an electronic message that retrieves VAT obligations. It defines the end date of the period for which to get information about VAT obligations from HMRC. |
| Description | This field is optional for an electronic message that retrieves VAT obligations. Enter a description of the electronic message. |

The **Action log** FastTab saves information about the user, and the date and time when the electronic message was created.

No additional fields are applicable to this type of electronic message.

Select **Send report** to initialize the retrieval of VAT obligation information from HMRC. In the **Run processing** dialog box, the **Retrieve VAT obligations** action is automatically defined, and information is filled in by the system. Select **OK**. A request in JSON format is created and addressed to the HMRC web application. A response from HMRC will be received and attached to the electronic message. Based on the response, either new electronic messages for the VAT return will be created, or existing electronic messages will be updated.

HMRC uniquely identifies each VAT return period via a **periodKey** parameter. This parameter is stored in Finance and Operation. However, according to HMRC requirements, its value must be hidden in the user interface. Users must not be able to see the **periodKey** value from the user interface.

The **periodKey** additional field is used to store the **periodKey** value in both the **UK MTD VAT TEST** processing and the **UK MTD VAT returns** processing. This field is set up as a hidden field, so that users can't see its value. To accommodate HMRC requirements, we don't recommend that you change this setup for the **periodKey** additional field.

The following illustration show the lifecycle of electronic message processing for the retrieval of VAT obligations.

![Lifecycle of electronic message processing for VAT obligation retrieval](media/mkd-process.png)

The last step of the processing is an **Import VAT obligations** action of the **Electronic reporting import** type. On this step, the system defines the following behavior:

- If a VAT obligation from the response doesn't exist in the database, and the status of this VAT obligation in HMRC is **Open**, a new electronic message is created that has a status of **New VAT return**.
- If a VAT obligation from the response doesn't exist in the database, and the status of this VAT obligation in HMRC is **Fulfilled**, a new electronic message is created that has a status of **Completed VAT return**.
- If a VAT obligation from the response does exist in the database, the system verifies and syncs the values of the **HMRC status**, **Due date**, and **Received date** additional fields with the information from the response.

All the actions that are done for electronic messages are logged and can be viewed on the **Log** FastTab.

## Test "Gov-Test-Scenario" for the "Retrieve VAT obligations" endpoint in the HMRC sandbox

HMRC lets you simulate different scenarios of VAT obligation retrieval on the sandbox web application. For example, "QUARTERLY\_NONE\_MET" simulates the scenario where the client has quarterly obligations, and none are fulfilled. You can find related information in the "Endpoints" paragraph of the "VAT" subscription API documentation.

To try different scenarios in sandbox application, go to **Workspaces** \> **Electronic reporting** \> **Reporting configurations**, and select **MTD VAT web request headers format (UK)** under **Electronic Messages framework model**. Derive a new child format configuration under **MTD VAT web request headers format (UK)**, and open it in the designer. Find the **File** \> **JSON Object** \> **Gov-Test-Scenario** property, expand it, and select **String** under it. Define the scenario that you want to test as the **String** value.

Here is an example.

![String value example](media/emea-gbr-format-designer-string.png)

Make sure that the **Gov-Test-Scenario** property is enabled in the format. On the **Mapping** tab, verify that the **Enabled** property value of the **Gov-Test-Scenario** node is either blank or set to **true**. To change the value of the **Enabled** property, select the **Edit** button (pencil symbol) near it.

![JSON object](media/emea-gbr-format-designer-json-object.png)

Save and complete the format. To enable the system to use the new format (where the **Gov-Test-Scenario** property is enabled) instead of the parent format for generation of the request to HMRC, go to **Tax** \> **Setup** \> **Electronic messages** \> **Web service settings**, select the **HMRC sandbox GET** web service, and select your new format instead of **MTD VAT web request headers format (UK)** in the **Request headers format mapping** field.

Change the **Gov-Test-Scenario** property in the new format for all the scenarios that you want to test. Clean up the **Gov-Test-Scenario** property in the format, and complete it when you've finished testing.

### Collect data for VAT return

The process of preparing and submitting a VAT return for a period is based on sales tax payment transactions that were posted during the [Settle and post sales tax](https://docs.microsoft.com/dynamics365/unified-operations/financials/general-ledger/tasks/create-sales-tax-payment) job in Finance and Operations. For more information about sales tax settlement and reporting, see [Sales tax overview](https://docs.microsoft.com/dynamics365/unified-operations/financials/general-ledger/indirect-taxes-overview).

Before you start to prepare and submit a VAT return to HMRC, complete the regular **Settle and post sales tax** job for the period that you will report to HMRC. When this job is run, new sales tax payment transactions are created. Go to **Tax** \> **Inquires and reports** \> **Sales tax inquires** \> **Sales tax payments** to view the sales tax payments. You can review the resulting values for each sales tax payment transaction on the **VAT 100** report in SSRS or Excel format. For information about how to define the format that is used, see the [Set up General ledger parameters](#vat-statement-format-mapping) section of this topic. To generate a **VAT 100** report for selected sales tax payment transactions, select **Print report** on the Action Pane.

In Finance and Operations, you can run the **Settle and post sales tax** job several times for the same period before you submit a VAT return to HMRC. All the sales tax payment transactions can be included on the same VAT return report for a period. The transactions that the system fills in for reporting depend on the sales tax settlement period that is defined in the **Populate VAT return records** action for the processing. For more information, see the [Define a sales tax settlement period](#define-a-sales-tax-settlement-period) section of this topic.

> [!IMPORTANT]
> MTD for VAT lets you do submit a VAT return only one time for each reporting period. As HMRC states on the official website, the current amendment process will stay in place for VAT:
>
> - If the net value of the errors in a VAT return is less than £10,000, the company will do the amendment in the next VAT return.
> - If the net value of the errors in a VAT return is more than £10,000, the company must complete the VAT 652 form that is available on the GOV.UK website.

When the **Settle and post sales tax** job is completed, you can start to prepare a report for electronic submission. The first step of data preparation is to collect sales tax payment transactions that are related to the period. Go to **Tax** \> **Inquires and reports** \> **Electronic messages** \> **Electronic messages**, and select either the **UK MTD VAT TEST** processing (for testing purposes) or the **UK MTD VAT returns** processing (for real-life interoperation with the production HMRC web application). On the **Message** FastTab, select the electronic message that is related to the period you want to submit a VAT return for. Don't update the **Start date** and **End date** fields of the record. These values are received from HMRC and will be used as criteria for collecting sales tax payment transactions. You can add a description of the electronic message. Collection of VAT data is available only for electronic messages that have a status of **New VAT return**.

To start to collect sales tax payment transactions, select **Collect data** on the **Message** FastTab. The **Populate VAT return records** action is predefined in the **Run processing** dialog box. Select **OK**. The system collects the sales tax payment transactions that were posted in the period that is defined by the **From date** and **To date** fields, and it enters those transactions as electronic message items of the message. You can review the transactions on the **Message items** FastTab.

If, for some reason, a sales tax payment transaction that the system entered must be excluded from the report, you can delete it. Alternatively, you can update its status to **Excluded** by selecting **Update status** on the **Message items** FastTab. Transactions that have a status of **Excluded** aren't considered for reporting. You can also change the status of a transaction from **Excluded** back to **Populated** by selecting **Update status** on the **Message items** FastTab.

You can repeatedly select **Collect data** on the **Message** FastTab until the electronic message is moved to the next status. When data is collected, select **Update status** on the **Messages** FastTab. The **Ready to generate VAT return** status is predefined in the **Update status** dialog box. Select **OK** to mark the electronic message as ready for report generation. The status of the electronic message items that are linked to the electronic message is updated to **To be reported**. If, for some reason, you must go back to the previous step and continue to collect data or change electronic message items status, select **Update status** on the **Messages** FastTab, select **New VAT return** in the **New status** field, and then select **OK**.

All the actions for the electronic message are reflected on the **Action log** FastTab.

After an electronic message has a status of **Ready to generate VAT return**, you can initialize report generation. Two generation options are available:

- **Preview VAT return** – The file will be generated in Excel format and attached to the electronic message. No statuses will be changed.
- **Generate file for submission** – The file will be generated in JSON format and attached to the electronic message. The status of the electronic message will be updated to **Generated VAT return**, and the status of the linked electronic message items will be updated to **Reported**.

### Generate a VAT return in Excel format for preview

To generate a VAT return in **VAT 100 report** format in Excel, go to **Tax** \> **Inquires and reports** \> **Electronic messages** \> **Electronic messages**, and select either the **UK MTD VAT TEST** processing (for testing purposes) or the **UK MTD VAT returns** processing (for real-life interoperation with the production HMRC web application). On the **Messages** FastTab, select the electronic message record that is related to the period that you want to generate a file for, and then select **Generate report**. The **Generate report** button is available only for electronic messages that have the following statuses:

- **Ready to generate VAT return** – The user changes the electronic message status to this value by using the **Update status** button.
- **Error VAT return generation** – If an error occurs during report generation, the electronic message status is changed to this value.
- **Error VAT return submission** – If an error occurs during report submission, the electronic message status is changed to this value. The response that includes a description of the error is attached to the action log.

In the **Run processing** dialog box, select the **Preview VAT return** action, and then select **OK**. The file will be generated in Excel format and attached to the electronic message. No statuses will be changed. To view the file, select the electronic message, and then select the **Attachments** button (paper clip symbol) in the upper-right corner of the page. On the **Attachments** page for the selected message, select the last attachment (**VAT statement.xlsx**), and then select **Open** on the Action Pane. The file is opened in Excel.

You can regenerate the **VAT 100** report several times before you generate the report in JSON format. At that point, the electronic message status will be changed to **Generated VAT return**.

### Generate a VAT return in JSON format

MTD for VAT accepts VAT returns in JSON format only. To generate a VAT return in JSON format, go to **Tax** \> **Inquires and reports** \> **Electronic messages** \> **Electronic messages**, and select either the **UK MTD VAT TEST** processing (for testing purposes) or the **UK MTD VAT returns** processing (for real-life interoperation with the production HMRC web application). On the **Messages** FastTab, select the electronic message record that is related to the period that you want to generate a file for, and then select **Generate report**. The **Generate report** button is available only for electronic messages that have the following statuses:

- **Ready to generate VAT return** – The user changes the electronic message status to this value by using the **Update status** button.
- **Error VAT return generation** – If an error occurs during report generation, the electronic message status is changed to this value.
- **Error VAT return submission** – If an error occurs during report submission, the electronic message status is changed to this value. The response that includes a description of the error is attached to the action log.

In the **Run processing** dialog box, select the **Generate file for submission** action, and then select **OK**. The file will be generated in JSON format and attached to the electronic message. The electronic message status will be updated to **Generated VAT return**, and the status of the electronic message items that are linked to the electronic message will be updated to **Reported**. To view the file, select the electronic message, and then select the **Attachments** button (paper clip symbol) in the upper-right corner of the page. On the **Attachments** page for the selected message, select the last attachment (**VAT\_return.json**), and then select **Open** on the Action Pane.

If, for some reason, you must regenerate a VAT return in JSON format before it's submitted to HMRC, use the **Update status** button on the **Messages** FastTab to update the status of the related electronic message to either **New VAT return** or **Ready to generate VAT return**, depending on whether you must go back to the data collection step or the file generation step.

### Submit VAT returns to HMRC

When a VAT return in JSON format is generated and ready to be submitted to HMRC, you can initialize its submission to the MTD for VAT web application. The last JSON file that was attached to the electronic message will be used for the submission. To avoid any discrepancy, we recommended that you delete any unnecessary JSON files that are attached to the electronic message that you will submit to HMRC. To find and clean up unnecessary attachments, select the electronic message, and then select the **Attachments** button (paper clip symbol) in the upper-right corner of the page. The **Attachments** page for the selected message is opened.

To start submission, go to **Tax** \> **Inquires and reports** \> **Electronic messages** \> **Electronic messages**, and select either the **UK MTD VAT TEST** processing (for testing purposes) or the **UK MTD VAT returns** processing (for real-life interoperation with the production HMRC web application). On the **Messages** FastTab, select the electronic message record that is related to the period that you want to submit the VAT return for, and then select **Send report**. The **Send report** button is available only for electronic messages that have the following statuses:

- **Generated VAT return** – The electronic message status is automatically updated to this value when a VAT return in JSON format is successfully generated and attached to the electronic message.
- **Error VAT return submission** – If an error occurs during report submission, the electronic message status is changed to this value. The response that includes a description of the error is attached to the action log.

In the **Run processing** dialog box, the **Submit VAT return** action is predefined. Select **OK**. A dialog box appears that contains mandatory declaration text that is required by HMRC. We recommended that you not modify or delete this declaration text in the setup of the **Submit VAT return** action, to remain compliant with HMRC requirements. By selecting **OK** in this dialog box, you submit VAT information, and confirm that the information is true and complete. A false declaration can result in prosecution.

A VAT return can be submitted to HMRC just one time for each period. Therefore, make sure that you want to submit the VAT return before you accept the declaration. If you aren't sure that the VAT return is ready to be submitted, select **Cancel**. When you select **OK**, the VAT return in JSON format that is related to the selected electronic message is submitted to HMRC. If the VAT return is successfully submitted to HMRC, the status of the electronic message is updated to **Sent VAT return**, and the response from HMRC is attached to the electronic message.

Next, the system automatically runs the **Import response for VAT return** action. This action reflects information from the response in the **Processing date** additional field of the electronic message, updates the status of the electronic message to **Completed VAT return**, and updates the status of the electronic message items to **Submitted**. If, for some reason, the **Import response for VAT return** action isn't automatically run, you can manually initialize it by selecting **Import response** on the **Messages** FastTab. The **Import response** button is available only for electronic messages that have the following status:

- **Sent VAT return** – The electronic message status is automatically updated to this value when a VAT return in JSON format is successfully submitted to the electronic message.

All the actions for the electronic message are reflected on the **Action log** FastTab.

### Retrieve VAT liabilities and payments from HMRC

HMRC lets you retrieve information about VAT liabilities and VAT payments. Therefore, the MTD for VAT web applications support specific endpoints.

The **UK MTD VAT returns** processing includes actions that let you retrieve information about VAT liabilities and VAT payments from HMRC.

To retrieve information about VAT payments, go to **Tax** \> **Inquires and reports** \> **Electronic messages** \> **Electronic messages**, and select the **UK MTD VAT returns** processing. On the **Messages** FastTab, select **New**. In the **Run processing** dialog box, select the **Create VAT payments request** action, and then select **OK**. An electronic message that has a status of **New payments request** is created. Specify the "from" date and "to" date for the electronic message to define the period that you want to retrieve VAT payment information from HMRC for. On the **Messages** FastTab, select **Send report**. In the **Run processing** dialog box, the **Request VAT payments** action is predefined. Select **OK**. A request is sent to HMRC, and a response that contains information about VAT payments is attached to the electronic message as a file in JSON format. To view the file, select the electronic message, and then select the **Attachments** button (paper clip symbol) in the upper-right corner of the page. On the **Attachments** page for the selected message, select the last attachment, and then select **Open** on the Action Pane.

To retrieve information about VAT liabilities, go to **Tax** \> **Inquires and reports** \> **Electronic messages** \> **Electronic messages**, and select the **UK MTD VAT returns** processing. On the **Messages** FastTab, select **New**. In the **Run processing** dialog box, select the **Create VAT liabilities request** action, and then select **OK**. An electronic message that has a status of **New liabilities request** is created. Specify the "from" date and "to" date for the electronic message to define the period that you want to retrieve VAT liability information from HMRC for. On the **Messages** FastTab, select **Send report**. In the **Run processing** dialog box, the **Request VAT liabilities** action is predefined. Select **OK**. A request is sent to HMRC, and a response that contains information about VAT liabilities is attached to the electronic message as a file in JSON format. To view the file, select the electronic message, and then select the **Attachments** button (paper clip symbol) in the upper-right corner of the page. On the **Attachments** page for the selected message, select the last attachment, and then select **Open** on the Action Pane.

## Security privileges

The following security privileges are available for electronic messages.

| Security privilege           | Access level description | Association |
|------------------------------|--------------------------|-----------------|
| Maintain electronic messages | This privilege gives full access to the Electronic messages functionality. It lets the user set up electronic messaging and run all the processing. | This privilege is included in the **Maintain sales tax transactions** security duty. That duty, in turn, is included in the **Accountant** security role. |
| View electronic messages     | This privilege gives read-only access to the Electronic messages functionality. It lets the user view both the electronic messaging settings and messages/items. However, it doesn't let the user set up or run anything. | This privilege is included in the **Inquire into sales tax transaction status** security duty. That duty, in turn, is included in the following security roles:<ul><li>Collections manager</li><li>Accounts receivable clerk</li><li>Accounts receivable manager</li><li>Tax accountant</li><li>Accountant</li><li>Accounting manager</li><li>Accounting supervisor</li><li>Sales manager</li><li>Accounts payable clerk</li></ul> |
| Operate electronic messages  | This privilege gives access only to the **Electronic messages** and **Electronic message items** pages. It lets the user run all the processing that is called from those pages. | This privilege is included in the **Operate electronic messages** security duty. That duty, in turn, is included in the **Electronic messages operator** security role. |

## Appendix 1: Electronic messages setup for MTD for VAT

This appendix provides information about the setup of Electronic messages functionality so that it supports both the **UK MTD VAT TEST** processing (for testing purposes) and the **UK MTD VAT returns** processing (for real-life interoperation with the production HMRC web application). Use this information to determine whether the Electronic messages functionality is set up correctly.

Although this appendix includes the most important information about the setup, it doesn't include all the data. We recommend that you use a package of data entities that provides a predefined setup of the functionality, and that includes all the data that is required in order to set up of the processing to interoperate with MTD for VAT.

### Electronic message processing

The following types of processing are defined to support interoperation with MTD for VAT.

| Name               | Description |
|--------------------|-------------|
| UK MTD VAT TEST    | The testing process for the preparation and submission of VAT returns to the HMRC sandbox. |
| UK MTD VAT returns | The process of preparing and submitting VAT returns to HMRC. |

Security roles should be defined for both types of processing to limit access to them (at the record level).

### Web applications

The following web applications are used by the **UK MTD VAT TEST** and **UK MTD VAT returns** processing.

| Name                                    | Description                                              |
|-----------------------------------------|----------------------------------------------------------|
| Dynamics 365 for Finance and Operations | HMRC Web application for Finance and Operations          |
| Sandbox HMRC                            | HMRC sandbox for Dynamics 365 for Finance and Operations |

The following table shows the parameters of the web applications.

| Parameter                                            | Value                                  |
|------------------------------------------------------|----------------------------------------|
| Base URL for Dynamics 365 for Finance and Operations | `https://api.service.hmrc.gov.uk`      |
| Base URL for Sandbox HMRC                            | `https://test-api.service.hmrc.gov.uk` |
| Authorization URL path                               | /oauth/authorize                       |
| Token URL path                                       | /oauth/token                           |
| Redirect URL                                         | urn:ietf:wg:oauth:2.0:oob              |
| Authorization format mapping                         | MTD VAT authorization format (UK)      |
| Import token model mapping                           | MTD VAT import token format (UK)       |

Additionally, security roles should be defined for both web applications to limit access to the access token.

### Web service settings

The following web services are used by the **UK MTD VAT TEST** and **UK MTD VAT returns** processing.

| Name                | Description                                                              | Web application                         |
|---------------------|--------------------------------------------------------------------------|-----------------------------------------|
| HMRC GET            | The HMRC web service for GET requests.                                   | Dynamics 365 for Finance and Operations |
| HMRC POST           | The HMRC web service for POST requests.                                  | Dynamics 365 for Finance and Operations |
| HMRC sandbox GET    | The sandbox that is used to test the HMRC web service for GET requests.  | Sandbox HMRC                            |
| HMRC sandbox POST   | The sandbox that is used to test the HMRC web service for POST requests. | Sandbox HMRC                            |
| HMRC TEST USER POST | The HMRC web service that is used to POST test user requests.            | Sandbox HMRC                            |

The following table shows the shared parameters for all these web services.

| Parameter                     | Value                                   |
|-------------------------------|-----------------------------------------|
| Request type – XML            | NO                                      |
| Accept                        | application/vnd.hmrc.1.0+json           |
| Content type                  | application/json                        |
| Request header format mapping | MTD VAT web request headers format (UK) |

### Additional fields

The following additional fields are used by the **UK MTD VAT TEST** and **UK MTD VAT returns** processing.

| Field           | Description |
|-----------------|-------------|
| Due date        | The due date for the obligation period. This field can't be changed by the user. |
| HMRC status     | The obligation status in HMRC:<ul><li><strong>O</strong> – Open</li><li><strong>F</strong> – Fulfilled</li></ul>This field can't be changed by the user. |
| periodKey       | The ID code for the period that the obligation belongs to. This field can't be changed by the user. It's also hidden and can't be seen by the user. |
| Processing date | The time when the message was processed by HMRC. This field can't be changed by the user. |
| Received date   | The date when the obligation was received by HMRC. This field can't be changed by the user. |

### Electronic message item types

The setup of electronic messages for both the **UK MTD VAT TEST** processing (for testing purposes) and the **UK MTD VAT returns** processing (for real-life interoperation with the production HMRC web application) uses one type of electronic message item: **VAT return**.

### Electronic message item statuses

The following electronic message item statuses are used by the **UK MTD VAT TEST** and **UK MTD VAT returns** processing.

| Status         | Description |
|----------------|-------------|
| Populated      | The record has been filled in from sales tax payments. Records that have this status can be deleted. |
| Excluded       | The record is excluded from report generation. Records that have this status can be deleted. |
| To be reported | The line will be included in the VAT return for submission. Records that have this status can't be deleted. |
| Reported       | The record has been included in a VAT declaration file. Records that have this status can't be deleted. |
| Sent           | The record has been sent to HMRC in a VAT declaration. Records that have this status can't be deleted. |
| Submitted      | The record has been submitted to HMRC. Records that have this status can't be deleted. |

### Electronic message statuses

The following electronic message statuses are used by the **UK MTD VAT TEST** and **UK MTD VAT returns** processing.

| Status                             | Description |
|------------------------------------|-------------|
| New obligation request             | New electronic message to retrieve VAT obligations. Record in this status can be deleted. |
| Retrieved VAT obligation           | VAT obligations request is sent. Record in this status can be deleted. |
| Error VAT obligations retrieving   | A technical error occurred on VAT obligations retrieving. Record in this status can be deleted. |
| Completed VAT obligations request  | VAT obligations are successfully retrieved. Record in this status can be deleted. |
| Error VAT obligations importing    | A technical error occurred on VAT obligations import. |
| New VAT return                     | This Sales tax payment is included for further submission. Record in this status can be deleted. |
| Ready to generate VAT return       | The message is ready to generate VAT return. Record in this status can be deleted. |
| Generated VAT return               | VAT return JSON file is generated and attached to the mess. Record in this status *can't* be deleted. |
| Error VAT return generation        | A technical error occurred on generation of GER report. Record in this status can be deleted.|
| Sent VAT return                    | VAT return is sent to HMRC in JSON format. Record in this status *can't* be deleted. |
| Error VAT return submission        | Error occurred while VAT return submission. Record in this status can be deleted. |
| Completed VAT return               | Completed VAT return. Record in this status *can't* be deleted. |
| Error VAT return import response   | A technical error occurred on VAT return importing response. |
| New liabilities request            | New electronic message to request liabilities. Record in this status can be deleted. |
| Error VAT liabilities request      | A technical error occurred on VAT liabilities request. Record in this status can be deleted.|
| Completed VAT liabilities request  | VAT liabilities are successfully retrieved. Record in this status can be deleted. |
| New payments request               | New electronic message to request VAT payments information. Record in this status can be deleted. |
| Error VAT payments request         | A technical error occurred on VAT payments request. Record in this status can be deleted. |
| Completed VAT payments request     | Completed VAT payments request. Record in this status can be deleted. |
| New test user request              | New electronic message to request test user. Record in this status can be deleted. |
| Generated test user request        | Test user JSON file is generated and attached to the message. Record in this status can be deleted. |
| Error test user request generation | A technical error occurred on generation of test user JSON. Record in this status can be deleted. |
| Completed test user request        | Test user request is sent to HMRC in JSON format. Record in this status can be deleted. |
| Error test user request            | Error occurred while test user request submission. Record in this status can be deleted. |

### Action populate records

The **Populate VAT return records** action is used by the **UK MTD VAT TEST** and **UK MTD VAT returns** processing. The following table shows the setup of the data source for the action.

| Property               | Value |
|------------------------|-------|
| Name                   | VAT payment |
| Message item type      | VAT return |
| Account type           | All |
| Master table name      | TaxReportVoucher |
| Document number field  | Voucher |
| Document date field    | TransDate |
| Document account field | TaxPeriod |
| User query             | Yes. Define the settlement period by using **Edit query** button. |

### Electronic message actions

The following electronic message actions are used by the **UK MTD VAT TEST** and **UK MTD VAT returns** processing.

| Name                                  | Description | Action type |
|---------------------------------------|-------------|-------------|
| Create VAT obligation request         | Create a message to retrieve VAT obligations.<ul><li><strong>From statuses:</strong> No</li><li><strong>To statuses:</strong> New obligation request</li></ul> | Create message |
| Retrieve VAT obligations              | Prepare the request to retrieve VAT obligations.<ul><li><strong>From statuses:</strong> Error VAT obligations retrieving, New obligation request</li><li><strong>To statuses:</strong> Error VAT obligations retrieving, Retrieved VAT obligation</li><li><strong>Format mapping for URL path:</strong> "MTD VAT interoperation (UK)"</li><li><strong>Web service:</strong> "HMRC GET"</li><li><strong>File name:</strong> "response.json.txt"</li></ul> | Web service |
| Test retrieve VAT obligations         | Retrieve VAT obligations from the HMRC sandbox.<ul><li><strong>From statuses:</strong> Error VAT obligations retrieving, New obligation request</li><li><strong>To statuses:</strong> Error VAT obligations retrieving, Retrieved VAT obligation</li><li><strong>Format mapping for URL path:</strong> "MTD VAT interoperation (UK)"</li><li><strong>Web service:</strong> "HMRC sandbox GET"</li><li><strong>File name:</strong> "response.json.txt"</li></ul> | Web service |
| Import VAT obligations                | Import the response from HMRC that includes VAT obligations.<ul><li><strong>From statuses:</strong> Retrieved VAT obligation, Error VAT obligations importing</li><li><strong>To statuses:</strong> Completed VAT obligations request, Error VAT obligations importing</li><li><strong>Model mapping:</strong> "MTD VAT obligations importing JSON (UK)"</li></ul> | Electronic reporting import |
| Populate VAT return records           | Enter information in sales tax payment records.<ul><li><strong>From statuses:</strong> New VAT return</li><li><strong>To statuses:</strong> No</li><li><strong>Populates records action:</strong> "Populate VAT return records"</li></ul> | Populate records |
| Exclude from reporting                | Mark the sales tax payment record as excluded from reporting. This action doesn't change the electronic message status. | User processing |
| Update to initial status              | Update the status of the sales tax payment to its initial status. This action doesn't change the electronic message status. | User processing |
| Ready to generate VAT return          | Update the status of the message to **Ready to generate**.<ul><li><strong>From statuses:</strong> New VAT return</li><li><strong>To statuses:</strong> Ready to generate VAT return</li></ul> | Message level user processing |
| Update to initial status VAT return | Update the status of the message to its initial status.<ul><li><strong>From statuses:</strong> Generated VAT return, Ready to generate VAT return, Error VAT return generation, Error VAT return import response. </li><li><strong>To statuses:</strong> New VAT return, Ready to generate VAT return</li></ul> | Message level user processing |
| Preview VAT return                    | Generate a preview file in Excel format.<ul><li><strong>From statuses:</strong> Error VAT return generation, Error VAT return submission, Ready to generate VAT return</li><li><strong>To statuses:</strong> Error VAT return generation, Ready to generate VAT return</li><li><strong>Format mapping:</strong> "VAT Declaration Excel (UK)"</li><li><strong>File name:</strong> "VAT statement.xlsx"</li></ul> | Electronic reporting export message |
| Generate file for submission          | Generate a VAT return file in JSON format for submission to HMRC.<ul><li><strong>From statuses:</strong> Error VAT return generation, Error VAT return submission, Ready to generate VAT return</li><li><strong>To statuses:</strong> Error VAT return generation, Generated VAT return</li><li><strong>Format mapping:</strong> "VAT Declaration JSON (UK)"</li><li><strong>File name:</strong> "VAT\_return.json"</li></ul> | Electronic reporting export message |
| Submit VAT return                     | Submit the VAT return that is generated in JSON format to HMRC.<ul><li><strong>From statuses:</strong> Error VAT return submission, Generated VAT return</li><li><strong>To statuses:</strong> Error VAT return submission, Sent VAT return</li><li><strong>Message item type:</strong> "VAT return"</li><li><strong>Format mapping for URL path:</strong> "MTD VAT interoperation (UK)"</li><li><strong>Web service:</strong> "HMRC POST"</li><li><strong>File name:</strong> "response.json"</li></ul> | Web service |
| Test submit VAT return                | Test submission of the VAT return to the HMRC sandbox.<ul><li><strong>From statuses:</strong> Error VAT return submission, Generated VAT return</li><li><strong>To statuses:</strong> Error VAT return submission, Sent VAT return</li><li><strong>Message item type:</strong> "VAT return"</li><li><strong>Format mapping for URL path:</strong> "MTD VAT interoperation (UK)"</li><li><strong>Web service:</strong> "HMRC sandbox POST"</li><li><strong>File name:</strong> "response.json"</li></ul> | Web service |
| Import response for VAT return        | Import a response from HMRC about the VAT return that was submitted.<ul><li><strong>From statuses:</strong> Sent VAT return, Error VAT return import response</li><li><strong>To statuses:</strong> Completed VAT return, Error VAT return import response</li><li><strong>Model mapping:</strong> "MTD VAT return response importing JSON (UK)"</li></ul> | Electronic reporting import |
| Create VAT liabilities request        | Create a message to request VAT liabilities.<ul><li><strong>From statuses:</strong> No</li><li><strong>To statuses:</strong> New liabilities request</li></ul> | Create message |
| Request VAT liabilities               | Request VAT liabilities.<ul><li><strong>From statuses:</strong> Error VAT liabilities request, New liabilities request</li><li><strong>To statuses:</strong> Completed VAT liabilities request, Error VAT liabilities request</li><li><strong>Format mapping:</strong> "MTD VAT interoperation (UK)"</li><li><strong>Web service:</strong> "HMRC GET"</li><li><strong>File name:</strong> "response.json.txt"</li></ul> | Web service |
| Create VAT payments request           | Create a message to request VAT payments.<ul><li><strong>From statuses:</strong> No</li><li><strong>To statuses:</strong> New payments request</li></ul> | Create message |
| Request VAT payments                  | Request VAT payments.<ul><li><strong>From statuses:</strong> Error VAT payments request, New payments request</li><li><strong>To statuses:</strong> Completed VAT payments request, Error VAT payments request</li><li><strong>Format mapping:</strong> "MTD VAT interoperation (UK)"</li><li><strong>Web service:</strong> "HMRC GET"</li><li><strong>File name:</strong> "response.json.txt"</li></ul> | Web service |
| Create test user request              | Create a message to request a test user.<ul><li><strong>From statuses:</strong> No</li><li><strong>To statuses:</strong> New test user request</li></ul> | Create message |
| Generate test user request            | Generate a JSON file to request a test user.<ul><li><strong>From statuses:</strong> Error test user request, New test user request</li><li><strong>To statuses:</strong> Error test user request, Generated test user request</li><li><strong>Format mapping:</strong> "MTD VAT interoperation (UK)"</li><li><strong>File name:</strong> "TestUserRequest.json"</li></ul> | Electronic reporting export message |
| Send test user request                | Send a JSON request for a test user.<ul><li><strong>From statuses:</strong> Error test user request, Generated test user request</li><li><strong>To statuses:</strong> Completed test user request, Error test user request</li><li><strong>Format mapping:</strong> "MTD VAT interoperation (UK)"</li><li><strong>Web service:</strong> "HMRC TEST USER POST"</li><li><strong>File name:</strong> "TestUserInfo.txt"</li></ul> | Web service |

### Electronic processing actions

The following electronic processing actions are used by the **UK MTD VAT TEST** processing.

| Name                                | Run separately | Inseparable sequence |
|-------------------------------------|----------------|----------------------|
| Create test user request            | Yes            |                      |
| Generate test user request          | Yes            | TestUser             |
| Send test user request              | No             | TestUser             |
| Create VAT obligation request       | Yes            |                      |
| Test retrieve VAT obligations       | Yes            | Obligation           |
| Import VAT obligations              | No             | Obligation           |
| Populate VAT return records         | Yes            |                      |
| Exclude from reporting              | Yes            |                      |
| Update to initial status            | Yes            |                      |
| Ready to generate VAT return        | Yes            |                      |
| Update to initial status VAT return | Yes            |                      |
| Preview VAT return                  | Yes            |                      |
| Generate file for submission        | Yes            |                      |
| Test submit VAT return              | Yes            | Submission           |
| Import response for VAT return      | No             | Submission           |

The following electronic processing actions are used by the **UK MTD VAT returns** processing.

| Name                                | Run separately | Inseparable sequence |
|-------------------------------------|----------------|----------------------|
| Create VAT obligation request       | Yes            |                      |
| Retrieve VAT obligations            | Yes            | Obligation           |
| Import VAT obligations              | No             | Obligation           |
| Populate VAT return records         | Yes            |                      |
| Exclude from reporting              | Yes            |                      |
| Update to initial status            | Yes            |                      |
| Ready to generate VAT return        | Yes            |                      |
| Update to initial status VAT return | Yes            |                      |
| Preview VAT return                  | Yes            |                      |
| Generate file for submission        | Yes            |                      |
| Submit VAT return                   | Yes            | Submission           |
| Import response for VAT return      | No             | Submission           |
| Create VAT liabilities request      | Yes            |                      |
| Request VAT liabilities             | Yes            |                      |
| Create VAT payments request         | Yes            |                      |
| Request VAT payments                | Yes            |                      |
