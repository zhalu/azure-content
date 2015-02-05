<properties 
   pageTitle="Implement OAth in Azure Marketplace Data Service" 
   description="How to implement OAth in Azure Marketplace data services" 
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

## Implement OAuth in your Marketplace App 

Developers can create and market their applications on the Marketplace. These applications may consume Marketplace data, in which case the user would have to subscribe to the dataset, or they may use no data from an outside source.
 

### User Consent Flows
Before an application accesses the Marketplace on behalf of a user, that user must provide consent for the application to access their account and subscriptions. The process by which a user provides that consent is the OAuth User Consent Flow.

The consent flow can contain different steps depending on the state of the user’s account and the consent options your application requests.

When the user successfully provides consent, your application is able to obtain an access token that it then used to authenticate against the Marketplace services on behalf of the user.

The subsections below describe how you can integrate the Oauth consent flow into your application depending on your architecture.

### Consent Flow for ASP.NET Web Applications with the Windows Identity Foundation Extension for OAuth
The Windows Identity Foundation (WIF) Extension for OAuth makes it easy to integrate with the Marketplace using OAuth. The library implements the OAuth2.0 protocol and exposes simple methods to manage the user consent flow.

##### Note  
The Windows Identity Foundation (WIF) Extension for OAuth is a Community Technology Preview (CTP) and is not supported by Microsoft.
 


### Prerequisites

