    
<properties 
   pageTitle="Import Marketplace data into Excel" 
   description="How to Import marketplace data into excel" 
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

#  Import Marketplace data into Excel 
 -----------
If you have an Marketplace account and the Excel Marketplace add-in, you can import data directly into your Excel worksheet. Once you have the data in your worksheet you can create graphs, do analysis on the data, and any other Excel action you desire.

 -----------
###Prerequisites
Before you proceed, you must have:


- A valid Windows Live ID or OrgID. <br>
If you need a Live ID go to the [Windows Live home page](http://go.microsoft.com/fwlink/?linkid=202643) and sign-up for a Live ID.


- A valid Marketplace account. If you do not have a Marketplace account, go to [Create Your Marketplace Account](./marketplace-data-market-create-your-marketplace-account.md) and follow the instructions there.


- A subscription to a dataset of interest. If you have not subscribed to a dataset, go to [Subscribe to a Data Offer](./Marketplace-data-market-subscribe-to-a-data-offer.md) and follow the instructions there.

- The Excel Marketplace add-in installed. If you have not downloaded and installed the add-in go to the [Azure Marketplace Add-In for Excel](https://datamarket.azure.com/addin) site, download, and install the add-in.


###Sections in This Topic

<table>

<tr><td>Section</td><td>Description</td>
</tr>
  <tr><td>Import Data into Excel
</td><td>Follow these steps to import a Marketplace dataset into Excel.</td>
</tr>
<tr><td>Filter the Results
</td><td>Follow these steps to import a filtered result set.
</td>
</tr>
<tr><td>Sort the Results
</td><td>Follow these steps to import a sorted result set. <br>
Flexible query datasets only.
</td>
</tr>
<tr><td>Limit the Results
</td><td>Follow these steps to import a limited number of records in the result set.
</td>
</tr>
<tr><td>Specify the Result Fields
</td><td>Follow these steps to specify the exact fields that are returned in the result set.
</td>
</tr>
</table>

###Import Data into Excel

1) Start Microsoft Excel 2010.

2) Click the **Data** tag.

3) Click the Marketplace add-in icon. (Figure 1)
<br>![alt text](./media/marketplace-data-market-import-marketplace-data-into-excel/importdata.png) <br> **Figure 1 – Excel Marketplace Add-in**

4) Select the **Public DataMarket** (default) radio button. (Figure 2.1)

5) If you are on a computer that is used by others, clear the **Remember Me** checkbox. (Figure 2.2)

6) Click **Sign in or Create account**. (Figure 2.3) <br> ![alt text](./media/marketplace-data-market-import-marketplace-data-into-excel/signintoazure.png)<br>
7) When prompted whether or not to allow Excel to access your Marketplace account, click **Allow Access**.

8) After the list of datasets you’re subscribed to appears (Figure 3) you can <br> 
 - Refresh the list – click the refresh icon. (Figure 3.1)
<br>
 - Browse and subscribe to additional datasets – click the shopping care icon. (Figure 3.2) <br>
 - Import a specific dataset – click **Import data**… for the dataset you want to import. (Figure 3.3) 
<br>
![alt text](./media/marketplace-data-market-import-marketplace-data-into-excel/selectthedataset.png)

9) If your dataset is a flexible query dataset, you can filter, sort, limit the number of records, and specify the fields the query should return. If you want to filter, sort, limit the number of returned rows, or specify the fields that are returned, follow the appropriate steps below before you click **Import Data**.
###Filter the Results <br>
-  Click the **Filter results** tab. <br>
-  Click **Add filter**. <br>
-  From the first dropdown, select the field you want to filter on. (Figure 4.1) <br>
-  From the second dropdown, select the relational operation you want to use for this filter. (Figure 4.2)<br>
-  In the text box, type in the value you want to use for this filter. (Figure 4.3) <br>
![alt text](./media/marketplace-data-market-import-marketplace-data-into-excel/filteryourresult.png) <br>Repeat steps b through e for each additional filter you want to apply to your query. 
<br><br>If your dataset is a fixed query dataset, there can be required and optional filters. Click the Filter results tab to see if there are any required or optional filters. If there are required filters, fill in legitimate values before you continue. (Figure 5.1) Optional filters can be filled in or ignored. (Figure 5.2) <br>
<br>![alt text](./media/marketplace-data-market-import-marketplace-data-into-excel/optionalfilters.png) <br>

###Sort the Results
-  Click the Sort results tab.<br>
-  Click the Add sort order button.<br>
-  In the first dropdown, select the field you want to sort on. (Figure 6.1) <br>
-  In the second dropdown, select whether you want to sort in Ascending or Descending order. (Figure 6.2)

![alt text](./media/marketplace-data-market-import-marketplace-data-into-excel/sorttheresults.png)

Repeat steps b through d for each additional field you want to sort on. The precedence of the field in the sort is the order they are listed. Figure 4 shows State is the primary sort field and Year the secondary sort field. The result set is then sorted by state and within each state subset by year. See Figure 7 for the result set.

###Limit the results
-  Click the Limit number of results tab. <br>
-  If you want to change the maximum number of records returned, the default is 50, check the Limit the number of items returned to: check box (Figure 7.1). <br>
-  Either type in or use the up/down arrows to set the maximum number of returned records (Figure 7.2).

		*Note
		Marketplace does not return over 100 records in a single query.

![alt text](./media/marketplace-data-market-import-marketplace-data-into-excel/limitrecords.png)


####Specify the Result Fields
- Click the Specify returned fields tab.
- Select the check box for each field you want the query to return. (Figure 8)

![alt text](./media/marketplace-data-market-import-marketplace-data-into-excel/specifyfields.png)<br>

If your dataset is a fixed query dataset, it can have required parameters. Click the Filter results tab to see and fill in any required parameters.

10) Click the Import Data button.

![alt text](./media/marketplace-data-market-import-marketplace-data-into-excel/dataimported.png)


##See Also
###Export to Excel PowerPivot or Tableau
###Tasks
Compare Fixed and Flexible Query Types <br>
Create Your Marketplace Account<br>
Manage Your Marketplace Account<br>
Subscribe to a Data Offer<br>
Explore a Dataset with Service Explorer

###Other Resources
Watch the video










