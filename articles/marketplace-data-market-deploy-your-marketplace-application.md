<properties 
   pageTitle="Deploy Your Marketplace Application" 
   description="How to Deploy Your Marketplace Application" 
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
#  Deploy Your Marketplace Application

 -----------
One of the easiest ways to make your application Internet accessible is to deploy it to Azure. This topic walks you through the process to deploy your application to Microsoft Azure. 

 -----------

### Deploy Your Marketplace Application

1. Sign up for one of the available Microsoft Azure offers found on the [Microsoft Online Services Customer Portal](http://go.microsoft.com/fwlink/?linkid=223338).

2. Navigate your browser to the [Azure Developer Portal](http://azure.microsoft.com/en-us/documentation/).

3. If any SQL resources are needed for your application, such as using the SQL Membership Provider, provision a SQL Database.
	<br>*Make sure that you configure firewall rules for your Azure SQL Database Instance.
<br>
*Make sure that you create a login that has nonadministrative access to your database.<br>
*If you are using one of these samples, connect to your Azure SQL Database and run the provisioning script located in *Database\Scripts\AzureDeploy.sql.*

		*Important
		Before you run the script, make sure that all variables are correctly set to reflect the database name and login you created.
		

		GO
		:setvar dbuser "MyAppUser"
		:setvar DatabaseName "MyDatabase"

		CREATE user [$(dbuser)] FOR LOGIN [$(dbuser)] WITH DEFAULT_SCHEMA = dbo;
		GO

4. In Visual Studio, create Cloud Application project that references your web application as a Web Role. <br><br> 
![alt text](./marketplace-data-market-deploy-your-marketplace-application/cloudapplication.png)


5. Make sure that your connection strings are set to point to the SQL Database you provisioned in step 3, including username and password of the user that accesses the database.

6. Publish your cloud application.

##See Also
###Tasks
Create a Flexible Query Application <br>
Create a Fixed Query Application

###Concepts
Compare Flexible and Fixed Query Code
