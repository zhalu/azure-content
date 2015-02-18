  
<properties 
   pageTitle="Use Auto-Refill to avoid service lapses" 
   description="How to use auto-refill to avoid service lapses" 
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
#   Use Auto-Refill to avoid service lapses
-----------

The Marketplace’s Auto-refill functionality gives you the ability to ensure that you, or anyone that uses your subscription, do not reach your usage limit before the end of your subscription period, and thus avoid the resultant loss of service. If you get within 10% of your subscription use limit, Auto-refill cancels your current subscription and creates a new subscription. Auto-refill also rolls your remaining transactions into the new subscription so you don’t lose what you already paid for.

With Auto-refill, you can prevent any loss of service by allowing Windows Azure Marketplace (WAM) to automatically “refill” your usage before you reach your limit. Auto-refill is subject to the Windows Azure Marketplace (WAM) [terms and conditions agreement](http://datamarket.azure.com/terms).
 -----------

###Sections in This Topic

<table>

<tr><td>Section</td><td>Section Overview</td>
</tr>
<tr><td>Auto-refill Overview
</td><td>This section has these subsections: <br><br>

-What is Auto-refill?<br>
-How does Auto-refill Work?<br>
-How do I control how often Auto-refill occurs?<br>
-What are the restrictions to using Auto-refill?<br>
-How do I know when a subscription is Auto-refilled?</td>
</tr>
<tr><td>How do I Manage Auto-refill?
</td><td>This section has these subsections:<br><br>
-How do I Enable Auto-refill for a subscription?<br>
-How do I update my Auto-refill options?<br>
-How do I disable Auto-refill?</td>
</tr>
</table>

###Auto-refill Overview

####What is Auto-refill?
Auto-refill is the customer requested ability to ensure that you, or anyone using your subscription, do not reach your usage limit before the end of your subscription period, and thus avoid the resultant loss of service. Auto-refill does this by cancelling your current subscription and creating a new subscription before you reach your usage limit.

####How does Auto-refill Work?
You subscription gives you a certain allotment of transactions, users, characters or other discrete limits (which we refer to herein as Transactions). Once you enable Auto-refill on a particular subscription, Windows Azure Marketplace (WAM) monitors your Transaction balance for the current subscription period. If your Transaction balance reaches 10% or less of your subscription limit, and you have not used up your maximum number of Auto-refills in the past 30 days (or have chosen unlimited Auto-refills), Windows Azure Marketplace (WAM) re-subscribes you to, and charges you the then-effective subscription rate for, a new subscription, thereby giving you a new subscription period and new Transaction balance. In addition, any Transactions remaining immediately before Auto-refill occurred are carried over to your new subscription so that you don’t lose anything you already paid for.

####How do I control how often Auto-refill occurs?
You can limit how often Auto-refill occurs in any given 30-day period or allow Auto-refill to occur without limit. 

When you sign up for Auto-refill, you have the option of setting a customer limit on the maximum number of Auto-refills in a 30 day period. Or, if you prefer, you can elect unlimited Auto-refills during any given 30-day period. 

You can also change your current Auto-refill limit (or change an unlimited option) at any time. For more information on changing your Auto-refill elections, see below for **How do I update my Auto-refill options?**.

So how does Auto-refill actually work? Let’s look at two examples:

#####Example 1: Auto-refill not enabled

You subscribe to Contoso Inc.’s address verification offering. For $100, you get 1,000 address verifications in a 30-day period. This offering turns out to be more useful than you anticipated and your business uses 900 address verifications in just nine days. At that rate you will run out of address verifications in one more day, leaving you with two options: 

1. Allow your balance of address verifications to reach zero and do without the service for the rest of your subscription period, at which time your subscription automatically renews, or


2. Go to the Windows Azure Marketplace (WAM) and manually create a new Contoso subscription of 1,000 address verifications.


Because you do not receive notice when the availability of address verifications is low, you may not even know that you have reached 10% of your original balance, in which case option 1 may occur without you even knowing it.

#####Example 2: Auto-refill enabled

You subscribe to Contoso Inc.’s address verification offering. For $100, you get 1,000 address verifications in a 30-day period. This offering turns out to be more useful than you anticipated and your business uses 900 address verifications in just nine days (Day 9). At this rate, you will run out of address verifications in one more day (Day 10). 

However, you enabled Auto-refill on the Contoso offering with a limit of two Auto-refills per 30-days. Thus, Windows Azure Marketplace (WAM) monitors your remaining address verifications so that you don’t have to. Because your balance reached 100 address verifications (10% of the original balance) on Day 10, Windows Azure Marketplace (WAM) creates a new Contoso subscription with a new subscription period (beginning on Day 10), giving you a new balance of 1,000 address verifications, plus the 100 remaining address verifications from your prior subscription, for a total balance of 1,100 address verifications.

If your balance reaches 100 address verifications on Day 20, Auto-Refill looks back 30 days to determine how many Auto-refills occurred. Because there has only been one Auto-refill in the last 30 days, Auto-refill again creates a new subscription with a new subscription period (starting on Day 20) and a new balance of 1,100 address verifications.

Say that user consumption spikes and your balance drops to 100 address verifications in just five days (Day 25). Windows Azure Marketplace (WAM) again looks back 30 days to determine how many Auto-refills occurred. This time, it detects that there have been two Auto-refills in the past 30 days (on Day 10 and Day 20). Because you set your limit to 2 Auto-refills, Windows Azure Marketplace (WAM) does not allow Auto-refill to create a new subscription. In this scenario, your balance continues to decrease until the subscription renews at the end of the then-current subscription period (which would be Day 50 for a 30-day subscription) or you manually upgrade or re-subscribe to your subscription. You can avoid this scenario in the future if you increase your Auto-refill limit to be resilient to unexpected spikes in usage, or you can choose unlimited Auto-refills.

####What are the restrictions to using Auto-refill?
Please note that Auto-refill is only available for paid subscriptions that are subject to a Transaction or character usage limit. Auto-refill is not available during:

- “Unlimited” subscriptions that are not subject to any Transaction/ Character limit (for example, $500 for unlimited Transactions in a subscription period).

- Promotional or trial subscriptions, including subscriptions that have been initiated using a coupon or other promotional code.

####How do I know when a subscription is Auto-refilled?
When Auto-refill occurs, you receive an e-mail notice that your current subscription has been canceled and that you have been charged for your new subscription.

You do not receive e-mail notification for any of the following:

- When you enable Auto-refill from your My Accounts page.

- When you make changes to your maximum Auto-refill election.

- When you disable Auto-refill.

- If there are problems with any of your payment methods when Auto-refill attempts to charge you for a new subscription.

- When Auto-refill attempts to create a new subscription but you have reached your maximum Auto-refill limit.


###How do I Manage Auto-refill?
Auto-refill may be managed from the My Data page after you subscribe to an offering.

####How do I Enable Auto-refill for a subscription?
Auto-refill is implemented from the **My Data** page after you subscribe to an offering.

1. Navigate to Windows Azure Marketplace (WAM) [home page](https://datamarket.azure.com/).

2. Click the **My Account** tab.

3. Click **My Data** in the left column.

4. Locate the offering where you want to enable Auto-refill.

5. Click **Enable Auto-refill**. (Figure 1.2) <br>
Subscriptions where Auto-refill is not enabled always show zero refills available. (Figure 1.1) <br>![alt text](./media/marketplace-data-market-use-auto-refill-to-avoid-service-lapses/enableautorefill.png)
6. A new window opens from which you can enable Auto-refill. (Figure 2)

7. If you want to limit the number of refills in a 30 day period, select **Limited**: then enter the maximum number of refills in any 30 day period. 
If you do not want to limit the number of refills in a 30 day period, select **Unlimited**. (Figure 2.1)

8. Select the check box confirming your choice. (Figure 2.2)

9. To enable Auto-refill with these limits, click **Submit**. 
<br>To undo these changes, click **Cancel**. (Figure 2.3)
<br><br>You then return to your **My Account** page, where your subscription shows the number of Auto-refills remaining since the last Auto-refill occurred and a link to **Edit Auto-refill**, indicating that Auto-refill is enabled. (Figure 3.1). 

![alt text](./media/marketplace-data-market-use-auto-refill-to-avoid-service-lapses/enableautorefilldialog.png)


###How do I update my Auto-refill options?

1. Navigate to Windows Azure Marketplace (WAM) [home page](https://datamarket.azure.com/).

2. Click the **My Account** tab.

3. Click **My Data** in the left column.

4. Locate the offering where you want to edit your Auto-refill parameters.

5. Click **Edit Auto-refill**. (Figure 3.2) 
<br>![alt text](./media/marketplace-data-market-use-auto-refill-to-avoid-service-lapses/editautorefill.png)
6. In the **Windows Azure Marketplace (WAM) “Auto-Refill”** window (Figure 2), make the changes you want.

7. Select the **By checking this box,…** checkbox.

8. To update your auto-refill parameter, click **Submit**. 
<br>To cancel the changes and return to the **My Account** page, click **Cancel**.


###How do I disable Auto-refill?
To disable Auto-refill on a subscription:

1. Navigate your browser to the Windows Azure Marketplace (WAM) [home page](https://datamarket.azure.com/).

2. Click the **My Account** tab.

3. Click **My Data** in the left column.

4. Locate the offering for which you want to disable Auto-refill.

5. Click **Edit Auto-refill**.

6. Click the **Disable Auto-refill** radio button. (Figure 5.1)

7. Select the **By checking this box,…** checkbox.

8. To disable Auto-refill, click **Submit**. <br>To cancel the changes and keep Auto-refill as it was, and return to the **My Account** page, click **Cancel**. <br>
![alt text](./media/marketplace-data-market-use-auto-refill-to-avoid-service-lapses/cancelautorefill.png)
 -----------
##See Also

###Tasks
Subscribe to a Data Offer

###Concepts
Understand Subscriptions
