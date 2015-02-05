<properties 
   pageTitle="Implement HTTP Basic Authentication in Azure Marketplace Data Service" 
   description="How to implement HTTP basic authentication in Azure Marketplace data services" 
   services="cloud-services" 
   documentationCenter="dev-center-name" 
   authors="kevinscharpenberg" 
   manager="manager-alias" 
   editor=""/>

<tags
   ms.service="marketplace"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="data-services" 
   ms.date="02/02/2015"
   ms.author="kevsch"/>

## Implement HTTP Basic Auth in your Marketplace App 

 HTTP Basic Authentication is one of two authentication protocols supported by the Marketplace. Since this authentication method requires storing the user’s name and password for all access, we recommend that you use HTTP Basic Authentication only when you are creating an application for your own use or a single account.
 

### HTTP Basic Authentication
HTTP Basic Authentication uses a user id and password to authenticate a user and then grant or deny access to a protected resource. The Marketplace implementation of HTTP Basic Authentication ignores the user id and requires a valid Marketplace account key (for example, /Xroufd9KIlLkr4Mjf8afk). As you design your application you need to decide whether you will include the account key in the application code, which makes your account key vulnerable to anyone who has the application, or ask the user to enter it at run time, which is error prone given the length and complexity of the key.

###Preliminaries
The code to implement HTTP Basic Authentication is relatively short and simple. Before you get to the code you must do the following in your application code.

1. Ensure that your project includes System.Net and your service class or reference namespace.  

	C#
		using System.Net;
		using service_class_namespace;
 
	Visual Basic   
    	Imports System.Net
    	Imports service_class_namespace
     
2. Create a Uri instance from the service’s root URL. 

To find the service root URL:


a. Click the **My Data** tab at the [Marketplace](https://datamarket.azure.com/account) home page.


b. Locate the dataset you need the root service URL to.


c. Click **Use**.


d. Scroll down and click the **Details** tab.


e. Include this URL in your application code.


	C#   
    	Uri serviceUri = new Uri(SERVICE_ROOT_URL);
     
	Visual Basic   
    	Private serviceUri As Uri
    	serviceUri = new Uri(SERVICE_ROOT_URL)
     

3. Create an identifier of the type of the dataset’s container. 

There are two ways to find the container name.

First,


a. Open the **Object Browser** in Visual Studio.


b. Locate your service class or reference.


c. Double-click the class name to expand it.


d. Locate a type whose name ends with “Container”. 
For example: ContosoSalesContainer.


Alternatively, you can use the service root URL to open the metadata page of the service. For example, if the service root URL is `https://datamarket.azure.com/data.ashx/contoso/sales/` navigate your browser to `https://datamarket.azure.com/data.ashx/contoso/sales/$metadata`.

Find the EntityContainer tag. The value of the Name attribute is the service container name. Example: `<EntityContainer Name="ContosoSalesContainer">`


	C#
		ContosoSalesContainer context;
     
	Visual Basic
		Private context As ContosoSalesContainer
     

### Implement HTTP Basic Authentication in an Application
There are just two steps to implement HTTP Basic Authentication.

1. Instantiate the context identifier.

	C#   
    	context = new ContosoSalesContainer(serviceUri);
     
	Visual Basic
		context = new ContosoSalesContainer(serviceUri)
 

2. Add the credentials to the context. 


	C#   

    context.Credentials = new NetworkCredential(USER_ID, SECRET_ACCOUNT_KEY);
 

	Visual Basic   
    context.Credentials = new NetworkCredential(USER_ID, SECRET_ACCOUNT_KEY)
     

#### Note  
At this time the Marketplace ignores the USER_ID so you can use an empty string in its place. Do not skip this parameter.
 


--------------------------------------------------------------------------------
