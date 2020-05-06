  ---
# required metadata

title: Customer electronic invoices
description: This topic provides information about customer electronic invoices management for Italy.
author: v-oloski
manager: 
ms.date: 04/24/2020
ms.topic: article
ms.: 
ms.service: dynamics-ax-applications
ms.technology: 

# optional metadata

# ms.search.form:
audience: Application User
# ms.devlang: 
ms.reviewer: 
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
# ms.custom
ms.search.region: Italy
# ms.search.industry: 
ms.author: v-oloski
---

# Customer electronic invoices

[!include [banner](../includes/banner.md)]

This topic describes how to set up and work with the functionality for creation
and sending sales and project invoices in electronic format (FatturaPA).  
  
Electronic invoices "FatturaPA" version 1.2 can be used for all types of businesses, including public administrations, private
and professional companies. Specifically, the invoices in question must be in .xml format, must be endorsed by using a qualified or digital electronic signature, and must be transmitted through an interchange data system or an authorized intermediary on the websites.

This topic contains:
- [Setup](/setup).
- [How to fill in data for CIG and CUP ouput](/How-to-fill-in-data-for-CIG-and-CUP-ouput).
- [Overview of electronic invoices page](/overview-of-electronic-invoices-page).

# Setup

Before starting work with the electronic invoice functionality, it is
necessary to fulfil the following settings:
- [Accounts receivable parameters](/accounts-receivable-parameters).
- [E-invoice parameters](/e-invoices-parameters).
- [Electronic documents properties](/electronic-document-properties)
- [Customers](/customers).
- [Digital certificate](/digital-certificates).
- [Destination for xml file output](/destination-for-xml-file-output) (optional).

## Accounts receivable parameters

Select the configurations which are used for creation electronic invoices xml
files for Sales and Free text invoices, Sales and Free text credit notes,
Project invoice, Project credit notes (**Accounts receivable \> Setup \>
Accounts receivable parameters**, **Electronic documents** tab).

![Accounts receivable parameters](media/emea-ita-electronic-invocies-AR-parameter-e-invoices.png)

 > [!NOTE] 
 > It is necessary to import the configurations before their selection.
 >   See [Download Electronic reporting configurations from Lifecycle Services](https://docs.microsoft.com/en-us/dynamics365/unified-operations/dev-itpro/analytics/download-electronic-reporting-configuration-lcs).

## E-Invoices parameters

**Accounts receivable \> Setup \> Electronic invoice parameters**)

Use these parameters to specify business scenarios and company specific information (**General**, **Company information** and **Art. 2250 Civil code registration** tabs).

On **Number sequences** tab fill in number sequences for e-invoice file number
and transmission number.

## Electronic document properties
Electronic document properties functionality are used for settting output to xml document blocks for different business cases: 
1. VAT registration number for customers who are out of EU and don't have VAT registration codes.  
2. Certified e-mail address (PEC) for private or professional companies.
3. Stamp duty (payable and not payble by customer).
2. Customer's representative data 

