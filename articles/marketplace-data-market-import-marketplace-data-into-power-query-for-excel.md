   
<properties 
   pageTitle="Import Marketplace data into Power Query for Excel" 
   description="How to import Marketplace data Power Query for Excel" 
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
 
#   Import Marketplace data into Power Query for Excel 
 
This topic covers how to import a Windows Azure Marketplace (WAM) dataset into Microsoft Power Query for Excel. Power Queryis a comprehensive ETL tool that you can use to merge data from multiple sources and formats so as to gain new insights and move your business to the next level. The article assumes that you already have a Marketplace account and subscription to the dataset you want to import.
 -----------

There are two prerequisites:

A Windows Azure Marketplace (WAM) account and subscription to the dataset you want to use. <br>
If you do not have a Marketplace account see the topic. <br>
If you need to subscribe to a Marketplace dataset see the topic.<br><br>


The Power Query Excel add-in installed. <br>
If you have not installed the Power Query add-in go to the Power Query download center, download and install the add-in before you continue. The Microsoft Power Query for Excel prerequisites are listed on the linked page.

 -----------

###Import a dataset into Power Query

1. Launch Microsoft Excel.

2. Locate and click the **Power Query** tab.

3. On the Power Query ribbon, locate and click **From Other Sources**.

4. On the context menu, locate and click **From Azure Marketplace**. <br>
If you are not signed in to Marketplace, sign in when prompted.

5. All your Marketplace subscriptions are listed on the left side of the screen. Click the subscription from which you want to import data. 
<br>This expands the subscription to show the dataset or datasets you have access to through the subscription.

6. Double-click the dataset you want to use.

The dataset is now loaded into Power Query. If the dataset is very large a subset of the entire dataset may be loaded.

See the [Power Query documentation](https://support.office.microsoft.com/en-us/article/Microsoft-Power-Query-for-Excel-Help-2b433a85-ddfb-420b-9cda-fe0e60b82a94?CorrelationId=1ac209c2-6388-4945-936d-d9f2dba21bde&ui=en-US&rs=en-US&ad=US) for guidance on using Power Query to transform, save, and share your insights.


##See Also
###Other Resources
Power Query documentation <br>
Power Query download page


