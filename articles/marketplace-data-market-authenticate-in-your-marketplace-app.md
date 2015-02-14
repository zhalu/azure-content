 
<properties 
   pageTitle="Authenticate in your Marketplace App" 
   description="How to Authenticate in your Marketplace App" 
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
#**Authenticate in your Marketplace App**
 -----------
Every access to a Marketplace dataset, whether free or paid, must authenticate the user before access is granted. When you create an application the authentication process must be included in your code. Marketplace provides two means of authenticating access:

* HTTP Basic Authentication
* OAuth Authentication

Which you use depends on the expected use of your application.
 
 -----------
###In This Section


[Select an Authentication Protocol](./marketplace-data-market-select-authentication-protocol.md)

[Implement OAuth in your Marketplace App ](./marketplace-data-market-implement-oath-in-marketplace-app.md)

[Implement HTTP Basic Auth in your Marketplace App](.marketplace-data-market-implement-http-basic-auth-in-marketplace-app.md)


<table>
  <tr>
<td>Link</td><td>Description</td>
</tr>

<td> Select an Authentication Protocol
</td><td>Determine which Marketplace supported authentication protocol best fits your program needs.</td>
</tr>

<td>Implement OAuth in your Marketplace App</td><td>OAuth permits your application to be widely distributed and used with each user paying for their own use.</td>
</tr>

<td>Implement HTTP Basic Auth in your Marketplace App   </td><td>HTTP Basic Authentication should be used only under specific application conditions. This article explains which uses are reasonable for HTTP Basic Authentication and how to implement it in your application. <br /><br />



HTTP Basic Authentication passes a User ID and Password over https to the Marketplace. <br />
Use HTTP Basic Authentication only if:
<br /><br />



* It is safe to hard-code (and thus potentially expose) your account key in the application, and<br /><br />
* It is acceptable that all access to the Marketplace datasets be charged to your account, and <br /><br />
* You will not need to remove access from some users while not affecting access of others, or <br /><br />
* If you will require each user to enter their own ID and private Marketplace account key, such as KufDkfLk39-xMwqFGCvDFq3-6rXcvGF+Wxc73z1hhJ whenever they attempt to access a dataset.</td>

</table>