For the functionality to work, it is necessary to set up:
1. **Electronic document property types** (**Account receivable > Setup > Electronic document property types**) and to which table the document property type is applied. For electronic invoice functionality the **Customers** and **Legal entities** tables are applied (**Applicability** button).
2. Required values in set tables on the level of the customer and the legal entity (**Accounts receivable \> Customers \> All customers, Customer** tab, **Electronic document properties** button and **Organization administration > Organizations > Legal entities**, **Electronic document properties** button.

Set values are used for output to the xml file blocks (see the table bellow how to fiil and where these values are used).

| Business scenario | Electronic document property type | Electronic document property type description | Applicability (Table) | Where to use | Element in the xml file |
|-------------------|-----------------------------------|-----------------------------------------------|-----------------------|--------------|-------------------------|
| For customers who are out of EU and don't have VAT registration codes VAT registration number should be 00000000000 | **VATnonEU** | For example: Customer, non-EU VAT number|**CustTable** (Customers) | **Customer, Electronic document properties**, Value=00000000000 |**IdCodice** (CessionarioCommittente\ DatiAnagrafici\ IdFiscaleIVA block) |
| Certified e-mail address (PEC) for private or professional company | **PEC** | **For example:** Customer, Certified e-mail address | **CustTable** (Customers) | **Customer, Electronic document properties**,   Value= < PEC >  | **PECDestinatario** (DatiTrasmissione block) |
| Stamp duty not included into invoice total (for sales invoices) and included/ not included for project invoices | **Bollo** Note. Used for sales order, free text and project invoices | **For example**: Stamp duty, included/ not included into invoice totals | **CompanyInfo** (Legal entities) |**Legal entity, Electronic document properties**,  Value=<Charge code/ Project category, which is used for stamp duties>. **Charges code**: Debit type for this charge code should be Ledger  **Project category**: should be billable | **ImportoBollo** (DatiBollo block) |
| Stamp duty included into invoice total | **BolloPay**. Note. Used only for sales order and free text invoices | **For example**: Stamp duty, included into invoice totals | **CompanyInfo** (Legal entities) | **Legal entity, Electronic document properties**, Value=<Charge code/ Project category, which is used for stamp duties>. **Charges code**: Debit type should be Customer/ Vendor | **ImportoBollo** (DatiBollo block) |
| Representative | TaxRepPaese, TaxRepPaese, TaxRepCodice, TaxRepDenominazione, TaxRepNome, TaxRepCognome | Any description | **CustTable** (Customers) | **Customer, Electronic document properties**. Value=IT (for TaxRepPaese) For other types, fill in data of representative | **Cognome** (RappresentanteFiscale block) |

> [!NOTE 1] In the table:

>  **Customer, Electronic document properties** is **Account receivable > Customers > All customers**, **Customer** tab, **Electronic document properties** button.

> **Legal entity, Electronic document properties** is **Organization administration > Legal entities**, **Electronic document properties** button

> [!NOTE 2]  
> In **Electronic document property types** list page, the **Description** field (left) is filled in automatically when a user is filling **Group description** and **Description** (right) fields.

> [!NOTE 3]
> Electronnic document property type must have the same code as specified in the table.

### How to use project categories for stamp duty

1. Set up Project categories with Fee/Expense transaction type (**Project management and accounting > Setup > Categories > Project categories**). Category Id should be equal to the value defined for **Bollo** on the Legal entity level. (see the table in this section).
2. Project category of Fee transaction type can be used only for stamp duty included in the invoice
3. Project category of expense transaction type can be used both for invoices included and not included in a customer invoice (**Bollo** document property type is used in both casess). 
3. When you create **Fee** or **Expese** journal lines select the category that was defined as stamp duty, enter Cost price. The system considers this cost price as stamp duty amount, 
If you fill in sales price with the cost price amount, the system considers this ammount included in the invoice totals. Sales price amount is equal to zero, this transaction is not included in invoice totals. 



> [!NOTE]
> You can use only one of the journal type (Fee or Exepense) for stamp duty. So if a company uses only payable stamp dute it is possible to use Fee journal type. If a company uses both payable and unpayable stamp duty it is better to use Expense journal type.   


## Customers 

### Authority office 
**Accounts receivable \> Customers \> All customers**, open a customer in **Edit** mode, **Sales demographics** FastTab, **Authority office** field).

The system uses this field value for defining the type of communication (B2G or B2B). If the length of this value is 6 then the customer will be considered as public administration (Transmission Format is **FPA12**) and if the length of this value is 7 then this customer will be considered as private companies or professionals (Transmission Format is **FPR12**). 
In these both cases the system fills in the CodiceDestinatario tag (xml file) with this field value.

![Authority office](media/emea-ita-electronic-invocies-customer-authority-office.png)

If **Authority office** field value is empty, the system considers a customer as a private company or professional (Transmission Format is **FPR12**) and fills in the CodiceDestinatario tag (xml file) with **0000000**.

In this case a certified e-mail address (**PEC**) should be set up (see the table in the [Electronic document properties](/electronic-document-properties) section).

