   
<properties 
   pageTitle="Create a Flexible Query Application" 
   description="How to Create a Flexible Query Application" 
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
# Create a Flexible Query Application 
 
 -----------

Use Service References in Visual Studio to programmatically consume Marketplace datasets that the data publisher has specified as flexible query datasets. 

	Important  
	The code in a service reference should not be modified as modification could result in improper functioning and side effects. 
	Additionally, modifications will be overwritten whenever the service reference is refreshed.  
 
 -----------


###Prerequisites
Before you proceed make sure you have:

* A valid Windows Live ID account. If you do not have a Live ID go to the [Windows Live home page](http://go.microsoft.com/fwlink/?linkid=202643) and sign up.


* A valid Marketplace account. If you do not have a Marketplace go to the topic [Create Your Marketplace Account](./marketplace-data-market-Create-your-Marketplace-Account.md) and follow the instructions there.


* A subscription to the Marketplace flexible query dataset you want to use in your application. If you have not subscribed to a flexible query dataset go to [Subscribe to a Data Offer](./marketplace-data-market-Subscribe-to-a-Data-Offer.md) and follow the instructions there.



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
<td>Step 3: Consume Data with Managed Code</td><td>Code you write to consume a Marketplace flexible query dataset.</td>
</tr>
  <tr>
<td>Completed Code</td>
<td>The complete console application in C# and VB.
</td>
</tr>
  <tr>
<td>Metadata</td><td>Example XML metadata for this flexible query dataset.</td>
</tr>  <tr>

</table>




###Step 1: Create Your Project in Visual Studio


####Run Visual Studio as Administrator
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
4. Give your project a meaningful name. For example, for this project you could name it **USCrime2006and2007**.

5. Click **OK**.

6.  Add the following code to the top of Program.cs (Program.vb) which is needed to authenticate your access to the dataset.

**C#**

	using System.Net; // needed for authentication



**Visual Basic**


	Imports System.Net ' needed for authentication 

###Step 2: Add the Service Reference for your Data Service

After starting Visual Studio as an administrator and creating a new console application (Step 1) add the service reference for the data service you want to consume.

####Get the Service Root URL
1. Go to the Marketplace home page.

2. Click the **My Data** tab.

3. Find the **2006 - 2008 Crime in the United States** data service. 

4. Click **Use** to the right of the dataset name. This takes you to the Details Page. for this dataset.

5. Scroll down the page to the tabs below **Learn How to Use this Data in Visual Studio**.

6. Click the **Details** tab.

7. Find the **Service root URL**.

![alt text](./marketplace-data-market-create-a-flexible-query-application/servicerooturl.jpg)

	**Figure 1 – Service root URL**	

8. Copy the **Service root URL** to your clipboard.

####Add the Service Reference to Your Code
1. Select **Program.cs (Program.vb)** in the Visual Studio Code Pane.

2. Add the following statement which makes your service reference accessible to your application.

<table>

<td> *Note  </td>
<tr><td>  Use the program namespace plus the service reference namespace name you created in #6 above.</td> </tr> 
 
</table> 
**C#**
	
	using USCrime2006and2007.DataGovCrimes; // using ApplicationName.ServiceReferenceName 
**Visual Basic**

	Imports USCrime2006and2007.DataGovCrimes ' Imports ApplicationName.ServiceReferenceName
 

###Step 3: Consume Data with Managed Code

####Create a class to do the work
**A.** Create a public class, *CrimeData*, within your project namespace.

**B.** Create two private variables within your class.<br>


- A Uri to the service. <br>
- A service container that stores your service credentials in the service context.


	####Find the Entity type
i. Go to the “Details Page.”  <br> 
ii. Click **Get Started with this Dataset**. <br> 
iii. Click the **Overview** tab. <br>
The entity set name and entity collection name are displayed.

**C#**

	class CrimeData
	}
		private Uri serviceURI;
     	private datagovCrimesContainer context;
	}	// end class CrimeData

**Visual Basic**

	Class CrimeData
    	Private serviceUri As Uri
    	Private context As datagovCrimesContainer
	End Class


<br>

