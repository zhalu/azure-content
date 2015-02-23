   
<properties 
   pageTitle="Download from the Marketplace to PowerPivot" 
   description="How to download from the Marketplace to PowerPivot" 
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

 
#  Download from the Marketplace to PowerPivot 

This topic covers how to download a dataset from Windows Azure Marketplace (WAM) into Microsoft Excel 2010’s PowerPivot. The article assumes that you already have a Marketplace account and subscription to the dataset you want to import.
 -----------

Microsoft Excel 2010 (and later) PowerPivot add in enables powerful data analytics and reporting. Combining Marketplace data with the power of PowerPivot’s pivot tables you can gain new insights that you can use for a competitive advantage.

There are two ways to get your dataset from the Marketplace into PowerPivot:

While using Service Explorer in the Marketplace, you can export from Service Explorer to PowerPivot. The subject of this article.


While using Excel 2010, you can import from the Marketplace into PowerPivot (if you have the installed the Excel PowerPivot add-in). See the article [Import Marketplace data into PowerPivot](./marketplace-data-market-import-marketplace-data-into-powerpivot.md).
 -----------
 
###Download data from the Marketplace into Excel PowerPivot
If PowerPivot for Microsoft Excel 2010 is not installed on your computer, go to the [PowerPivot download site](http://www.microsoft.com/en-us/server-cloud/solutions/business-intelligence/default.aspx) and follow the instructions to install PowerPivot.

####Select a dataset to analyze
1. Login to the [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/?source=datamarket) (WAM) with your Windows account (formerly known as Live ID). 

2. Navigate to **My Data | Datasets.**

3. Locate a dataset of interest. <br>
If you cannot find a dataset of interest among your subscriptions, click the Marketplace **Data** tab, then locate and subscribe to an interesting dataset.

4. Click the data set’s name.

####Query the dataset
1. On the dataset’s home page, click **Explore This Dataset**.

2. If there are any required parameters, fill them in. (Figure 1.1)

3. If there are any optional parameters, you can fill them in or leave them blank. (Figure 1.2)

4. Click **Apply**. (Figure 1.3)

![](./media/marketplace-data-market-download-from-the-marketplace-to-powerpivot/querythedataset.png)

####Download the data to PowerPivot

1. From the list of **Download Options**, select **PowerPivot 2010**. (Figure 2).
<br>![](./media/marketplace-data-market-download-from-the-marketplace-to-powerpivot/downloadoptionspp.png)

2. When prompted, click **Open**.

3. On the **Table Import Wizard** paste in your Marketplace account key. <br>
If you need to find your account key, click **Find**, then copy the account key to your clipboard and paste it into the wizard.

4. If you are on a computer that only you use, you can check the **Save my account** key checkbox.

5. Click **Next**.

6. If want to select the columns you import, click the **Preview & Filter** button and clear the checkbox for any column that you don’t want imported for analysis.

7. Click **Finish** to import your data. 

8. After the data is completed, click **Close**. 
You can analyze the data using PowerPivot. For information on using PowerPivot see the videos at the [PowerPivot download page](http://www.microsoft.com/en-us/server-cloud/solutions/business-intelligence/default.aspx), or search for “PowerPivot training” on [Bing.com](http://www.bing.com).


##See Also

###Other Resources
Learn to Use PowerPivot <br>
PivotTable reports 101
