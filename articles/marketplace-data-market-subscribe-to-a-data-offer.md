  
<properties 
   pageTitle="Subscribe to a Data Offer" 
   description="How to subscribe to a data offer" 
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
#   Subscribe to a Data Offer 
 -----------

This topic walks you through how to discover and subscribe to an Marketplace premium or trusted public data offer.

 -----------
###Prerequisites
Before you proceed, make sure that you have:

- A valid Windows Live ID or OrgID. 
If you need a Live ID go to the [Windows Live home page](http://go.microsoft.com/fwlink/?linkid=202643) and sign-up for a Live ID.


- A valid Marketplace account. If you do not have a WAM account, go to [Create Your Marketplace Account](./marketplace-data-market-create-your-marketplace-account.md) and follow the instructions there.


###Sections in this Document

<table>
<tr><td>Find a Dataset of Interest 
</td><td>Browse available datasets, select a dataset that looks interesting.</td>
</tr><tr><td>Pre-Examine the Dataset
</td><td>Look at a dataset from various perspectives before you decide if you want to subscribe.
</td>
</tr><tr><td>Subscribe to the Dataset
</td><td>Subscribe to a dataset of interest.
</td>
</tr><tr><td>Additional Resources
</td><td>Use any of these resources to consume data from your dataset.
<td>
</tr>
</table>

###Find a Dataset of Interest 
If you are not signed in to the marketplace navigate your browser to the [Marketplace](http://go.microsoft.com/fwlink/?LinkId=188981) home page and on the top ribbon click **Sign in**.

To find a dataset that looks like it might be what you need:

1. Click the **Data** tab.

2. If you know what publisher or category you're interested in, you can optionally click a category or publisher to browse a subset of available offers.

3. Browse through the dataset offerings. Read the descriptions until you find a dataset of interest.  <br>
If the publisher provides sample data the phrase **View sample data** is to the right of the offering (Figure 1.1). Click this to view a sample of the data available through this offering. (Figure 1) Click **Hide sample data** (Figure 1.1) to hide the data once you examine it. <br> ![alt text](./media/marketplace-data-market-subscribe-to-a-data-offer/viewdata.png)

4. Click the name of the dataset.

###Pre-Examine the Dataset

Use the tabs on the dataset preview page to get a fuller picture of the dataset before you subscribe.

<table>
<tr><td>Tab Name  
</td><td>Tab Description </td>
</tr>
<tr><td>View Sample Data
[Optional]
 
</td><td>Use a predefined query to preview a sample of the dataset. <br>
If the publisher has enabled sample data for multiple datasets, you can choose which dataset to preview.<br><br>

-On the Browse page, click View Sample Data to the right of the offer name.<br><br>

a) Click View Sample Data to see a sample of the offering. <br>
b) Click Hide Sample Data to hide the sample data. <br><br>


This tab is present only if the data publisher enabled the View Sample Data functionality.
</td>
</tr>
<tr><td>Interactive
[Optional]
 
</td><td>If the data is conducive to and publisher permits, this tab is available and you can interact with the dataset in real time.
</td>
</tr>
<tr><td>Sample Images
[Optional]
 
</td><td>Graphical representation of dataset data.
</td>
</tr>
<tr><td>Details
 
</td><td> *See figure 2 below<br>
-Service root URL. (Figure 2.1) <br>
-Whether this dataset supports flexible or fixed queries. (Figure 2.2)<br>
-Names of available data series. (Figure 2.3) <br>
-Input fields by name and data type with example values. (Figure 2.4) <br>
-Return fields by name and data type. (Figure 2.5) <br><br>

If a dataset has more than one data series available, each series is listed separately, each with its input and return fields.
</td>
</tr>
<tr><td>Publisher Terms of Use
 
</td><td>The End-User License Agreement (EULA) which you must accept before you can subscribe to this dataset.
</td>
</tr>
</table>

![alt text](./media/marketplace-data-market-subscribe-to-a-data-offer/detailstab.png)

