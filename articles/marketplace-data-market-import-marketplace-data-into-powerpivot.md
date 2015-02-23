   
<properties 
   pageTitle="Import Marketplace data into PowerPivot" 
   description="How to import Marketplace data into PowerPivot" 
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
 
#   Import Marketplace data into PowerPivot 
 This topic covers how to import a Windows Azure Marketplace (WAM) dataset into Microsoft Excel 2010’s PowerPivot. The article assumes that you already have a Marketplace account and subscription to the dataset you want to import.
 -----------

Microsoft Excel 2010 (and later) PowerPivot add in enables powerful data analytics and reporting. Combining Marketplace data with the power of PowerPivot’s pivot tables you can gain new insights that you can use for a competitive advantage.

There are two ways to get your dataset from the Marketplace into PowerPivot:

- While using Service Explorer in the Marketplace, you can export from Service Explorer to PowerPivot. See the article [Download from the Marketplace to PowerPivot](marketplace-data-market-download-from-the-marketplace-to-powerpivot.md).

- While using Excel 2010, you can import from the Marketplace into PowerPivot (if you have the installed the Excel PowerPivot add-in). The subject of this article.

  -----------
 
###Import a dataset into Excel 2010 PowerPivot
If PowerPivot for Microsoft Excel 2010 is not installed on your computer, go to the [PowerPivot download site](http://www.microsoft.com/en-us/server-cloud/solutions/business-intelligence/default.aspx) and follow the instructions to install PowerPivot.

1. Launch Microsoft Excel 2010.

2. Locate and click the **PowerPivot** tab.

3. Locate and click **PowerPivot Window**.

4. In the PowerPivot window, locate and click **From Azure DataMarket**.

5. On the **Table Import Wizard**: <br>
 - Enter the dataset’s Service root URL. If you do not know the URL, 

		- Click **View available Azure DataMarket datasets**.
		- Locate and open the dataset you want to import. 
		- Scroll down to and click the **Details** tab.		
		- Locate and copy the **Service root URL** to your clipboard.
		- Return to PowerPivot **Table Import Wizard** and paste the URL in the text box. <br><br>

 - Enter your account key. <br>
	If you do not know your account key, click **Find**, then copy the account key to your clipboard, and paste it into the text box. 

6. If you are working on a computer that is not shared, you can check the **Save my account** key checkbox.

7. The **Advanced** properties should be fine as they are. If you want to check them, click the **Advanced** button. 

	**Advanced Properties** Click **OK** when finished with **Advanced Propereties**.

 - **Integrated Security** should be Basic.

 - **Persist Security Info** should be True

 - **User ID** should be AccountKey.

8. Click **Test Connection**. If the connection fails, confirm that you have internet access, the Service root URL and your Account Key are correct.

9. Click **Next**.

10. If you want to import the entire dataset, click **Finish**. If you want to filter the results that you import, click **Preview & Filter**. <br>
<br>
**Preview & Filter**
	- To remove any unneeded columns from the result set, clear the checkbox on the column name. <br>
 - When finished, click OK.<br><br>

11. Click **Finish** to import your data. 

12. After the data is completed, click **Close**. <br> 
You can analyze the data using PowerPivot. For information on using PowerPivot see the videos at the [PowerPivot download page](http://www.microsoft.com/en-us/server-cloud/solutions/business-intelligence/default.aspx), or search for “PowerPivot training” on [Bing.com](http://www.bing.com).


##See Also
###Other Resources
Learn to Use PowerPivot <br>
PivotTable reports 101
