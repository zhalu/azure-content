  
<properties 
   pageTitle="Compare Fixed and Flexible Query Types" 
   description="How to Compare Fixed and Flexible Query Types" 
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
 
#Compare Fixed and Flexible Query Types 
 -----------

DataMarket Logo The Marketplace exposes data using OData feeds. The Open Data Protocol (OData) is a Web protocol for querying and updating data that provides a way to unlock your data and free it from silos that exist in applications today. OData does this by applying and building upon Web technologies such as HTTP, Atom Publishing Protocol (AtomPub) and JSON to provide access to information from a variety of applications, services, and stores.  

OData is consistent with the way the Web works - it uses URIs for resource identification and an HTTP-based, uniform interface for interacting with those resources. OData provides the ability for a service to allow clients to dynamically build queries against feeds adding filters, sorting, and the like, or for a service to provide fixed query methods (similar to other web service endpoints) where the client must provide a specific set or subset of parameters and is returned a specific result set as determined by the content owner. The Marketplace publishes services that make use of both of these types of queries. The type of query available to a dataset is specified on the dataset’s **Details** page, as seen in the image below. 
 -----------

###Flexible Query

A flexible query dataset permits you to add optional parameter name/value filters when you query the dataset (columnName=dataValue), as well as an array of OData query options supported by the Marketplace. For more information on which query options the Marketplace supports see Supported OData Query Options [Supported OData Query Options](./marketplace-data-market-supported-odata-query-options.md).


When you develop an application that uses a flexible query dataset, use Visual Studio Add Service Reference to generate strongly typed .NET classes that you can then use to call the OData service from within your application. See [Step 2: Add the Service Reference for your Data Service](./marketplace-data-market-create-a-flexible-query-application.md) for more information.

###Fixed Query

A fixed query dataset permits you to call predefined query methods that the content publisher makes available. A query method may have a set of required and/or optional parameters that allow you to add constrained filtering to your query. You can find a list of the required and/or optional parameters for any fixed query dataset included in the dataset’s Details page.

Visual Studio Add Service Reference does not currently support code generation for data services that supports fixed query. Any dataset that supports fixed query provides a pre-created proxy class for the dataset. The proxy class file is available on the dataset Details page after the subscription is purchased. The proxy classes use the WCF Data Service client library to create a strongly typed .NET class that can call the OData service. See [Create a Fixed Query Application](./marketplace-data-market-create-a-fixed-query-application.md)  for more information.

To determine which type of query a dataset supports, see the section **Determine the Query Type** below.

###Prerequisites
Before you proceed make sure you have:

* A valid Windows Live ID account. If you do not have a Live ID go to the [Windows Live home page](http://go.microsoft.com/fwlink/?linkid=202643) and sign up.


* A valid Marketplace account. If you do not have a Marketplace go to the topic [Create Your Marketplace Account](./marketplace-data-market-create-your-marketplace-account.md) and follow the instructions there.


* A subscription to the **Data.gov 2006-2008 Crime in the United States** dataset. If you have not subscribed to this dataset go to [Subscribe to a Data Offer](./marketplace-data-market-Subscribe-to-a-Data-Offer.md) and follow the instructions.



###Sections in this Topic

<table>
  <tr>
<td>Section </td><td>Description</td>
</tr>

<td> URI Examples</td>
<td>Examples of flexible query and fixed query URIs.</td>
</tr>

<td>Determine the Query Type</td>
<td>Steps to determine whether a dataset supports flexible or fixed queries.</td>
</tr>

</table>
 

 
 
###URI Examples

<table>
  <tr>
<td>URI</td><td>URI Description</td>
</tr>

<td> https://api.datamarket.azure.com/data.ashx/contoso.com/salesreport/GetSalesReport?region=northamerica </td>
<td>Flexible query to access the Contoso, Ltd. Sales Report data for North America.</td>
</tr>

<td>https://api.datamarket.azure.com/data.ashx/contoso.com/salesreport/GetSalesReport
 </td>
<td>Flexible query to access the Contoso, Ltd. Sales Report data. 
Since no parameters are specified, the result set is unfiltered and the query returns all Sales Reports in the system.</td>
</tr>

  <tr>
<td>https://api.datamarket.azure.com/Data.ashx/adatum.com/CensusInfo/GetCensusData </td>

<td>Fixed query with no required parameters to access the latest census data from the A. Datum, Inc. service. </br></br>

The call to GetCensusData is the data access method in the downloaded C# service class provided by the Marketplace.
</td>
</tr>

  <tr>
<td>https://api.datamarket.azure.com/Data.ashx/thephone-company.com/accountbalance/GetAccountBalance?phonenumber=5551234567</td>

<td> Fixed query with one required parameter to access a specific account balance data from The Phone Company’s Marketplace service. </br>
If the required parameter name/value pair is not supplied the query fails. </br></br>

The call to GetAccountBalance is the data access method in the downloaded C# service class provided by the Marketplace.
 </td>
</tr>
</table>
 
 
<table>
  <tr>
<td>

- Important</td>
</tr>

<td>A flexible query with no parameters returns an unfiltered result set. </br>
A fixed query with the wrong number of parameters (too few or too many) fails. 
</td>
</tr>
</table>



For more information on building URIs to query OData services see [OData URI Conventions](http://www.odata.org/developers/protocols/uri-conventions) at OData.org.

###Determine the Query Type
Some datasets permit only fixed queries, queries without parameters or with required parameter/value pairs. Other datasets permit flexible queries, queries which include optional parameter/value pairs to filter the result set. Find out what type of query your dataset requires.

1.  Click the **My Data** tab.

2.  Click the word **Use** to the right of the name of the dataset you want to use in your application.

3.  Scroll down the page to the tabs below the dataset description.

4.  Click the **Details** tab.

5.  Find the line of text below the service root URL that tells you the query type. This example is for a flexible query.

![alt text](./marketplace-data-market-compare-fixed-and-flexible-query-types/servicerooturl.jpg)

**Figure 1 – Query Type**


 -----------
##See Also

###Tasks<br />
Create a Flexible Query Application<br />
Create a Fixed Query Application

###Concepts<br />
Compare Flexible and Fixed Query Code

###Other Resources<br />
Odata.org<br />
OData URI Conventions