Download and install the [Windows Identity Foundation Runtime](http://go.microsoft.com/fwlink/?linkid=234216)..


Download and install the [Windows Identity Foundation (WIF) Extension for OAuth](http://go.microsoft.com/fwlink/?LinkId=217261).


Add a reference in your project to the following two assemblies:


Microsoft.IdentityModel.Protocols.OAuth
This assembly is in the target directory where you unzipped the Windows Identity Foundation (WIF) Extension for OAuth.


System.IdentityModel
This assembly is in your .NET Runtime install directory.


### Begin the Consent Flow
You can begin the consent flow by calling the static RedirectToEndUserEndpoint() method on the OAuthClient class. This causes the current HTTP request to respond with an HTTP 302 redirect to the Marketplace Consent Flow.

The third parameter in the code sample below is the URL that the user’s browser is redirected to after the consent flow is complete. This must match the Redirect URI you provided when registering your application with Marketplace.

   
    OAuthClient.RedirectToEndUserEndpoint(
      "https://datamarket.azure.com",
      AuthorizationResponseType.Code,
      "http://myapp.com/authcomplete");

 

### Receive the Post-Consent Redirect
When the user completes the consent flow or if there is an error, the user’s browser is redirected back to your application at the URI you previously provided. The WIF Extension for OAuth receives and processes this redirect and calls an event handler that you register.

To enable the WIF Extension for OAuth to process the redirect, you must register the client library’s handler by creating or adding the following to the Web.config of your ASP.NET application.

   
    <system.webServer>
       <handlers>
      <add name="DataMarketOAuthHandler" 
       verb="*" 
       path="DataMarketOAuthHandler.ashx"
       type="Microsoft.IdentityModel.Protocols.OAuth.Client.EndUserAuthorizationResponseHandler, 
     Microsoft.IdentityModel.Protocols.OAuth" />
       </handlers>
    </system.webServer>

 

You can choose your own values for the name and path attributes. The absolute URL consists of your application’s base URL concatenated with the path attribute for the `OAuthClient.RedirectToEndUserEndpoint()` method. This absolute URL must match the one you provided when registering your application with theMarketplace.

Second, you must implement event handlers to receive the OAuth 2.0 access and refresh tokens or to handle a consent flow error. The methods you implement must match the following signatures.

   
public void OAuthClientSettings.AccessTokenReceived(
  object Sender,
  AccessTokenReceivedEventArgs tokenReceivedEventArgs);

Void OAuthClientSettings.EndUserAuthorizationFailed(
  object Sender,
  EndUserAuthorizationFailedEventArgs authorizationFailedEventArgs);

 

In the AccessTokenReceived handler you obtain the access token at `tokenReceivedEventArgs.AuthorizationResponse.Parameters[OAuthConstants.AccessToken]` and the refresh token at `tokenReceivedEventArgs.AuthorizationResonse.Parameters[OAuthConstants.RefreshToken]`.

###Configure the WIF Extension for OAuth
Add the following code to your application to configure the WIF Extension for OAuth with the Marketplace OAuth settings. You could add this to the Application_Start method for your ASP.NET HttpApplication class.

In the code below replace the placeholders with the Client ID and Client Secret values you obtained when you registered your application. Replace AccessTokenReceived and EndUserAuthorizationFailed with the names of your event handlers as described in the section above.

  
    // set up the ServerRegistry
    InMemoryAuthorizationServerRegistery serverRegistry = 
       new InMemoryAuthorizationServerRegistry(); 
    AuthorizationsServerRegistration registrationInfo = 
       new AuthorizationServerRegistration(   "https://datamarket.accesscontrol.windows.net/v2/OAuth2-13",
       "https://datamarket.azure.com/embedded/consent", 
       <<Your OAuth Client ID>>, 
       <<Your OAuth Client Secret>>>);
    
    serverRegistry.AddOrUpdate(registrationInfo);
    OAuthClientSettings.AuthorizationServerRegistry = serverRegistry; 
    
    // set up the ResourceRegistry 
    InMemoryResourceScopeMappingRegistry resourceRegistry = 
       new InMemoryResourceScopeMappingRegistry(); 
    
    resourceRegistry.AddOrUpdate(
     "https://datamarket.azure.com/embedded/consent", 
     "https://datamarket.accesscontrol.windows.net/v2/OAuth2-13”, 
     "https://datamarket.azure.com/embedded/consent", 
     new string[] { "" }); 
    OAuthClientSettings.ResourceScopeMappingRegistry = resourceRegistry; 
    
    // handle the token received event 
    OAuthClientSettings.AccessTokenreceived += 
       new EventHandler<AccessTokenReceivedEventArgs>(OAuthClientSettings_AccessTokenReceived);  
    
    // handle the event when the user denies consent 
    OAuthClientSettings.EndUerAuthorizationFailed += 
       new EventHandler<EndUserAuthorizationFailedEventArgs>(OAuthClientSettings_EndUserAuthorizaitonFailed);  
    
    // register the Authentication Module
    AuthenticationManager.Register(new OAuthAuthenticationModule());

 

###Consent Flow for Web Applications
This section describes how to integrate your web application with the Marketplace OAuth 2.0 consent flow. If your web application is implemented using ASP.NET, you should consider using the Windows Identity Foundation (WIF) Extension for OAuth as described in the previous section.

A web application begins the consent flow by navigating the user’s browser to the Marketplace Consent URL. The user will then complete the consent flow steps in their browser window. When complete, the user’s browser will be redirected by Marketplace to your application’s Post Consent Redirect URL.

Begin the Consent Flow
You begin the consent flow by navigating the user’s browser to the Marketplace Consent URL. This URL is constructed using the base URL and query string parameters.

The base URL is https://datamarket.azure.com/embedded/consent.

The consent flow URL supports the following query string parameters.

	Parameter  	Required/Optional  	Description  
	client_id 		Required 			The client ID you registered with the Marketplace.

 
	redirect_uri 	Optional 			The URI that the user’s browser is redirected to once the consent flow is complete.If provided, the system validates that this parameter matches the redirect URI pre-registered for this client. They match if all components of the URI are the same except for the query string.This parameter value must be URL encoded.
 
	response_type 	Required 			The mechanism that will be used to return an access token to the requesting application. Only the value code is supported.
 
	state 			Optional 			You can use this parameter to pass arbitrary data from the beginning to the end of the consent flow. Any value you include for this parameter will be appended to the scope query string parameter when the user’s browser is redirected to the redirect URI after the consent flow is finished.
 
	x_permissions Optional 			This parameter determines what permissions your application will have for the user’s Azure Marketplace account. This parameter can either contain the word account or an offer identifier. With account, your application will have access to the user’s entire Azure Marketplace account, including all current and future subscriptions. With an offer identifier, your application will have access only to subscriptions to the specified offer. 

	Offer identifiers can be specified as a space-delimited list. Each offer identifier corresponds to the provider and offer names from the Service Root URL on that offer’s dataset detail page. For example, to request access to the Data.gov Crime dataset, you would construct the x_permissions parameter as follows:

	Look at the dataset detail page for the offer here.


	Find the Service Root URL in the Details tab. For this offer, it is https://api.datamarket.azure.com/data.gov/Crimes/.


	Construct the offer identifier by taking the provider and offer parts of the URL. For this offer, it is data.gov/Crimes.


	Set x_permissions=data.gov/Crimes.


	If offer identifier(s) are specified, any access tokens from this consent grant are scoped to only access the specified offers.

	If account is specified, any access tokens from this consent grant all access to all current and future offers.
 
	x_required_offers 		Optional		 This parameter requires that the user has a subscription to the specified offer. If the user does not already have an active subscription, the user is prompted to subscribe as part of the consent flow.

	The offer identifier used in this parameter have the same format as those in the x_permissions parameter defined above.

	If this parameter is specified, x_permissions is automatically set to the same offer identifier and can’t be set on the query string.
 
	x_scope 		Optional 		The URL-encoded form of the endpoint hosting the data service you will access. If omitted, the default is https://api.datamarket.azure.com/.

	For example, if you are accessing the data service at https://api.datamarket.azure.com/data.gov/crimes, then the scope value is https://api.datamarket.azure.com/.

	Similarly, if you are accessing the data service at http://api.microsofttranslator.com, then the scope value is http://api.microsofttranslator.com/.
 

For example, the following consent URL would request access to a user’s entire account. 

The line breaks are for readability only and should not be included in your code.

   
    https://datamarket.azure.com/embedded/consent?
    client_id=myapp&
    response_type=code&
    x_permissions=account
    
 

For example, the following consent URL would request access to a user’s entire account and require that they have an active subscription to the Data.gov Crime dataset.

The line breaks are for readability only and should not be included in your code.

   
    https://datamarket.azure.com/embedded/consent?
    client_id=myapp&
    response_type=code&
    x_required_offers=data.gov/Crimes

 

The example below would require that the user have an active subscription to the Microsoft Translator subscription and allow access to the SOAP endpoint at http://api.microsofttranslator.com/V2/Soap.svc.

The line breaks are for readability only and should not be included in your code

   
    https://datamarket.azure.com/embedded/consent?
    client_id=myapp&
    response_type=code&
    x_required_offers= Bing/MicrosoftTranslator&
    x_scope=http%3a%2f%2fapi.microsofttranslator.com%2f
    0
 

Once your application has constructed an Marketplace Consent URL, you can navigate the user’s browser to this URL, either through a HTTP 302 redirect or by opening and navigating a new browser to this URL.

### Receive the Post-Consent Redirect
When the user completes the consent flow or if there is an error, the user’s browser will be redirected back to your application’s Post Consent Redirect URL.

If the consent flow was successful, the post-consent redirect URL will have a query string parameter named code that contains the authorization code returned from the Marketplace. You can exchange this code for an access token and refresh token for use authenticating with the Marketplace services.

If the consent flow was not successful, the post-consent redirect URL will contain the following query string parameters.

	Parameter  Description  
	error
 			A single error code from the following:

	invalid_request
	The request is missing a required parameter, includes an unsupported parameter or parameter value, or is otherwise malformed.


	unauthorized_client
	The client is not authorized to request an authorization code using this method.


	access_denied
	The resource owner or authorization server denied the request.


	unsupported_response_type
	The authorization server does not support obtaining an authorization code using this method.


	invalid_scope
	The requested scope is invalid, unknown, or malformed.


 
	error_description
 	A human-readable text providing additional information, used to assist in the understanding and resolution of the error occurred.
 
	state
 	If present, this is the "state" parameter from the original consent request. Set to the exact value received from the application.
 

### Exchange the Authorization Code for an Access Token and Refresh Token
You exchange the authorization code for an access token and refresh token by making an HTTP POST request to the Marketplace OAuth 2.0 token endpoint (https://datamarket.accesscontrol.windows.net/v2/OAuth2-13).

The request to this endpoint must have several parameters in the HTTP request body. The request body must be of the content type application/x-www-form-urlencoded.

	Parameter  	Required/Optional  		Value  
	client_id 	Required 				The client ID of your application that you registered with Marketplace. The client_id must match the client ID passed to the Marketplace Consent URL to begin the consent flow and must be in URL-encoded form.
 
	client_secret Required 				The client secret of your application that you registered with Marketplace. The client_secret must be in URL-encoded form.
 
	code 		Required 				The authorization code you received on the post-consent redirect URL. The authorization code must be in URL-encoded form.
 
	grant_type Required 				Must be the authorization_code.
 
	redirect_uri Required 				The redirect URI you provided when registering your application. The redirect_uri must be in URL-encoded form.
 
	scope 		Required 				The URL-encoded form of the endpoint hosting the data service you will access. This must match the scope value you provided when invoking the consent flow.

	For example, if you are accessing the data service at https://api.datamarket.azure.com/data.gov/crimes, then the scope value is https://api.datamarket.azure.com/.

	Similarly, if you are accessing the data service at http://api.microsofttranslator.com, then the scope value is http://api.microsofttranslator.com/.
 

Your request to the token endpoint to exchange an authorization code might look as follows.

#### Note  
The line breaks in the HTTP request body are only for readability and should be removed.
 


   
    Post /v2/OAuth2-13 HTTP/1.1
    Host: datamarket.accesscontrol.windows.net
    Content-Type: application/x-www-form-urlencoded
    
    code=1235486542&
    client_id=myapp&
    client_secret=MzX8SVXpgjOQWODwZfqiUGfp0FvGPZ&
    redirect_uri=https%3a%2f%2fmyapp.com%2fauthcomplete&
    grant_type=authorization_code&
    scope=https%3a%2f%2fapi.datamarket.azure.com%2f

 

You receive back an access token encoded in a JSON object.

   
    HTTP/1.1 200 OK
    Cache-Control: public, no-store, max-age=0
    Content-Type: application/json; charset=us-ascii
    Expires: Wed, 20 Apr 2011 18:48:53 GMT
    Last-Modified: Wed, 20 Apr 2011 18:48:53 GMT
    Vary: *
    Server: Microsoft-IIS/7.0
    Set-Cookie: ASP.NET_SessionId=chqpl445frmvsaeozn45bu55; path=/; HttpOnly
    X-AspNetMvc-Version: 2.0
    X-AspNet-Version: 2.0.50727
    X-Powered-By: ASP.NET
    Date: Wed, 20 Apr 2011 18:48:53 GMT
    Content-Length: 883
    
    {"access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=812d5dea-1111-43c0-b2af-38cbe4d58bf8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fpermissions=10a6465f-b0a6-49ca-9175-b24caaf74db0&http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2009%2f09%2fidentity%2fclaims%2factor=myapp&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=DataMarketIdentityProvider&Audience=https%3a%2f%2fapi.datamarket.azure.com&ExpiresOn=1303325933&Issuer=https%3a%2f%2fdatamarket.accesscontrol.windows.net%2f&HMACSHA256=YWSfH6Byumh7HqI4j7U8dsXFD88f42irvNVtGdG8zCY%3d",
    "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
    "expires_in":"599",
    "refresh_token":"uG/QvG8eKagO5NFM2XcnSQ==","scope":
    "https://api.datamarket.azure.com/"}
    
 

### Authenticate against Marketplace services using OAuth
All Marketplace services now support OAuth as an authentication method. When authenticating using OAuth, you must provide a valid Access Token on the request as part of the Authorization header. The value of the Authorization header must be "Bearer " + access token.

An example of a request with an OAuth access token is shown below.

   
    GET /Data.ashx/WeatherBug/HistoricalObservations/HistHilo?$filter=Station_ID%20eq%20'46005' HTTP/1.1
    Host: api.datamarket.azure.com
    Connection: keep-alive
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=812d5dea-1111-43c0-b2af-38cbe4d58bf8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fpermissions=10a6465f-b0a6-49ca-9175-b24caaf74db0&http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2009%2f09%2fidentity%2fclaims%2factor=myapp&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=DataMarketIdentityProvider&Audience=https%3a%2f%2fapi.datamarket.azure.com&ExpiresOn=1303325933&Issuer=https%3a%2f%2fdatamarket.accesscontrol.windows.net%2f&HMACSHA256=YWSfH6Byumh7HqI4j7U8dsXFD88f42irvNVtGdG8zCY%3d
    User-Agent: Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US) AppleWebKit/534.16 (KHTML, like Gecko) Chrome/10.0.648.204 Safari/534.16
    Accept: application/atomsvc+xml;q=0.8, application/json;q=0.5, */*;q=0.1
    Accept-Encoding: gzip,deflate,sdch
    Accept-Language: en-US,en;q=0.8
    Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3
    
 

If you are using JSON/P capabilities, you can also include the access token in the query string parameter accessToken with the prefix "Bearer ". For more information **on JSON/P support see the topic JSON/P support for Marketplace services.**

   
    <html>
    <body>
    
    <script type="text/javascript">
    function ondataready(data) {
    alert(data);
    }
    </script>
    
    <script type="text/javascript" src="https://api.datamarket.azure.com/UnitedNations/Demographic/DataSeries?
    $callback=ondataready&$format=json&accesstoken=Bearer%20http%253a%252f%252fschemas.xmlsoap.org%252fws
    %252f2005%252f05%252fidentity%252fclaims%252fnameidentifier%3dbac9e6aa-3e22-4e05-87da-0525283708de%26http%253a%252f
    %252fschemas.microsoft.com%252faccesscontrolservice%252f2010%252f07%252fclaims%252fpermissions%3daccount%26http%253a%252f
    %252fschemas.xmlsoap.org%252fws%252f2009%252f09%252fidentity%252fclaims%252factor%3dembedded_demo%26http%253a%252f
    %252fschemas.microsoft.com%252faccesscontrolservice%252f2010%252f07%252fclaims%252fidentityprovider
    %3dDataMarketIdentityProvider%26Audience%3dhttps%253a%252f%252fapi.datamarket.azure.com%252f%26ExpiresOn
    %3d1329153508%26Issuer%3dhttps%253a%252f%252fdatamarket.accesscontrol.windows.net%252f
    %26HMACSHA256%3dcPBhxF7iLAy4mSQ98D8NYyrthl2QxqLu0aqHuxlCBOU%253d"></script>
    
    </body>
    </html>
    
 

### Use the Refresh Token to obtain a new OAuth Access Token
Since access tokens are only valid for 10 minutes, if your application expects to access the user’s account for longer than this period you must handle token refresh.

See the [OAuth 2.0 spec, section 6](http://tools.ietf.org/html/draft-ietf-oauth-v2-13) for details on how to perform an access token refresh. Note that the same token endpoint is used as for refreshing as was used to exchange the authentication code for an access token. Note also that you must provide scope=https%3a%2f%2fapi.datamarket.azure.com%2f as part of the refresh request.

An example of a request for a new access token is shown below.

#### Note  
The line breaks in the HTTP request body are only for readability and should be removed.
 


   
    Post /v2/OAuth2-13 HTTP/1.1
    Host: datamarket.accesscontrol.windows.net
    Content-Type: application/x-www-form-urlencoded
    
    grant_type=refresh_token&
    client_id=myapp&
    client_secret=mysecret&
    refresh_token=uG%2fQvG8eKagO5NFM2XcnSQ%3d%3d&
    scope=https%3a%2f%2fapi.datamarket.azure.com%2f
    
 

### Kinds of Permission Requests
Once the user has signed in to their Marketplace account the application may request access to all datasets the user subscribes to or to specific datasets. If the application specifies anything other than account wide access it must request authorization and get an access token for each dataset it needs to access. The `x_permissions` parameter in the HTTP request designates either an account wide or a specific dataset access request.

* Account wide access

Access to every dataset the user subscribes to is requested by assigning the value `account` to the `x_permissions` parameter when redirecting to the consent flow. 
Example: `x_permissions=account`


* Specific dataset access

Access to a particular dataset is requested by assigning the relative path of the dataset to the x_permissions parameter. The relative path is the portion of the service root URL that identifies the dataset publisher and dataset name. For example, if the service root URL is `https://datamarket.azure.com/data.ashx/contoso/sales`, the relative path is `contoso/sales`. 
Example: `x_required_offers=contoso/sales`

To find the service root URL


Navigate your browser to the **Marketplace** and sign in.


Click **My Data**.


Find the dataset of interest (if it is not listed you need to subscribe to it). See **Subscribe to a Data Offer for guidance.**


Click **Use** on the right side of the screen.


Scroll down and click the **Details** tab.


Find the **Service root URL** near the top of the page. Copy it down for later use.


* Required dataset access

Rather than limiting the permissions to a specific dataset, an application can require that a user have a particular dataset. This will ensure that the consent flow does not successfully complete unless the user has an active subscription to a dataset. To use this option, provide an offering identifier in the x_required_offers parameter instead of in the x_permissions parameter.


A client-side request always uses code as the request type (`request_type=code`).

### Access the Entire Account
If the application requests access to all datasets the user subscribes to (`x_permissions=account`) the explicit grant screen is presented where the user clicks either **Allow Access** or **Cancel**. 

If the application requires a particular dataset (or datasets) the user may or may not subscribe to all of them. If the user has a subscription to each required dataset the explicit grant screen (see above) is presented where the user clicks either **Allow Access** or **Cancel**. If there are any required datasets that the user is not subscribed to they are given opportunity to subscribe or **Cancel**.

### Access a Specific Dataset or Datasets
The application specifies a specific dataset in the request by giving the x_permissions parameter a specific offer ID in the format `DataOwner/Dataset`. 

If the application requires a particular dataset (or datasets) the user may or may not subscribe to all of them. The application will only have access to a dataset if a user has an existing subscription (unless the application uses the x_required_offers query string parameter).

### Register an Application
For your application to receive an authentication code from the Marketplace it must first be registered with the Marketplace. When you register your application with the Marketplace you are assigned an application ID and secret which are used in the authentication and authorization process.

Application Process

Sign in to the Marketplace.


Navigate your browser to https://datamarket.azure.com/developer/applications. 


Click **Create**.


Enter a unique ID for your application. 
Example: MyGreatApp10

Important  
The ID can only be set when you create a registration and cannot be changed if you edit your registration later on.
 


Enter the name of your application. 
Example: My Great Application v1.0


Enter the application's post consent redirect URI.

The application’s post consent redirect URI is the URL that you want the user’s browser redirected to after the consent flow is completed successfully.U


Click **Save**.



### Appendix
#### Parameters
The OAuth Consent Flow Endpoint supports the following client settable query string parameters.

	Parameter  		Required/Optional  	Description  
	client_id 		Required 			The client ID you registered with the Marketplace.
 
	redirect_uri 	Optional 			If provided, these system validates that this matches the redirect URI pre-registered for this client. If it matches everything except for the query string has the same canonical form.

	If not provided, this value defaults to the pre-registered URI.
 
	response_type 	Required 			The Marketplace only supports code.
 
	x_permissions 	Required 			If account is specified, any access tokens from this consent grant all access to all current and future offers. If an offer identifier is specified, any access tokens from this consent grant are scoped to only access the specified offer. 

	If an offer identifier is specified, any access tokens from this consent grant are scoped to only access the specified offer.
 
	state 			Optional 			An opaque value that is passed between the request and callback.
 
	x_required_offers Optional 			An offer id that uses the same format as the x_permissions parameter. 

	For SU2 the list is limited to one offer.

	If provided, the system ensures that the account has an active subscription to all the offers in the list before returning a successful response.

	The offer included in this list is implicitly included in the x_permissions parameter for determining the scope of the access token.

	Optionally, an offer can be appended with a minimum transaction requirement. If this is provided the system ensures that the account is subscribed to an offer variant a monthly limit equal to or greater than the number specified in this parameter.
 

### x_permissions and x_required_offers Matrix
Matrix of the offer ID and x_required_offers parameters. Whether they are supported and resultant Marketplace behavior.

	x_permissions  			x_required_offers  			Resultant Behavior  
		Null 					Null 						Error
 
		account 				Null 						Explicit grant for entire account.
 
		account 				One offer ID 				Explicit grant for entire account and embedded purchase for offer.
 
		account 				More than one offer ID 		Error
 
		One or more offer IDs 	Null 						Error
 
		Same offer ID as 
		x_required_offers		One offer ID 				Embedded purchase for offer. 
															Only access to purchased offer.
 
		Same offer ID as 
		x_required_offers	 	More than one offer IDs 	Error
 
		Null 					One offer ID 				Embedded purchase for offer. 
															Only access to purchased offer.
 

### Error Messages
Error conditions and messages shown to the user when they are navigated to the consent flow.

	Error Condition  										Message  
	Query string value for response_type is 
	missing or an unsupported value.					   <h1>Bad Request</h1>
														   <p>The application you are using sent a bad request to the Marketplace. Contact your application vendor to report this error.</p>  <p>Parameter <param/> was missing or was an unsupported value.</p>
 
	Query string value for x_required_offers 
	contains offer identifiers that do not exist.			<h1>Bad Request</h1>  
															<p>The application you are using sent a bad request to the Marketplace. Contact your application vendor to report this error.</p>  <p>Offer does not exist: <BadOfferId/></p>
 
	Query string value for client_id is invalid 
	(that is, the client_id is not registered with the 
	Marketplace).											<h1>Bad Request</h1>
															<p>The application you are using sent a bad request to the Marketplace. Contact your application vendor to report this error.</p>  <p>Application not registered: <ClientId/></p>
 
	Query string value for client_id maps to an 
	application that is suspended.							<h1>Bad Request</h1>
															<p>The application you are using sent a bad request to the Marketplace. Contact your application vendor to report this error.</p>  <p>Application is suspended: <ClientId/></p>
 
	Too many x_premissions or x_required_offers 
	entries.												<h1>Bad Request</h1>
															<p>The application you are using sent a bad request to the Marketplace. Contact your application vendor to report this error.</p>  <p>More than 50 identifiers were present for x_permissions or x_required_offers.</p>
 




--------------------------------------------------------------------------------
