 
<properties 
   pageTitle="Retrieve a User's Subscription Info" 
   description="How to Retrieve a User's Subscription Info" 
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
# Retrieve a User's Subscription Info 

 -----------
Determine, at runtime, which WAM datasets a user subscribes to. With this information you can then leverage the datasets they subscribe to or offer them the opportunity to subscribe to datasets needed by your application. Other than this user’s subscription information, you cannot access other user information.


 -----------
###Authentication
The My Datasets service requires an access token to be passed in each request to authenticate the calling application. To obtain an access token, see the [Marketplace OAuth documentation](https://msdn.microsoft.com/library/azure/gg193416.aspx). 

To access this service, you must request consent with *x_permissions=account*.


###Call the Service
The endpoint for the My Datasets service is [https://api.datamarket.azure.com/Services/My/Datasets](https://api.datamarket.azure.com/Services/My/Datasets). There are no request parameters for the service.
 

###Response Parameters
The response from the service is an Atom feed with one entry for each subscription for the user’s account. The response parameters are:

<table>
  <tr>
<td>Parameter
</td><td>Type
</td><td>Description  
</td>
</tr>
<tr>
<td>OfferId
 
</td><td>Guid

</td><td>ID of an offer the user is subscribed to 
</td>
</tr><tr>
<td>Title
 
</td><td>String

</td><td>Title of the offer.
 
</td>
</tr><tr>
<td>Description

</td><td>String

</td><td>Description of the offer.
 
</td>
</tr><tr>
<td>ProviderId

</td><td>Guid

</td><td>Unique identifier of the offering provider.
 
</td>
</tr>

  <tr>
<td>ProviderName

</td><td>String

</td><td>Unique name for the data provider.
  
</td>
</tr>
<tr>  <tr>
<td>ProviderDescription

</td><td>String

</td><td>Description of the data provider.
  
</td>
</tr>
<tr>  <tr>
<td>Category

</td><td>String

</td><td>Primary category of the offer.
  
</td>
</tr>
<tr>  <tr>
<td>ServiceEntryPointUrl

</td><td>String

</td><td>URL where queries can be made against this offer.
  
</td>
</tr>
<tr>  <tr>
<td>PreviewUrl

</td><td>String

</td><td>Url of the offer logo.
  
</td>
</tr>
<tr>  <tr>
<td>MarketplaceDetailUrl

</td><td>String

</td><td>URL of the offer detail page on the Marketplace.
  
</td>
</tr>
<tr>  <tr>
<td>Type

</td><td>Int

</td><td>Reserved for future use.
  
</td>
</tr>
<tr>
</td>
</tr>
<tr>  <tr>
<td>Status

</td><td>Int

</td><td> Integer that represents the subscription status.<br>

2 - Active <br>
3 - Suspended<br>
4 - Canceled<br>
5 - Provisioning<br>
7 – Purchase error<br>
All other values may be treated as error states.
   
</td>
</tr>
<tr></td>
</tr>
<tr>  <tr>
<td>ResourceBalance

</td><td>Int

</td><td>Currently available balance for the user’s subscription.
  
</td>
</tr>
<tr></td>
</tr>
<tr>  <tr>
<td>ResourceType

</td><td>String

</td><td>Units for ResourceBalance. <br>
Example: Transactions
  
</td>
</tr>
<tr>

</table>

###Example Call

	GET /Services/My/Datasets HTTP/1.1
	Host: api.datamarket.azure.com
	Connection: keep-alive
	Cache-Control: max-age=0
	Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims
	%2fnameidentifier=adamw_dnbcrm&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fdatamarket.accesscontrol.windows.net%2f&Audience=https%3a%2f%2fsvcs.marketplace.azure.com%2f&ExpiresOn=1314920964&Issuer=https%3a%2f%2fdatamarket.accesscontrol.windows.net%2f&HMACSHA256=UR%2fQ0p3BixKpF8Fla7JwX7kVIwZx5bR60embAlvmcVs%3d
	User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/535.7 (KHTML, like Gecko) Chrome/16.0.912.77 Safari/535.7
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
	Accept-Encoding: gzip,deflate,sdch
	Accept-Language: en-US,en;q=0.8
	Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3


###Example Response

	HTTP/1.1 200 OK
	Content-Length: 89771
	Content-Type: application/xml; charset=utf-8
	<feed xmlns="http://www.w3.org/2005/Atom" xmlns:base="https://api.datamarket.azure.com/Services.svc/My/Datasets" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata">
  	<title type="text">List of all subscribed Azure Marketplace datasets</title>
  	<id>https://api.datamarket.azure.com/Services.svc/My/Datasets</id>
  	<rights type="text">2012 Microsoft</rights>
  	<updated>2012-02-08T05:49:28Z</updated>
  	<link rel="self" title="List of all subscribed Azure Marketplace datasets" href="https://api.datamarket.azure.com/Services.svc/My/Datasets"/>
  	<entry>
	<id>https://api.datamarket.azure.com/Services.svc/My/Datasets&amp;$page=2
	&amp;$itemsperpage=1(640bda37-f32e-4186-84ac-112919155746)</id>
    <title type="text">UNESCO UIS Data - UNESCO Institute of Statistics</title>
    <updated>2012-02-08T05:49:28Z</updated>
    <content type="application/xml">
      <m:properties>
        <d:OfferId m:type="Edm.Guid">640bda37-f32e-4186-84ac-112919155746</d:OfferId>
        <d:Title m:type="Edm.String">UNESCO UIS Data - UNESCO Institute of Statistics</d:Title>
        <d:Description m:type="Edm.String">The Data Centre of the UNESCO Institute for Statistics (UIS) contains over 1,000 types of indicators and raw data on education, literacy, science and technology, culture and communication. The UIS collects these data from more than 200 countries and other international organizations.</d:Description>
        <d:ProviderId m:type="Edm.Guid">68c1c378-2326-458d-ac46-53fbf7e4f374</d:ProviderId>
        <d:ProviderName m:type="Edm.String">United Nations</d:ProviderName>
        <d:ProviderDescription m:type="Edm.String">The United Nations Statistics Division (UNSD) of the Department of Economic and Social Affairs (DESA) launched a new internet based data service for the global user community. It brings UN statistical databases within easy reach of users through a single entry point (&lt;a href = "http://data.un.org/"&gt;http://data.un.org/&lt;a&gt;). Users can now search and download a variety of statistical resources of the UN system.&#xD; &#xD; At the occasion of the launch of this service DESA Under-Secretary General Sha Zukang stated: &#xD; &#xD; "The UN-system has accumulated over the past 60 years an impressive amount of information. UNdata , developed by the Statistics Division of DESA, is a new powerful tool, which will bring this unique and authoritative set of data not only to the desks of decision makers and analysts, but also to journalists, to students and to all citizens of the world."&#xD; Since its foundation, the United Nations System has been collecting statistical information from member states on a variety of topics. The information thus collected constitutes a considerable information asset of the organization. However, these statistical data are often stored in proprietary databases, each with unique dissemination and access policies. As a result, users are often unaware of the full array of statistical information that the UN system has in its data libraries. The current arrangement also means that users are required to move from one database to another to access different types of information. UNdata addresses this problem by pooling major UN databases and those of several international into one single internet environment. The innovative design allows a user to access a large number of UN databases either by browsing the data series or through a keyword search.&#xD; &#xD; Useful features like Country Profiles, Advanced Search and Glossaries are also provided to aid research. The numerous databases, tables and glossaries containing over 60 million data points cover a wide range of themes including Agriculture, Crime, Education, Employment, Energy, Environment, Health, HIV/AIDS, Human Development, Industry, Information and Communication Technology, National Accounts, Population, Refugees, Tourism, Trade, as well as the Millennium Development Goals indicators. Whilst this initial version of UNdata is fully equipped with all the functionalities for data access, the development team is continuously adding new databases and features to further enhance the usefulness to users. When fully developed, UNdata will have a comprehensive array of international and national databases providing the world instant access to a wealth of statistical information.&#xD; &#xD; UNdata is the brainchild of UNSD, the statistical arm of the Department of Economic and Social Affairs and the coordinator of statistical activities throughout the UN System. UNSD's core mission is to advance the development of the global statistical system and promote the dissemination of statistical information. This database service is part of a project launched by UNSD in 2005, called "Statistics as a Public Good", whose objectives are to provide free access to global statistics, to educate users about the importance of statistics for evidence-based policy and decision-making and to assist National Statistical Offices of Member Countries to strengthen their data dissemination capabilities. The project is implemented in partnership with Statistics Sweden and the Gapminder Foundation with partial financial support from the Swedish International Development Cooperation Agency (SIDA).</d:ProviderDescription>
        <d:Category m:type="Edm.String">Science &amp; Statistics</d:Category>
        <d:ServiceEntryPointUrl m:type="Edm.String">https://api.datamarket.azure.com/Data.ashx/UnitedNations/UNESCO</d:ServiceEntryPointUrl>
        <d:PreviewUrl m:type="Edm.String">https://datamarket.azure.com/handlers/Image.ashx?type=Offer&amp;id=640BDA37-F32E-4186-84AC-112919155746</	d:PreviewUrl>
        	<d:MarketplaceDetailUrl m:type="Edm.String">https://datamarket.azure.com/dataset/640BDA37-	F32E-4186-84AC-112919155746</d:MarketplaceDetailUrl>
        	<d:Type m:type="Edm.Int32">0</d:Type>
        	<d:Status m:type="Edm.Byte">2</d:Status>
      		</m:properties>
    		</content>
  		</entry>
	</feed>



##See Also
**Use Datasets in Your Application**
