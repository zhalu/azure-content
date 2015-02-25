  
<properties 
   pageTitle=" Marketplace billing and how it works " 
   description="Understanding how Marketplace bills and how it works" 
   services="cloud-services" 
   documentationCenter="" 
   authors="kevinscharpenberg" 
   manager="manager-alias" 
   editor=""/>

<tags
   ms.service="marketplace"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="data-services" 
   ms.date="02/16/2015"
   ms.author="kevsch"/>
#    Marketplace billing and how it works 
Windows Azure Marketplace (WAM) billing process explained and illustrated.
 -----------
If you are unclear as to when your credit card is charged for your Marketplace subscriptions, this article should help clarify how it works.

In this article we:

- Explain what your Marketplace Account is and how it differs from your credit card account.

- Explain what your Account Anniversary is and how it relates to when your credit card is billed.

- Explain the Subscriptions Billing Date is and how it relates to the WAM Account and your credit card charges.

We also illustrate how these three work together in a typical customer scenario.

 -----------

###Accounts and Dates

This section identifies and explains the various accounts and dates you need to be aware of when tracking your Marketplace subscriptions and billing.

####Azure Marketplace Account
Your Windows Azure Marketplace (WAM) Account is associated with your Customer ID. You can find your Customer ID under **My Account/Account Information**. Whenever you incur a charge, it is posted to your Windows Azure Marketplace (WAM) Account. On your Account Anniversary Date the balance in your Windows Azure Marketplace (WAM) Account is charged to your credit card.

####Your credit card account
Your credit card account is credit card that you associated with your Windows Azure Marketplace (WAM) Account when you subscribed to your first paid offering. Charges are made to your credit card whenever you first subscribe to a paid offering, and then on the monthly Subscription Billing Date.

####Your Account Anniversary Date
Your Account Anniversary Date is the day of the month you first subscribed to a paid offer and established a billing relationship with Microsoft. For example, if you created your Marketplace account January 1st, subscribed to a free offer on January 3rd, and subscribed to a paid offer January 5th, then the 5th of each month is your Account Anniversary Date. The current balance in your Windows Azure Marketplace (WAM) Account is charged to your credit card on the Account Anniversary Date.

Accounts created on the 29th, 30th or 31st of a month have the 1st as their Account Anniversary Date.

####Your Subscription Billing Date
Your Subscription Billing Date is the day of the month that you subscribed to a particular paid offer. If you have multiple subscriptions, it is likely that you also have multiple Subscription Billing Dates. On the Subscription Billing Date, the cost of the subscription is added to your Windows Azure Marketplace (WAM) Account balance. For example, if you subscribe to paid offer A on January 5th and paid offer B on January 9th, then you have two Subscription Billing Dates, the 5th (for offer A) and the 9th (for offer B).


###Customer Scenario

The events shown in Figure 1, Billing Timeline, are described in detail in the following table. In this scenario we walk through a typical customer’s subscriptions, billings and charges to their credit card. 


![](./media/marketplace-data-market-marketplace-billing-and-how-it-works/billingtimeline.png)

<table>
  <tr>
<td>
</td><td>Date
</td><td>Event  
</td><td>Results 
</td><td>WAM Account  
</td><td>Credit Card 
</td></tr>
<tr>
<td>1.
</td><td>5/9
</td><td>Customer creates Windows Azure Marketplace (WAM) account. Customer subscribes to a free offering but no paid offerings. 
</td><td>- The customer is given a Customer ID. 
</td><td>N/A 
</td><td>N/A 
</td></tr>
<tr>
<td>2.
</td><td>5/17
</td><td>Customer subscribes to Bing Search at $13 level.
Note, this is the first time the customer has subscribed to a paid offering.
</td><td>- Subscription amount ($13) immediately charged to the credit card. <br><br>
-The 17th of the month becomes the Account Anniversary Date.<br><br>
-The 17th of the month becomes the Bing Search Subscription Billing Date.
 
</td><td>$0.00
 
</td><td>$13.00
 
</td></tr>
<tr>
<td>3.
</td><td>5/26 
</td><td>Customer subscribes to Bing Translator at $30 level.
Since this is not the first paid subscription it has no impact upon the Account Anniversary Date.
</td><td>-Subscription amount ($30) immediately charged to the credit card. <br><br>
-The 26th of the month becomes the Bing Translator Subscription Billing Date. 
</td><td>$0.00
 
</td><td>$30.00
 
</td></tr>
<tr>
<td>4.
</td><td>6/5
</td><td>Customer cancels Bing Search subscription.
</td><td>-Bing Search subscription set to expire on 6/16 - the day before the next Bing Search Subscription Billing Date.<br><br>
-The Bing Search Subscription Billing is cancelled. 
</td><td>$0.00
 
</td><td>$0.00
 
</td></tr>
<tr>
<td>5.
</td><td>6/17 
</td><td>Account Anniversary date
</td><td>-Balance in the Marketplace Account ($0) is charged to credit card.<br> 
No charge for Bing Search since it was canceled. <br>
No charge for Bing Translator since it is paid up to 6/26 (its Subscription Billing Date). 
</td><td>$0.00
 
</td><td>$0.00
 
</td></tr>
<tr>
<td>6.
</td><td>6/26
</td><td>Bing Translator Subscription Billing Date 
</td><td>-Monthly charge for Bing Translator ($30) is added to the Marketplace Account. 
</td><td>$30.00
 
</td><td>$0.00
 
</td></tr>
<tr>
<td>7.
</td><td>7/17
</td><td>Account Anniversary date 
</td><td>-Balance in the Marketplace Account is charged to credit card.  
</td><td>$0.00
 
</td><td>$30.00
 
</td></tr>
</table>




 -----------
##See Also

###Tasks
Subscribe to a Data Offer<br>
Subscribe to an Application Offer

###Concepts
Subscribe to a Marketplace Offering<br>
Understand Subscriptions<br>
Use Auto-Refill to avoid service lapses
