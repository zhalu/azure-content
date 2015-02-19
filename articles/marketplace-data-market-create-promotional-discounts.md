
 
<properties 
   pageTitle="Create Promotional Discounts" 
   description="How to Create Promotional Discounts for Your Offerings" 
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
   ms.date="02/13/2015"
   ms.author="kevsch"/>
#   Create Promotional Discounts

 -----------
Promotion codes are important for marketing purposes. They provide a mechanism whereby you are able to motivate others to purchase your datasets through time limited discounts which enable you to be more competitive in the Windows Azure Marketplace (WAM).

This topic covers creating and redeeming promotion codes for data and services on the WAM.
 -----------


###Create a Promotion Code
From the Publishing Portal, as a publisher you can create and apply a promotion code for any of your offerings at any time.

1). Navigate your browser to [Marketplace home page](https://azure.microsoft.com/en-us/marketplace/?source=datamarket).

2) Click **Publish** to navigate to the **Publishing on Azure Marketplace** introduction page. 

3) Click the **Get Started** button to navigate to the Publishing Portal. 

4) Sign in to the publishing portal. This is a different sign in than when you sign in to the Marketplace.

After you sign in you go to the **My Offerings** page.

5) Click the **Promotions** tab. (Figure 1)

![](./media/marketplace-data-market-create-promotional-discounts/myofferings.png)

6) Click **Add Promotion.** (Figure 2)

![](./media/marketplace-data-market-create-promotional-discounts/addpromotion.png)

7) Fill in the values you want for this coupon using the **Add Promotion** dialog. The coupon code must be alphanumeric. The coupon code must be unique among all your active promotion codes.

- **Code** <br>
The unique promotional code value that you enter. Customers enter this code when they want to apply a promotion to a purchase. (Figure 3.1)

- **Description**<br>
Enter your description of the promotion. An internal description for you to distinguish among your promotions and is not shown to customers. (Figure 3.2)

- **Discount** <br>
Enter the percent discount for this coupon. A whole number between 1% and 100%. If you enter a discount of 100%, the customer is not asked to provide a credit card when they purchase. (Figure 3.3)

- **Offer**<br>
From the dropdown select the offer this promotion applies to. Only your published offers are listed in the dropdown and not your draft or approved offers. (Figure 3.4) 
Note: A promotion can apply to only one offer.

- **Variants**<br>
Select to apply this promotion to all or specific variants of your offering. (Figure 3.5) 

- **Promotion Duration**<br>
From the dropdown select the length of time to apply the promotional price to this subscription. This time is calculated beginning when the customer redeems the promotion code. (Figure 3.6)

- **Validity period**<br>
You control when customers are able to redeem a promotion code. You can select either a valid from date, a valid to date, or both. The Pacific Time zone is used when checking whether the promotion code is within the validity period. (Figure 3.67a and 3.7b)

- **Redemption limit**<br>
Set the number of times this promotion code can be redeemed, from 1 to unlimited. (Figure 3.8)

- When you finish filling in the fields, click **Ok** or **Cancel**. (Figure 3.9)

![](./media/marketplace-data-market-create-promotional-discounts/coupondialog.png)

After you click **OK**, you return to **My Promotions**. Here you can see all of your promotions, including the one you created, with their details. (Figure 4)

![](./media/marketplace-data-market-create-promotional-discounts/mypromotions.png)


###Redeem Promotion Codes
Your customers can redeem promotion codes in several ways.

- **Direct link** <br> 
From the promotions page, you can view a link to your offer detail page that includes the promotion code with the link. You can send this link in emails, use it on your website, or include it in marketing materials. Then, when a customer clicks the link, they see the promotional pricing associated with the promotion code. 


- **Enter code at checkout** <br>
Customers can also enter the promo code during the checkout process. Once they enter the promotion code during checkout, the customer sees the promotional pricing in the checkout process. 



###Managing Your Coupons
After you create one or more promotion codes, you can manage them from the **My Promotions** tab in the Publishing portal.

From this page, you can:

A) Click Add Promotion to create promotion code. (Figure 2)

B) Review each of your promotion codes with their details. (Figure 4) <br>
The table has the following columns:

- **Code** <br>
The promotion code.

- **Description**<br>
The promotion description you entered when you created the promotion code.

- **Status** <br>
Any of the following:

 - **Not Yet Started** - the promotion code is valid from date is in the future. Customers are not able to redeem the promotion code until the valid from date is reached (in the Pacific Time zone).

 - **Active** – the promotion is in its validity period and has remaining redemptions.

 - **Fully Redeemed** – the promotion code is in its validity period but has no remaining redemptions. Customers are not able to redeem the promotion code.

 - **Ended** – the promotion code valid to date is in the past. Customers are not able to redeem the promotion code.

 - **Canceled** – you canceled this promotion.

- **Offer** <br>
The offer that this promotion code applies to.

- **Validity period**<br>
One of the following:

 - **Always valid** – no valid from or valid to dates.

 - **From mm/dd/yyyy** – only has a valid from date, no ending date.

 - **Until mm/dd/yyyy**– only has a valid to date. Promotion became valid when it was created.

 - **From mm/dd/yyyy to mm/dd/yyyy** – the beginning and ending dates of the promotion’s validity period.

- **Discount** <br>
The discount percent,

- **Redemptions**<br>
The number of times this promotion code has been redeemed. 
For promotions with unlimited redemptions the number of redemptions is shown. For promotions with a limited number of redemptions both the number of redemptions and the limit are shown (24 of 100).

- **Actions**<br>
If the coupon status is Not Yet Started, Active or Fully Redeemed you can:

 - **Cancel** - cancel this promotion.

 - **View link** – a link to the detail page for the offer this promotion applies to. This link includes the promotion code so customers automatically see promotional pricing if they visit this link.