### Activate automatic creation of e-invoices  
**Accounts receivable \> Customers \> All customers,** open a customer in **Edit** mode**, Invoice and delivery** FastTab, **E-INVOICE** field group, **eInvoice registe** option.
If this option is set to **Yes**, the system automatically creates the record in **Electronic customer invoices** page list (see [Overview of electronic invoices page](/overview-of-electronic-invoices-page).

![E-invoice activation](media/emea-ita-electronic-invocies-customer-e-invoice.png)

## Digital Certificates

Open **Accounts receivable \> Setup \> Electronic invoice digital certificates**
This functionality can perform electronic singing of e-Invoices by using either **Company** certificate or **User** certificate.

![digital certificate](media/emea-ita-electronic-invocies-certificate.png)

Each [FatturaPA file](http://www.fatturapa.gov.it/export/fatturazione/en/b-2.htm) that is transmitted to the [Exchange System](http://www.fatturapa.gov.it/export/fatturazione/en/sdi.htm) must be signed by using a qualified signature certificate by the party that is issuing the invoice.  
A qualified signature certificate may be obtained from one of the certifiers in the [list of authorized certifiers](http://www.digitpa.gov.it/firma-digitale/certificatori-accreditati).  
  
The current release supports the **XAdES-BES** signature format.  
To be able to support FatturaPA you must perform the following steps:

-   Install and configure digital certificates that have private and public keys
    in Certificate Server to the **Personal** node on client computers.  
      
  > [!NOTE] 
  > You can do this by using standard Windows functionality.

-   Define Company-level certificates and User-level certificates, as required.

## Destination for xml file output

If it is necessary to output xml files to specified place (for example, SharePoint folder) when invoices are posting (**Print invoice** option must be set to **Yes**), first set up a document type (**Organization administration \> Document management \> Document types**) and then set up a destination (**Organization administration \> Electronic reporting \> Electronic reporting destination**) (see setting details under the links [Configure document management](https://docs.microsoft.com/en-us/dynamics365/fin-ops-core/fin-ops/organization-administration/configure-document-management) and [Electronic reporting (ER) destinations](https://docs.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/analytics/electronic-reporting-destinations)).

> [!NOTE] 
> **Print invoice** option must be set to **Yes** and if destination is set up the e-invoice record for this invoice  is set to **Sent** status automatically.(see **Overview of electronic invoices page**).

Example of setup:

- Document type:

![Document type](media/emea-ita-electronic-invocies-document-type.png)

- Destination for Sales invoice (IT) format:

![Destination](media/emea-ita-electronic-invocies-destination.png)

# How to fill in data for CIG and CUP ouput

Companies may report the following blocks in the output e-invoices: 
 - **DatiOrdineAcquisto** block contains the information relative to the payment order. 
 - **DatiContratto** block contains the information relative to the contract. 
 - **DatiConvenzione** block contains the information relative to the agreement. 
 - **DatiRicezione** block contains the information relative to the data present on the management system used by the PA (Tax Agencies) regarding the reception phase. 
 - **DatiFattureCollegate** block contains the information relative to the invoices previously transmitted and to which the present document is connected; it regards the cases of the forwarding of a credit note and/or invoice pursuant to previous advance payment invoices 

In order to the system could populate these blocks the following fields should be filled in Free text invoice/ Sales order/ Project proposal:
- **Accounts receivable \> Orders \> All sales orders**, **Header**, **Setup** FastTab, **Base document** field group.
- **Accounts receivable \> Invoices \> All free text invoices**, **Header**, **Base document** field group.
- **Project management and accounting \> Projects \> All projects**, **Manage** tab, **Bill** \> **Invoice proposal** button, **Base document** field group

> [!NOTE]
> In which block the system outputs data from **Base document** fields depends on the value specified in the **Base document** field: 
> Payment order - **DatiOrdineAcquisto** block
> Contract - **DatiContratto** block
> Agreement - **DatiConvenzione** block
> Management system - **DatiRicezione** block
> Original invoice - **DatiFattureCollegate** block

# Overview of electronic invoices page 

To overview all customer e-invoices and fulfil different actions open **Electronic customer invoices** page list (**Accounts receivable \> Invoices \> E-invoices \> Electronic invoices**).

In this page list a user can:

-   Select invoice manually by different criteria (Select button). This function
    is useful if the **eInvoice register** option is not set to **Yes** in
    customers.

-   Create xml files, digital signature for selected invoices and send them

-   Export the selected invoice to xml file.
>[NOTE]
>The system outputs a file to the folder set up on your computer (doesn't use the destination settings).   

-   Overview details of the electronic invoice.

> [!NOTE]  
> The similar page list with the same functions is in **Project management
and accounting \> Project invoices \> E-invoices \> Electronic invoices.**

![Customer electronic invoices](media/emea-ita-electronic-invocies-electronic-customer-invoices.png)

 
