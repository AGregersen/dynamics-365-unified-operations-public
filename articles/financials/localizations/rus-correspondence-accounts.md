---
# required metadata

title: About Correspondence 
description: This topic provides information about correspondence in Russia. 
author: ShylaThompson
manager: AnnBe
ms.date: 10/28/2018
ms.topic: article
ms.prod: 
ms.service: dynamics-ax-applications
ms.technology: 
			
# optional metadata

# ms.search.form:  
audience: Application User
# ms.devlang: 
ms.reviewer: shylaw
ms.search.scope: Core, Operations
# ms.tgt_pltfrm: 
# ms.custom: 
ms.search.region: Russia
# ms.search.industry: 
ms.author: shylaw
ms.search.validFrom: 2018-10-28
ms.dyn365.ops.version: 8.1

---

# About Correspondence 

Correspondence of accounts is an approach to continuous and interrelated registration of business transactions in corresponding general ledger accounts, based on the double-entry bookkeeping system. Ledger vouchers are represented by using the Russian accounting standards with corresponding accounts.

You can enter multidimensional transactions in the ledger journals and other modules. In most cases, transactions that are created automatically from other modules are multidimensional. These transactions should be changed to two-dimensional, which could involve splitting ledger transactions. In this case, the following correspondence cases are specified.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Type of correspondence</p></th>
<th><p>Before correspondence</p></th>
<th><p>After correspondence</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>One–to–one</p></td>
<td><p>Account A 200 (debit transaction)</p>
<p>Account B 200 (credit transaction)</p></td>
<td><p>Account A – Account B 200</p>
<p>(two transactions)</p></td>
</tr>
<tr class="even">
<td><p>One–to–many</p></td>
<td><p>Account A 200 (debit transaction)</p>
<p>Account B 160 (credit transaction)</p>
<p>Account C 40 (credit transaction)</p></td>
<td><p>Account A – Account B 160</p>
<p>Account A – Account C 40</p>
<p>(four transactions)</p></td>
</tr>
<tr class="odd">
<td><p>Many–to–one</p></td>
<td><p>Account A 200 (debit transaction)</p>
<p>Account B 160 (debit transaction)</p>
<p>Account C 360 (credit transaction)</p></td>
<td><p>Account A – Account C 200</p>
<p>Account B – Account C 160</p>
<p>(four transactions)</p></td>
</tr>
<tr class="even">
<td><p>Many–to–many</p></td>
<td><p>Account A 200 (debit transaction)</p>
<p>Account B 160 (debit transaction)</p>
<p>Account C 260 (credit transaction)</p>
<p>Account D 100 (credit transaction)</p></td>
<td><p>Individual processing</p>
<p>(multiple transactions)</p></td>
</tr>
</tbody>
</table>


When the **Use corresponding mechanism** check box in the **General ledger parameters** form is cleared, no correspondence relationships are created between transactions.

When the **Use corresponding mechanism** check box is selected, each new accounting transaction that is created consists of a set of two-way corresponding transactions. When the accounting transactions are posted, the corresponding relationship is defined automatically.

If non-corresponding accounts already exist before the account correspondence mechanism is enabled, they are not linked automatically. You must define relationships for these transactions manually.


## Activate corresponding mechanism for accounting transactions 

The account correspondence mechanism allows you to create correspondence relations between transactions. When the account correspondence mechanism is turned on, each new accounting transaction created will consist of a set of two-way corresponding transactions. When posting the accounting transactions, the corresponding relation is defined automatically. If non-corresponded transactions existed before the account correspondence mechanism was turned on, they would not be linked automatically.

1.  Click **General ledger** \> **Setup** \> **General ledger parameters**.

2.  Click **Ledger**, and then select the **Use corresponding mechanism** check box to activate the account correspondence mechanism.

3.  Click **Number sequences** and then select the number sequence code for **Correspondence pack**.


> [!NOTE]
> After the correspondence mechanism is activated, all new transactions will have correspondence relations. If you cannot establish a correspondence link for a transaction, a message with a warning is displayed. Click this message to go to the manual correspondence function to correspond the transactions manually.


## (RUS) Define corresponding relations for transactions manually 

Use the manual transaction correspondence function to define a relationship between non-corresponding transactions. When the account correspondence mechanism is turned off in the ledger, all transactions are generated normally. No correspondence link is established between accounts. The function is not retroactive. When correspondence is turned back on, correspondence will not be established for transactions that were performed earlier.



1.  Click **General ledger** \> **Periodic** \> **Manual correspondence**.

2.  In the left pane view the list of posted vouchers.

3.  On the **Overview** tab to view the voucher transaction.

4.  In the **Show only vouchers** field, select the vouchers to view from the following options:
    
      - **Not corresponded** − View vouchers with no corresponding ledger transactions.
    
      - **Corresponded** − View vouchers with corresponding ledger transactions.
    
      - **All** − View all vouchers.

5.  Click the **Offset** tab.

6.  In the upper pane, select a line under the **Debit transactions** and **Credit transactions** field groups and then click **\<-\>** to correspond, or link, a debit and a credit transaction and move them to the lower pane as a corresponded transaction.
    

    > [!NOTE]
    > You can also drag one transaction over the other to move them to the lower pane as a corresponded transaction.



7.  Click **\<\<-\>\>** to correspond the relationships of all credit and debit vouchers for the selected voucher automatically.

8.  Click **Save** to save the results, or click **Restore** to cancel the last modifications.

9.  Click the **Refresh data** button to refresh the data in the **Manual correspondence** form.
    

    > [!NOTE]
    > After refreshing the data, the voucher for which correspondence has been established will appear in the list of corresponded vouchers.



10. To remove the corresponding relationships for a voucher, select the voucher in the left pane, click **Remove ledger bond**, and then click **Refresh data**.
    

    > [!NOTE]
    > After refreshing the data, the voucher for which correspondence has been removed will appear in the list of non-corresponded vouchers.