###Subscribe to the Dataset
Some publishers of paid datasets offer one-month trial subscriptions. A trial subscription allows you to "try out" the dataset before you commit to purchase it. If you sign up for a trial subscription, it automatically rolls over to a paid subscription if not canceled before the end of the trial period. <br>

1) In the right column of the page, find the subscription variants that are available for this dataset.


2) If there is more than one subscription variant, click **Sign up** (free variants) or **Buy** (paid variants) for the variant you want. <br><br>
For information on subscription costs and billing, see [Understand Subscriptions](./marketplace-data-market-understand-suscriptions.md).

If a publisher offers both paid and free subscriptions, the free subscriptions are generally restricted to noncommercial use. Read the **Publisher Terms Of Use** carefully so you know the limitations on the service you selected. 

If this is a paid or trial subscription, you are taken to the **Purchase** page to complete the purchase. Fill in the required information on the page (first time only, after that you only reselect your credit card).

####Purchase Page: Billing Information (first time only)
- If you want to continue with this purchase click **Next**, otherwise click **Cancel**.

- Wait while your request is processed. This process might take several minutes.

- Carefully read the terms of use.

- If you agree to the terms of use, check the **I have read and agree to the terms of use** check box.

- After your request has been approved click the **Purchase** button to finish the purchase or **Cancel** to cancel the purchase.

If you have a discount code, click the **Have a Promotion Code**? Link (Figure 3.1), enter the promotion code in the dialog (Figure 3.2) and click **OK**. (Figure 3.3) <br>
For more information on promotion codes see the **Promotion Codes** section in this topic.

![alt text](./media/marketplace-data-market-subscribe-to-a-data-offer/promotioncode.png)

3) On the **Thank You** page, click **Print** if you want a hard copy of the subscription receipt for your records.

You are now subscribed to this dataset and can use it in accordance with the **Publisher Terms Of Use**. When you click the **My Account** tab then click My Data, this dataset appears as one you are subscribed to.

####Promotion Codes
A publisher might, at times, elect to promote an offering by with a limited time discounted price on an offering. If you received a promotional discount code, you can apply that discount code in any of three ways.

- On the Purchase page, enter the discount code via the **Promotional Discount** link.

- On the Details page, add a parameter to the query URL. 

		Example:
		http://datamarket.azure.com/dataset/5ba839f1-12ce-4cce-bf57-a49d98d29a44?x_promocode=<myPromoCode>

- On the Checkout page, add a parameter to the query URL. 

		Example: 
		*https://datamarket.azure.com/checkout/6c6f1096-e8a6-4a82-9916-2e91e8db01e6?x_promocode=<myPromoCode>*


Once applied, the discount code is saved as a cookie on your computer. Thus, to receive the discounted price you must have cookies enabled on your computer.

###Additional Resources
After you subscribe to a dataset, there are additional resources available to you. Some of these resources are listed in the center pane of the dataset Thank You page and the Details page. To access the Details page, click the **My Account** tab then **My Data**. Find the dataset then click **Use** to the right of the dataset name.


<table>
<tr><td>Explore this Dataset
</td><td>Use Service Explorer to interactively explore and analyze data from this dataset.
</td>
</tr>
<tr><td>Microsoft PowerPivot For Excel 2010

</td><td>Use PowerPivot for Excel to create compelling self-service BI.
</td>
</tr>
<tr><td>Tableau Software

</td><td>Use Tableau software to create best-in-house data visualizations and web dashboards.
</td>
</tr>
<tr><td>Learn How To Use This Data in Visual Studio

</td><td>riUse Visual Studio and its strongly typed data access with complete IntelliSense to ease development.
ght</td>
</tr>
</table>
 -----------
##See Also
Export to Excel PowerPivot or Tableau <br><br>
###Tasks
Create Your Marketplace Account <br>
Manage Your Marketplace Account<br>
Explore a Dataset with Service Explorer

###Concepts
Develop a Marketplace Application<br>
Understand Subscriptions
