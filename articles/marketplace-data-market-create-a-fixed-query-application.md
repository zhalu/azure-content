  
<properties 
   pageTitle="Create a Fixed Query Application" 
   description="How to Create a Fixed Query Application" 
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
#  Create a Fixed Query Application 

 
 -----------

Use downloadable Service Classes in Visual Studio to programmatically consume Marketplace datasets that the data publisher has specified as fixed query datasets.
 
 -----------


###Prerequisites
Before you proceed make sure you have:

* A valid Windows Live ID account. If you do not have a Live ID go to the [Windows Live home page](http://go.microsoft.com/fwlink/?linkid=202643) and sign up.


* A valid Marketplace account. If you do not have a Marketplace go to the topic [Create Your Marketplace Account](./marketplace-data-market-Create-your-Marketplace-Account.md) and follow the instructions there.


* A subscription to the Marketplace flexible query dataset you want to use in your application. If you have not subscribed to a fixed query dataset go to [Subscribe to a Data Offer](./marketplace-data-market-Subscribe-to-a-Data-Offer.md) and follow the instructions there.


###Sections in this Topic
 
<table>

<td>Section</td><td>Description</td>
</tr>
  <tr>
<td>Step 1: Create Your Project in Visual Studio</td><td>Steps to take in Visual Studio to start a new console project for the Marketplace.</td>
</tr>
  <tr>
<td>Step 2: Add the Service Reference for your Data Service</td><td>Steps you need to take to add a Service Reference to consume Marketplace data.</td>
</tr>
  <tr>
<td>Step 3: Add System.Data.Services.Client
</td><td>Add a reference to System.Data.Services.Client to your project.
.</td>
</tr>
  <tr>
<td>Step 4: Consume Data with Managed Code</td><td>Code you write to consume a Marketplace fixed query dataset.</td>
</tr>
  <tr>
<td>Completed Code</td>
<td>Code for the completed program.
</td>
</tr>
  <tr>
<td>Metadata</td><td>Example XML metadata for this flexible query dataset.</td>
</tr>  <tr>

</table>

###Step 1: Create Your Project in Visual Studio

####Start Visual Studio
1. Find **Visual Studio** in your **Start Menu**. <br><br>
2. Right click **Visual Studio**.<br><br>
3. In the dropdown menu click **Run as administrator**.<br><br>
4. When asked if you want to allow this program (devenv.exe) to make changes to your computer click **Yes**.

####Create a New Project
1.  On the Visual Studio Start Page select **New Project…**<br><br>
2.  Select **Visual C#** and **Console Application** (**Visual Basic** and **Console Application** if you prefer Visual Basic) in the New Project dialog. <br><br>
3.  From the left drop-down list at the top of the **New Project** dialog box, select **.NET Framework 4**. 
<br><br> 
Visual Studio 2010 defaults to **.NET Framework 4**. If you use an earlier version of Visual Studio and do not have .NET Framework 4 installed go to the [.NET Framework 4 download page](http://www.microsoft.com/en-us/download/details.aspx?id=17851) to download and install it. <br><br>
4. Give your project a meaningful name. For example, for this project you could name it **CensusDemographics**.

5. Click **OK**.

###Step 2: Add the Service Class for your Data Service

After starting Visual Studio as an administrator and creating a new console application (Step 1) download and add the service reference for the data service you want to consume.

####Download the Service Class
1. Go to the Marketplace.

2. Click the **My Data** tab.

3. Find the **Alteryx – Census Demographic Data** data service. 

4. Click **Use** to the right of the Service name. <br>
	This takes you to the “Details Page.”

5. Click **.NET C# Class Library** on the right side of the page.



![alt text](./marketplace-data-market-create-a-fixed-query-application/csharpcclasslibrary.jpg)

	**Figure 1 – Download the .NET C# Class Library**	

6. Click the **Save** button on the dialog box.

7. Save the **CensusDemographicDataContainer.cs** file to your project folder.

		Tip
		If you intend to use more than one data service from the same data publisher in this project, 
		make sure each class library file has a unique and meaningful name so you don’t overwrite one service class file with another.

####Add the Service Class to Your Project

1. Return to your Visual Studio project.

2. In Solution Explorer right click the project name (which is in bold).

3. Select **Add Existing Item** from the dropdown menu.

4. Select the service proxy class you just downloaded to your project folder.

5. Click **Add**. 

6. Double click the file name in **Solution Explorer**. 

7. Find the namespace for this service class. <br>
For example, *namespace Alteryx*.

8. Add the following code at the top of any code files that make use of Marketplace datasets.

 
</table> 
**C#**
	
	using System.Net;  // needed for authentication
	using Alteryx;     // the namespace of your service class


**Visual Basic**

	Imports System.Net   ' needed for authentication
	Imports Alteryx      ' the namespace of your service class

If multiple datasets are being used in a single application, repeat steps 2 through 8 for each data service. 

###Step 3: Add System.Data.Services.Client
In addition to the service class for the dataset you need to add a reference to System.Data.Services.Client to your project.

####Add System.Data.Services.Client to the Application

1. Open **Solution Explorer**.

2. Right-click **References**.

3. From the drop-down menu select **Add Reference**.

4. From the dialog click the **.NET** tab.

5. Locate *System.Data.Services.Client*.

6. Click OK.

###Step 4: Consume Data with Managed Code
After the service classes have been properly imported and a reference to System.Data.Services.Client has been added, you can invoke the methods of the container class to query the dataset. 

The following code defines a simple Console Application that uses the **CensusDemographicDataContainer.cs** dataset. It is important to note which particular dataset is being used, as the service classes have pre-configured the methods that expose the service parameters as strongly-typed method parameters in the application code, and the symbolic names of the service class objects are unique to the dataset.

####Create a class to do the work

**A.** Create a public class, *CensusDemographicData*, within your project namespace.

**B.** Create two private variables within your class.<br>

- A Uri to the service. <br>
	*private Uri serviceUri;*
- A service container for your authentication credentials. <br>
	*private CensusDemographicDataContainer context;*

**C#**

	class CensusDemographicData
	{
    	private Uri serviceUri;
    	private CensusDemographicDataContainer context;
	}



**Visual Basic**

	Class CensusDemographicData
    	Private serviceUri As Uri
    	Private context As CensusDemogrphicDataContainer
	End Class

<br>

**C.** Add a constructor for the CensusDemographicData class. <br> 
The constructor initializes both private variables and the user credentials. 
 <br>
The ROOT_SERVICE_URL is the Service Root URL. (See [Get the Service Root URL](marketplace-data-market-Create-a-Flexible-Query-Application.md) for how to find the Service Root URL.)<br>
The *context* is the service container which is used for user credentials. <br>
The *IgnoreMissingProperties* property is set to true to make the client robust to properties being added to the type on the server. (See [MSDN documentation](http://msdn.microsoft.com/en-us/library/system.data.services.client.dataservicecontext.ignoremissingproperties.aspx) for additional information.)<br>
The *USER_ID* is your Live ID.<br>
The *SECURE_ACCOUNT_KEY* is the Marketplace account key you’re using for this application. (See [Manage Your Marketplace Account](./marketplace-data-market-Manage-Your-Marketplace-Account.md).)

**C#**

	class CensusDemographicData
	{
    	private Uri serviceUri;
    	private CensusDemographicDataContainer context;

    	// class constructor
    	public CensusDemographicData()
    	{
        	serviceUri = new Uri(ROOT_SERVICE_URL);
        	context = new CensusDemographicDataContainer(serviceUri);
        	context.IgnoreMissingProperties = true;
        	context.Credentials = new NetworkCredential(USER_ID, 
                                                    SECURE_ACCOUNT_KEY);
    	}
	}



**Visual Basic**

	Class CensusDemographicData
    	Private serviceUri As Uri
    	Private context As CensusDemogrphicDataContainer

    	' class constructor
    	Sub New()
        	serviceUri = new Uri(ROOT_SERVICE_URL)
        	context = new CensusDemographicDataContainer(serviceUri)
        	context.IgnoreMissingProperties = True
        	context.Credential = new NetworkCredential(USER_ID, 
                                                   SECURE_ACCOUNT_KEY)
    	End Sub
	End Class
<br>
**D.** Create a public method (Sub) in the CensusDemographicData class that returns a generic list.  <br>
For our program the generic type is *CensusDemographicDataEntity*. 
This method queries the data service and if successful returns the result set as an *IList<>* (*IList* (*Of* )). If the query fails for any reason the method returns a *null (Nothing)*.

**C#**

	class CensusDemographicData
	{
    	private Uri serviceUri;
    	private CensusDemographicDataContainer context;
    	// constructor
    	public CensusDemographicData()
    	{
        	serviceUri = new Uri(ROOT_SERVICE_URL);
        	context = new CensusDemographicDataContainer(serviceUri);
        	context.IgnoreMissingProperties = true;
        	context.Credentials = new NetworkCredential(USER_ID, 
                                                    SECURE_ACCOUNT_KEY);
    	}

    	// the method that queries the service and returns the IList<> of demographic data
    	public IList<CensusDemographicDataEntity> GetCensusDemographicData()
    	{
        	IEnumerable<CensusDemographicDataEntity> query;

        	query = context.GetCensusDemographicData(LONGITUDE,LATITUDE,RADIUS,null);
        	// The function GetCensusDemographicData is the fixed web function that you can use to request data from this service
        	//    It is found in the service class you downloaded and added to your project.
        	// Note: either of the last two parameters may be null but both cannot be null

        	try
        	{
            return query.ToList();
        	}
        	catch (Exception ex)
        	{
            Console.WriteLine("Census ERROR {0}",ex.Message);
            return null;
        	}		
    	}
	}
**Visual Basic**

	Class CensusDemographicData
    	Private serviceUri As Uri
    	Private context As CensusDemogrphicDataContainer

    	Sub New()
        	serviceUri = new Uri(ROOT_SERVICE_URL)
        	context = new CensusDemographicDataContainer(serviceUri)
        	context.IgnoreMissingProperties = True
        	context.Credential = new NetworkCredential(USER_ID, 
                                                   SECURE_ACCOUNT_KEY)
    	End Sub

    	' – the function that queries the service and return the IList of demographic data
    	Public Function GetCensusDemographicData As IList (Of CensusDemographicDataEntity)
       		Dim query As IEnumerable (Of CensusDemographicDataEntity)
        	query = context.GetCensusDemographicData(LONGITUDE,LATITUDE,RADIUS,null);
        	' The function GetCensusDemographicData is the fixed web function that you use to request data from this service
        	'   It is found in the service class you downloaded and added to your project.
        	' Note: either of the last two parameters may be null but both cannot be null

        	Try
            	Return query.ToList()
        	Catch ex As Exception
            	Console.WriteLine("Census ERROR {0}",ex.Message)
            	Return Nothing
    	End Function
	End Class

###Write Main()
1. Write your *Main*() method (*Sub Main*()) with two private variables. <br> 
A generic *IList* that receives the data list from your method. <br>
A variable to instantiate your class.


**C#**

	static void Main(string[] args)
	{
    	IList<CensusDemographicDataEntity> demographicsList;
    	CensusDemographicData dataClass; 
	}



**Visual Basic**

	Sub Main()
    	Dim demographicsList As IList (Of CensusDemgraphicDataEntity)
    	Dim dataClass As CensusDemographicData
	End Sub
<br>
2. Add the code to main that exercises your class and its method. 


- Create an instance of the CensusDemographicdata class.

- Call the public GetCensusDemographicData method.

- If the method returns a list loop through the list and print out the contents.

**C#**

	static void Main(string[] args)
	{
    	IList<CensusDemographicDataEntity> demographicList;
    	CensusDemographicData dataClass; 

    	dataClass = new CensusDemographicData();
   		demographicsList = dataClass.GetCensusDemographicData();

    	if (demographicsList != null)
    	{
        	Console.WriteLine("Demographic Data");
        	Console.WriteLine("0,-15} {1,10} {2,6} {3,4}",  "Name", 
                                                       		"Population", 
                                                       	 	"Female", 
                                                        	"Male");
        foreach (CensusDemographicDataEntity entity in demographicList)
            	Console.WriteLine("{0,-15} {1,10} {2,6} {3,4}", entity.NAME,
                                                            	entity.POP00,
                                                            	entity.SEX00FEM,
                                                            	entity.SEX00MAL);
            	}
            	Console.Write("Tap any key to end. ");
            	Console.ReadKey();
    	}
	}
**Visual Basic**

	Sub Main()
    	Dim demographicsList As IList (Of CensusDemgraphicDataEntity)
    	Dim dataClass As CensusDemographicData

    	dataClass = New CensusDemographicData()
    	demographicList = dataClass.GetCensusDemographicData()

    	If Not demographicsList Is Nothing
        	Console.WriteLine("Demographic Data");
        	Console.WriteLine("0,-15} {1,10} {2,6} {3,4}",  "Name", 
                                                       		"Population", 
                                                       		"Female", 
                                                       		"Male")
        	For Each entity In demographicList
            	Console.WriteLine("{0,-15} {1,10} {2,6} {3,4}", entity.NAME,
                                                            	entity.POP00,
                                                            	entity.SEX00FEM,
                                                            	entity.SEX00MAL)

        	Next
    	End If
    	Console.Write("Tap any key to end. ")
    	Console.ReadKey()
	End Sub
####Completed Program Code

**C#**

	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Net;           // needed for authentication
	using System.Text;
	using Alteryx;              // service class for this data service

	namespace FixedDataQuery
	{
    	//============================================ Program class
    	class Program
    	{
        	static void Main(string[] args)
        	{
            	IList<CensusDemographicDataEntity> demographicList;
            	CensusDemographicData censusData = new CensusDemographicData();
            	demographicList = censusData.GetCensusDemographicData();

            	//============================================ CENSUS DEMOGRAPHIC DATA OUTPUT
            	// confirm data was returned from query
            	if (demographicList != null)
            	{
                	// print column headings
                	Console.WriteLine("Demographic Data");
                	Console.WriteLine("{0,-15} {1,10} {2,6} {3,4}", "Name", 
                                                                	"Population", 
                                                                	"Female", 
                                                                	"Male");
                	// print query results
                	foreach (CensusDemographicDataEntity entity in demographicList)
                    	Console.WriteLine("{0,-15} {1,10} {2,6} {3,4}", entity.NAME,
                                                                    	entity.POP00,
                                                                    	entity.SEX00FEM,
                                                                    	entity.SEX00MAL);
            	}
            	// pause until a key is struck
            	Console.Write("Tap any key to end. ");
            	Console.ReadKey();
            	Console.WriteLine();
        	}
    	}

    	//============================================ CensusDemographicData class
    	class CensusDemographicData
    	{
        	private const string USER_ID = "yourLiveId";
        	private const string SECURE_ACCOUNT_ID = "yourMarketplaceAccountKey";  // not your Live password
        	private const string ROOT_SERVICE_URL = "https://api.datamarket.azure.com/Data.ashx/Alteryx/CensusDemographicData";

        	private const double LONGITUDE = 47.394;
        	private const double LATITUDE = -122.392;
        	private const double RADIUS = 10.0; 

        	private Uri serviceUri;
        	private CensusDemographicDataContainer context;

        	// ------ constructor
        	public CensusDemographicData()
        	{
        	    serviceUri = new Uri(ROOT_SERVICE_URL);
        	    context = new CensusDemographicDataContainer(serviceUri);
            	context.IgnoreMissingProperties = true;
            	context.Credentials = new NetworkCredential(USER_ID,
                                                        SECURE_ACCOUNT_ID);
        	}

        	// ------ method that queries the dataset and returns the resultset (or null)
        	public IList<CensusDemographicDataEntity> GetCensusDemographicData()
        	{
            	IEnumerable<CensusDemographicDataEntity> query;

            	query = context.GetCensusDemographicData(LONGITUDE,LATITUDE,RADIUS,null);
            	// The function GetCensusDemographicData is the fixed web function that you can use to request data from this service
            	// Note: either of the last two parameters may be null but both cannot be null

            	try
            	{
                return query.ToList();
            	}
            	catch (Exception ex)
            	{
                Console.WriteLine("Census ERROR {0}",ex.Message);
                return null;
            	}
        	}
    	}
	}

**Visual Basic**

	Imports System;
	Imports System.Collections.Generic;
	Imports System.Linq;
	Imports System.Net;           ' needed for authentication
	Imports System.Text;
	Imports Alteryx;              ' service class for this data service


	Class Program
	    Sub Main()
	        Dim demographicList As IList (Of CensusDemgraphicDataEntity)
        	Dim dataClass As CensusDemographicData

        	dataClass = New CensusDemographicData()
        	demographicsList = dataClass.GetCensusDemographicData()

        	If Not demographicsList Is Nothing
            	Console.WriteLine("Demographic Data");
            	Console.WriteLine("0,-15} {1,10} {2,6} {3,4}",  "Name", 
                                                           		"Population", 
                                                           		"Female", 
                                                           		"Male")
            	For Each entity In demographicList
                	Console.WriteLine("{0,-15} {1,10} {2,6} {3,4}", entity.NAME,
                                                                	entity.POP00,
                                                                	entity.SEX00FEM,
                                                                	entity.SEX00MAL)

            	Next
        	End If
        	Console.Write("Tap any key to end. ")
        	Console.ReadKey()
    	End Sub
	End Class

	Class CensusDemographicData
    	Private serviceUri As Uri
    	Private context As CensusDemogrphicDataContainer

    	Sub New()
        	serviceUri = new Uri(ROOT_SERVICE_URL)
        	context = new CensusDemographicDataContainer(serviceUri)
        	context.IgnoreMissingProperties = True
        	context.Credential = new NetworkCredential(USER_ID, 
                                                   SECURE_ACCOUNT_KEY)
    	End Sub

    	' – the function that queries the service and return the IList of demographic data
    	Public Function GetCensusDemographicData As IList (Of CensusDemographicDataEntity)
        	Dim query As IEnumerable (Of CensusDemographicDataEntity)
        	query = context.GetCensusDemographicData(LONGITUDE,LATITUDE,RADIUS,null);
        	' The function GetCensusDemographicData is the fixed web function that you use to request data from this service
        	'   It is found in the service class you downloaded and added to your project.
        	' Note: either of the last two parameters may be null but both cannot be null

        	Try
            	Return query.ToList()
        	Catch ex As Exception
            	Console.WriteLine("Census ERROR {0}",ex.Message)
            	Return Nothing
    	End Function
	End Class



###Metadata

The dataset’s metadata informs intellisense as you write your code. If your IDE does not support intellisense or intellisense fails to work you can get the metadata from the service.

1. Get the dataset’s service root URI. 
See the section [Get the Service Root URL](marketplace-data-market-Create-a-Flexible-Query-Application.md) for instructions on how to get the service root URI.

2. Add /$*metadata* to the end of your service root URL. 
For example, if your service root URL is *https://datamarket.azure.com/Data.ashx/fabrikam.com/inventory* the metadata URL is *https://datamarket.azure.com/Data.ashx/fabrikam.com/inventory/$metadata*.

3. Navigate your browser to the metadata URL.

4. Parse the metadata. 
The following metadata is for the **Alteryx – Census Demographic Data** data service.


			<?xml version="1.0" encoding="utf-8" ?> 
			<edmx:Edmx Version="1.0" xmlns:edmx="http://schemas.microsoft.com/ado/2007/06/edmx" xmlns:dr="http://schemas.microsoft.com/dallas/2010/04">
   			<edmx:DataServices xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" m:DataServiceVersion="1.0">
      	<Schema xmlns="http://schemas.microsoft.com/ado/2009/08/edm" Namespace="Alteryx" Alias="Alteryx">
         <EntityContainer Name="CensusDemographicDataContainer">
            <EntitySet Name="CensusDemographicDataEntitySet" EntityType="Alteryx.CensusDemographicDataEntity" /> 
                   <FunctionImport Name="GetCensusDemographicData" EntitySet="CensusDemographicDataEntitySet" ReturnType="Collection(Alteryx.CensusDemographicDataEntity)">
               <Parameter Name="Latitude" Type="Edm.Double" Mode="In" Nullable="false" /> 
               <Parameter Name="Longitude" Type="Edm.Double" Mode="In" Nullable="false" /> 
               <Parameter Name="Radius" Type="Edm.Double" Mode="In" Nullable="true" /> 
               <Parameter Name="Minutes" Type="Edm.Double" Mode="In" Nullable="true" /> 
            </FunctionImport>
         </EntityContainer>
         <EntityType Name="CensusDemographicDataEntity">
            	<Property Name="NAME" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            	<Property Name="KEY" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="POP00" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="SEX00FEM" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XSEX00FEM" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="SEX00MAL" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XSEX00MAL" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE000004" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE000509" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE001013" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE001014" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE001417" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE001820" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE002024" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE002124" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE002529" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE003034" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE003539" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE004044" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE004549" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE005054" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE00GT55" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE005559" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE006064" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE006569" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE007074" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE007579" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE008084" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XAGE00G85" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="AGE00MED" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XEDU00GR911" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XEDU00ASSOC" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XEDU00BACH" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XEDU00GRAD" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XEDU00HSCH" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XEDU00NSCH" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XEDU00LTGR9" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XEDU00SCOLL" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XRAC00AMIND" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XRAC00ASIAN" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XRAC00BLACK" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIS00HISP" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XRAC00HAWAI" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIS00NHISP" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XRAC00OTHER" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XRAC00MULT" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XRAC00WHITE" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN00LT10" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN001015" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN001520" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN002025" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN002530" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN003035" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN003540" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN004045" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN004550" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN005060" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN006075" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN0075100" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN0010025" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN0012550" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN0015020" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XHIN00GT200" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="HIN00MED" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="INC00AVEHH" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="INC00PCI" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="HOO00MEDN" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XYMI00BF69" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XYMI007079" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XYMI008089" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XYMI009094" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XYMI009598" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="XYMI009900" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="HOU00STAB" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
            <Property Name="HOU00TURN" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" /> 
         </EntityType>
      	</Schema>
   		</edmx:DataServices>
		</edmx:Edmx>


Important information found in the metadata includes:

- The name of the fixed web function for this dataset that you call to request data and the type it returns. <br>
 *FunctionImport Name="GetCensusDemographicData" EntitySet="CensusDemographicDataEntitySet" ReturnType="Collection(Alteryx.CensusDemographicDataEntity)">*

- The order of the parameters you pass to the function as well as the name, type, mode and whether it is required or not for each parameter. <br>
*Parameter Name="Latitude" Type="Edm.Double" Mode="In" Nullable="false" /> <br>
Parameter Name="Longitude" Type="Edm.Double" Mode="In" Nullable="false" /> <br>
Parameter Name="Radius" Type="Edm.Double" Mode="In" Nullable="true" /> <br>
Parameter Name="Minutes" Type="Edm.Double" Mode="In" Nullable="true" />* <br>
Note that two of the parameters require values (*Nullable="false"*) and two where values are optional (*Nullable="true"*). 

- The name, data type, whether a null (Nothing) is a valid value, of the returned fields. <br>
*Property Name="HOU00TURN" Type="Edm.String" Nullable="true" dr:Queryable="false" dr:Returned="true" />* <br>
Note that in fixed query dataset the attribute *dr:Queryable* is always “*false*”. 

- The name of this dataset’s entity. <br> 
*EntityType Name="CensusDemographicDataEntity">*

- The container name for this dataset. <br>
*EntityContainer Name="CensusDemographicDataContainer">*


 -----------
##See Also

###Tasks
Compare Fixed and Flexible Query Types

###Concepts
Compare Flexible and Fixed Query Code