**C.** Create a constructor for the CrimeData class. <br>
The constructor initializes both private variables and initializes user credentials. <br>
The *SERVICE_ROOT_URL* is the https link you copied to your clipboard above. (See **Get the Service Root URL**.)<br>
The *context* is the service container which is used for user credentials. <br>
The *IgnoreMissingProperties* property is set to true to make the client robust to properties being added to the type on the server. (See [MSDN documentation](http://msdn.microsoft.com/en-us/library/system.data.services.client.dataservicecontext.ignoremissingproperties.aspx) for additional information.)<br>
The *USER_ID* is your Live ID.<br>
The *SECURE_ACCOUNT_KEY* is the Marketplace account key you’re using for this application. (See [Manage Your Marketplace Account](./marketplace-data-market-Manage-Your-Marketplace-Account.md).)

**C#**

	class CrimeData
	{
    	private Uri serviceURI;
    	private datagovCrimesContainer context;

   		// constructor for the CrimeData class
    	public CrimeData()  
    	{
        	serviceURI = new Uri(SERVICE_ROOT_URL);
        	context = new datagovCrimesContainer(serviceURI);
        	context.IgnoreMissingProperties = true;
        	context.Credentials = new NetworkCredential(USER_ID,
                                                    SECURE_ACCOUNT_ID); // Your Marketplace account key
    	}  // end constructor

	}  // end class CrimeData

**Visual Basic**

	Class CrimeData
    	Private serviceUri As Uri
    	Private context As datagovCrimesContainer

    	' – constructor for the CrimeData class
    	Public Sub New()
        	serviceUri = New Uri(SERVICE_ROOT_URL)
       	 	context = New datagovCrimesContainer(serviceUri)
       		context.IgnoreMissingProperties = True
        	context.Credentials = New NetworkCredential(USER_ID,
                                                    SECURE_ACCOUNT_KEY) ' Your Marketplace account key
   		 End Sub
	End Class



<br>
**D.** Create a public method within your class that returns a generic list. For our program the generic list type is *CityCrime*. 
This method queries the service and if successful returns the result set as a list. If the query fails for any reason the method returns a *null* (*Nothing*).

**C#**

	class CrimeData
	{
    	private Uri serviceURI;
    	private datagovCrimesContainer context;

    	// constructor for the CrimeData class
    	public CrimeData()
    	{
        	serviceURI = new Uri(SERVICE_ROOT_URL);
        	context = new datagovCrimesContainer(serviceURI);
        	context.IgnoreMissingProperties = true;
        	context.Credentials = new NetworkCredential(USER_ID,
                                                    SECURE_ACCOUNT_ID);
    	}  // end constructor

    	// -- public method that returns a list of crime data
    	public IList<CityCrime> GetCrimeData()
    	{
        	IEnumerable<CityCrime> query = context.CityCrime.Where(crime => crime.City == "Newport").OrderBy(crime => crime.Year);

        	try
        	{
            	return query.ToList();
        	}
        	catch (Exception ex)
        	{
            Console.WriteLine("Error: {0}", ex.Message);
            return null;
    	    }  // end try

    	}  // end function GetCrimeData

	}  // end class CrimeData



**Visual Basic**

	Class CrimeData
    	Private serviceUri As Uri
    	Private context As datagovCrimesContainer

    	' – constructor for the CrimeData class
    	Public Sub New()
        	serviceUri = New Uri(SERVICE_ROOT_URL)
        	context = New datagovCrimesContainer(serviceUri)
        	context.IgnoreMissingProperties = True
        	context.Credentials = New NetworkCredential(USER_ID,
                                                    SECURE_ACCOUNT_KEY) ' Your Marketplace account key
   		End Sub

    	' – public function that returns a list of crime data
    	Public Function GetCrimeData() As IList(Of CityCrime)
        	Dim query As IEnumerable(Of CityCrime)
        	' – query the service
        	query = From crimes In context.CityCrime
                     Select crimes

        	Try
        	    Return query.ToList()
        	Catch ex As Exception
           		Console.WriteLine("Error: {0}", ex.Message)
            	Return Nothing
        	End Try
    	End Function
	End Class

The query can be any valid Marketplace LINQ query and may optionally include the *where (Where)* filter and/or *orderby (Order By)*. 
For more information on LINQ queries see [LINQ Query Expressions (C# Programming Guide)](https://msdn.microsoft.com/library/bb397676.aspx) [(LINQ in Visual Basic)](https://msdn.microsoft.com/library/bb385100.aspx). 

For information on LINQ query limitations within the Marketplace see [Supported OData Query Options](./marketplace-data-market-Supported-OData-Query-Options.md).

The following LINQ queries are valid within the Marketplace.


**C#**

	query = from crimes in context.CityCrime
            where crimes.City == "Newport" 
            orderby crimes.Year Ascending
            select crimes;
	//  this query could also be written as
	//  IEnumerable<CityCrime> query = context.CityCrime.Where(crime => crime.City == "Newport").OrderBy(crime => crime.Year);

**Visual Basic**

	query = From Crimes In Context.CityCrime
    	Where crimes.City = "Newport"
    	Order By (crimes.Year) Ascending
    	Select crimes
	' – this query could also be written as
	' – IEnumerable(Of CityCrime) query = context.CityCrime.Where(crime => crime.City == "Newport").OrderBy(crime => Crime.Year)

<br>
**E.** Write the code in Main() that utilizes your CrimeData class and GetCrimeData() method to consume the data and display it.


**C#**

	using System.Net;
	using USCrime2006and2007.DataGovCrimes; // using ApplicationName.ServiceReferenceName

	namespace USCrime2006and2007
	{
   		class Program
   		{
     		public static void Main(string[] args)
     		{
          		IList<CityCrime> crimeList;  // CityCrime is the entity type returned by the service
          		CrimeData crimeData = new CrimeData();

          		crimeList = crimeData.GetCrimeData();

          		if (crimeList != null)
          		{
              		Console.WriteLine("{0,4} {1,-12} {2,-15} {3,10} {4,13}","Year",
                                                                      		"City",
                                                                      		"State",
                                                                      		"Population",
                                                                      		"Violent Crime");

       			    foreach (CityCrime c in crimeList)
              		{
                  		Console.WriteLine("{0,4} {1,-12} {2,-15} {3,10} {4,13}",	c.Year, 
                                                                           			c.City, 
                                                                           			c.State, 
                                                                           			c.Population,
                                                                           			c.ViolentCrime);
					} // end foreach

          		}  // end if

          		Console.Write("Tap any key to exit. ");
          		Console.ReadKey();

      		}  // end Main
	
    	}  // end class Program

	}  // end namespace



**Visual Basic**

	Imports System.Net
	Imports USCrime2006and2007.DataGovCrimes ' Imports ApplicationName.ServiceReferenceName
	
	Module Module1

    	Sub Main()
        	Dim crimeList As IList(Of CityCrime) ' CityCrime is the entity type returned by the service
       		Dim crimeData As CrimeData = New CrimeData()

        	crimeList = CrimeData.GetCrimeData()

        	If Not crimeList Is Nothing Then
            	Console.WriteLine("{0,4} {1,-12} {2,-15} {3,10} {4,13}", "Year",
                                                                     "City",
                                                                     "State",
                                                                     "Population",
                                                                     "Violent Crime")

            	Dim crime As CityCrime
            	For Each crime In crimeList
                	Console.WriteLine("{0,4} {1,-12} {2,-15} {3,10} {4,13}", crime.Year,
                                                                      		 crime.City,
                                                                        	 crime.State,
                                                                         	 crime.Population,
                                                                         	 crime.ViolentCrime)
            	Next
        	End If

        	Console.Write("Tap any key to exit program. ")
        	Console.ReadKey()

   		End Sub

	End Module


####Completed Code

**C#**

	using System.Net;
	using USCrime2006and2007.DataGovCrimes; // using ApplicationName.ServiceReferenceName

	namespace USCrime2006and2007
	{
   			class Program
   			{
      			public static void Main(string[] args)
      			{
          			IList<CityCrime> crimeList;  // CityCrime is the entity type returned by the service
          			CrimeData crimeData = new CrimeData();

          			crimeList = crimeData.GetCrimeData();

          			if (crimeList != null)
          			{
              			Console.WriteLine("{0,4} {1,-12} {2,-15} {3,10} {4,13}","Year",
                                                                      			"City",
                                                                      			"State",
                                                                      			"Population",
                                                                      			"Violent Crime");

              			foreach (CityCrime c in crimeList)
              			{
                  			Console.WriteLine("{0,4} {1,-12} {2,-15} {3,10} {4,13}", c.Year, 
                                                                           			 c.City, 
                                                                           			 c.State, 
                                                                           			 c.Population,
                                                                           			 c.ViolentCrime);
              			} // end foreach

          			}  // end if

          			Console.Write("Tap any key to exit. ");
          			Console.ReadKey();

      			}  // end Main

    		}  // end class Program

    		class CrimeData
    		{
        		private Uri serviceUri;
        		private datagovCrimesContainer context;

        		// constructor for the CrimeData class
        		public CrimeData()
        		{
            		serviceUri = new Uri(SERVICE_ROOT_URL);
            		context = new datagovCrimesContainer(serviceUri);
            		context.IgnoreMissingProperties = true;
            		context.Credentials = new NetworkCredential USER_ID,
                                                        SECURE_ACCOUNT_KEY); // Your Marketplace account key
        		}  // end constructor
 
        		// – public function that returns a list of crime data
        		public IList<CityCrime> GetCrimeData()
        		{
            		IEnumerable<CityCrime> query = context.CityCrime.Where(crime => crime.City == "Newport").OrderBy(crime => crime.Year);
 
            		try
            		{
                		return query.ToList();
            		}
            		catch (Exception ex)
            		{
                		Console.WriteLine("Error: {0}", ex.Message);
                		return null;
            		}  // end try

        		}  // end function

    		}  // end class CrimeData

	}  // end namespace

**Visual Basic**

	Imports System.Net
	Imports USCrime2006and2007.DataGovCrimes ' Imports ApplicationName.ServiceReferenceName

	Module Module1

    	Sub Main()
        	Dim crimeList As IList(Of CityCrime) ' CityCrime is the entity type returned by the service
        	Dim crimeData As CrimeData = New CrimeData()

        	crimeList = CrimeData.GetCrimeData()

        	If Not crimeList Is Nothing Then
            	Console.WriteLine("{0,4} {1,-12} {2,-15} {3,10} {4,13}", "Year",
                                                                     	"City",
                                                                     	"State",
                                                                     	"Population",
                                                                     	"Violent Crime")

            	Dim crime As CityCrime
            	For Each crime In crimeList
                	Console.WriteLine("{0,4} {1,-12} {2,-15} {3,10} {4,13}", crime.Year,
                                                                         	crime.City,
                                                                         	crime.State,
                                                                         	crime.Population,
                                                                         	crime.ViolentCrime)
            	Next
        	End If

        	Console.Write("Tap any key to exit program. ")
        	Console.ReadKey()

    	End Sub

	End Module

	Class CrimeData
    	Private serviceUri As Uri
    	Private context As datagovCrimesContainer

    	' – constructor for the CrimeData class
    	Public Sub New()
        	serviceUri = New Uri(SERVICE_ROOT_URL)
        	context = New datagovCrimesContainer(serviceUri)
        	context.IgnoreMissingProperties = True
        	context.Credentials = New NetworkCredential(USER_ID,
                                                    SECURE_ACCOUNT_KEY) ' Your Marketplace account key
    	End Sub

    	' – public function that returns a list of crime data
    	Public Function GetCrimeData() As IList(Of CityCrime)
        	Dim query As IEnumerable(Of CityCrime)
        	' – query the service
        	query = From crimes In context.CityCrime
                     Select crimes

        	Try
            	Return query.ToList()
        	Catch ex As Exception
            	Console.WriteLine("Error: {0}", ex.Message)
            	Return Nothing
        	End Try
    	End Function
	End Class

###Metadata

The dataset’s metadata informs intellisense as you write your code. If your IDE does not support intellisense or intellisense fails to work you can get the metadata from the service.

1. Get the dataset’s service root URL. 
See the section **Get the Service Root URL** above for instructions on how to get the service root URL.

2. Add */$metadata* to the end of your service root URL. 
For example, if your service root URL is *https://api.datamarket.azure.com/Data.ashx/fabrikam.com/inventory* the metadata URL is *https://api. datamarket.azure.com/Data.ashx/fabrikam.com/inventory/$metadata.*

3. Navigate your browser to the metadata URL.

4. Parse the metadata. 
The following metadata is for the **2006 - 2008 Crime in the United States** data set ([https://api.datamarket.azure.com/Data.ashx/data.gov/Crimes/$metadata](https://api.datamarket.azure.com/Data.ashx/data.gov/Crimes/$metadata)).


		<?xml version="1.0" encoding="utf-8" standalone="yes" ?> 
		<edmx:Edmx Version="1.0" xmlns:edmx="http://	schemas.microsoft.com/ado/2007/06/edmx" xmlns:dr="http://schemas.microsoft.com/dallas/2010/04">   
   			<edmx:DataServices xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" m:DataServiceVersion="1.0">      
      			<Schema Namespace="data.gov.Crimes"xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices"
              			xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"
              			xmlns="http://schemas.microsoft.com/ado/2007/05/edm">
         			<EntityType Name="CityCrime">
            		  	<Key>
               			 <PropertyRef Name="ROWID" />
            			</Key>
            			<Property Name="ROWID" Type="Edm.Int32" Nullable="false" dr:Queryable="true" dr:Returned="true" />
            			<Property Name="State" Type="Edm.String" Nullable="true" dr:Queryable="true" dr:Returned="true" />
            			<Property Name="City" Type="Edm.String" Nullable="true" dr:Queryable="true" dr:Returned="true" />
            			<Property Name="Year" Type="Edm.Int32" Nullable="false" dr:Queryable="true" dr:Returned="true" />
            			<Property Name="Population" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
            			<Property Name="ViolentCrime" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
            			<Property Name="MurderAndNonEgligentManslaughter" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
            			<Property Name="ForcibleRape" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
            			<Property Name="Robbery" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
            			<Property Name="AggravatedAssault" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
            			<Property Name="PropertyCrime" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
            			<Property Name="Burglary" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
            			<Property Name="LarcenyTheft" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
            			<Property Name="MotorVehicleTheft" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
            			<Property Name="Arson" Type="Edm.Int32" Nullable="false" dr:Queryable="false" dr:Returned="true" />
         			</EntityType>
         			<EntityContainer Name="datagovCrimesContainer" m:IsDefaultEntityContainer="true">
            			<EntitySet Name="CityCrime" EntityType="data.gov.Crimes.CityCrime" />
         			</EntityContainer>
      			</Schema>
			</edmx:DataServices>
		</edmx:Edmx>

**Code Example 1 – Metadata XML**

You are able to get a lot of useful information from the schema.


- The entity container name. <br>
*<EntityContainer Name="datagovCrimesContainer" m:IsDefaultEntityContainer="true">* <br>
This is the type of the private *context* identifier used to authenticate access to the service. 

- The entity set name and type. <br>
*<EntitySet Name="CityCrime" EntityType="data.gov.Crimes.CityCrime" />*
This is the type of the IEnumerable<T> and IList<T>.

- The entity and type. <br>
*<EntityType Name="CityCrime">*
This is the type used in your query and *foreach (For Each)* loop variable. 

- The name of each field that is returned by a query. <br>
*Name=”State”*

- The data type of each field. <br>
*Type=”Edm.String”*

- Whether the field can be null or not.<br>
*Nullable=”false”*

- Whether or not a field may be used to filter query results.<br>
*dr:Queryable=”true”<br>
dr:Queryable="false"<br>*
A queryable field may be used in a *where (Where)* clause of your query. Non-queryable fields cannot be used in a query *where (Where)* clause. 

- Whether or not this field is returned when you query the dataset.<br> 
*dr:Returned=”true”*


 -----------
##See Also

###Tasks<br />
Compare Fixed and Flexible Query Types

###Concepts
Supported OData Query Options <br>
Compare Flexible and Fixed Query Code

###Other Resources
LINQ Query Expressions (C# Programming Guide)<br>
LINQ in Visual Basic<br>
Code Sample: DataMarket Web App


