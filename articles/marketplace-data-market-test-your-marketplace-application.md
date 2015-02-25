<properties 
   pageTitle="Test Your Marketplace Application" 
   description="How to Test Your Marketplace Application" 
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
#  Test Your Marketplace Application 

 -----------
This topic covers how to access and use the Windows Azure Marketplace (WAM) dedicated page where registered developers can test their web applications using a test Azure Marketplace account. 

 -----------

### Test with the Developer Playground Page

1. Navigate your browser to the [Marketplace home page](https://datamarket.azure.com/register?redirect=%2F).

2. If you do not have an account with the Windows Azure Marketplace (WAM) create one. See for instructions.

3. Register your application on the Developer Applications page. You need to provide Client Id, Application Name, Application Description and Redirect Url (your Authorization Endpoint address). <br>
See the topic [Register your Marketplace Application](./marketplace-data-market-register-your-marketplace-application.md) for how to register your application.

4. If your application uses Marketplace data, ensure that you are subscribed to the required data offers.

5. Navigate to the [Developer Playground Page](https://datamarket.azure.com/register?redirect=%2Fdeveloper%2Fplayground).

6. Enter your Client Id.

7. Click **Purchase** to simulate a user subscribing to your application. After you complete the purchase process you should be redirected to your application. Sign in and ensure that you have access to the Marketplace resources.

8. Click **Unsubscribe** to simulate a user canceling their subscription to your application. Once you see an alert stating that the subscription is successfully canceled, verify that your application has correctly handled the cancelation by deactivating or removing subscription information from your system.


##See Also
###Concepts
Develop a Marketplace Application <br> 
Query Marketplace Datasets from your App<br> 
Implement OAuth in your Marketplace App<br> 
Deploy your Marketplace Application

