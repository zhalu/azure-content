 
<properties 
   pageTitle="JSON Support" 
   description="What JSON Support is Available" 
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
# JSON Support 

 -----------
Windows Azure Marketplace (WAM) enables JSON support for WSPF and JSON/P support for all WAM services. Such support is important for creators of applications that want to request data cross-domains.

 -----------
###JSON support for Marketplace services
Applications specify that they require a JSON response by adding a *$format* parameter to their request URL.
	
	*note
	See http://www.odata.org/developers/protocols/json-format for additional information on the JSON specification.
	
	*Important
	The Marketplace supports OData 2, not OData 1. 

###The $format parameter
The *$format* parameter is optional. When provided, it specifies the return format for a Marketplace dataset. Supported values are “json” and “atom.” If the parameter is omitted, the Marketplace returns an ATOM response.


<table>
  <tr>
<td>$format included
</td><td>$format value
</td><td>response 
</td>
</tr>
<tr>
<td>No 
</td><td>N/A
</td><td>ATOM 
</td>
</tr><tr>
<td>Yes 
</td><td>ATOM
</td><td>ATOM 
</td>
</tr><tr>
<td>Yes
</td><td>JSON
</td><td>JSON 
</td>
</tr><tr>
<td>Yes
</td><td>Any other value
</td><td>Error 
</td>
</tr>
</table>

The following example requests the response in JSON format.

	https://api.datamarket.azure.com/Services/All/Datasets?$format=json


###JSON/P support for Marketplace services

Applications are able to request and received data crossdomain using JSON/P.


####The $callback parameter
The *$callback* parameter is optional for requests, but is required for JSON/P requests. It can only be used with *$format=json*, otherwise the request is invalid and fails. When you specify the *$callback* value the Marketplace pads the JSON format with a call to the JavaScript method specified in the *$callback* value.

For example:


<table>
  <tr>
<td>Request 
</td><td>$format value
</td><td>$format=json&$callback=myMethod
</td>
</tr>
<tr>
<td>Response
 
</td><td>{'x1':'A', 'x2':'B'}

</td><td>myMethod({'x1':'A', 'x2':'B'})
 
</table>


The JSON/P formatted result automatically causes the JavaScript engine in the browser to trigger the callback method once the data download is complete. Thus, the developer can include a script tag that points directly to the data source and trigger code without the need to manage XmlHttpRequest callbacks or other infrastructure.

For example,

	<script type="text/javascript"
	src=https://api.datamarket.azure.com/Services/All/Datasets?$format=json&$callback=response>
	</script>

<table>
  <tr>
<td>$format
</td><td>$callback
</td><td>response 
</td>
</tr>
<tr>
<td>Not present
</td><td>Present
</td><td>Error

</td>
</tr><tr>
<td>Something other than json
 
</td><td>Present
</td><td>Error 
</td>
</tr><tr>
<td>json
</td><td>not present
</td><td>JSON 
</td>
</tr><tr>
<td>json
</td><td>JavaScript identifier

</td><td> name>(JSON)
 
</td>
</tr>
</table>

###The accessToken parameter
The *accessToken* parameter enables you to pass the OAuth Access Token to the Marketplace through the URL rather than through HTTP headers. In turn, you are able to include all the data required to obtain data in the src attribute of a script tag. This also provides a convenient workaround to scenarios in which some browsers prevent downloading content from other domains when the necessary information is passed through HTTP headers.

	*important
	After getting the OAuth token, developers UrlEncode it and pass it to the parameter accessToken.

For example:

	<script type="text/javascript"
	src="https://api.datamarket.azure.com/data.gov/crimes/CityCrime?$filter=City eq 'Seattle'&$format=json&$callback=response&accessToken=...">
	</script>

###Obtaining a WAM access token
To learn about obtaining an access token, look here: [Implement OAuth in your Marketplace App](./marketplace-data-market-implement-oath-in-marketplace-app.md). Web applications that take advantage of the new JSON/P feature must implement an OAuth Authentication flow that causes a user to log in and to grant access to their Marketplace subscription. The refresh token for that user can then be associated with that user’s identity on the web application and can be used to obtain new Access Tokens each time an old access token expires. 



##See Also
###Concepts
Develop a Marketplace Application
