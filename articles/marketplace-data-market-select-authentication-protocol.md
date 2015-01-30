<properties 
   pageTitle="Select an Authentication Protocol" 
   description="How to select an authentication protocol for an Azure data service" 
   services="service-name" 
   documentationCenter="dev-center-name" 
   authors="kevinscharpenberg" 
   manager="manager-alias" 
   editor=""/>

<tags
   ms.service="required"
   ms.devlang="may be required"
   ms.topic="article"
   ms.tgt_pltfrm="may be required"
   ms.workload="required" 
   ms.date="01/29/2015"
   ms.author="kevsch"/>

Create an application and market it to a wide and growing consumer base on the Marketplace. Whether or not your application consumes Marketplace data, you can be a member of the community that leverages the Marketplace to sell your applications. The Marketplace does the provisioning and billing, leaving you to reap the rewards. If your application consumes Marketplace data, the user must be authenticated and authorized to access the datasets.

The Windows Azure Marketplace (WAM) supports two authentication protocols, HTTP Basic Authentication and OAuth. Deciding which protocol to use is a matter of determining who uses your application and how it is used.
 

## Select anNP Authentication Protocol

Both HTTP Basic Authentication and OAuth authentication are able authenticate a user and, as appropriate, either grant or deny access to a protected resource. 

If you answer these questions for your application, you can determine which is better to use:

  * Will I sell this application on the Marketplace?

  * Will the user access one or more Marketplace datasets?

If you answered “Yes” to either or both of these questions, OAuth is the required authentication protocol.

## HTTP Basic Authentication
The Marketplace implementation of HTTP Basic Authentication ignores the user id and only requires that a valid secret account key as a password. You can ignore the user id, or if you want to manage usage and billing on your own, you can use it to identify specific users. If your application uses HTTP Basic Authentication protocol to access the Marketplace:

  * All access is through a single account. 

  * All users share and use a single password (the Marketplace account key). 
Whether the account key is included in the code or entered by the user, the account key less private and secret. Thus it can introduce vulnerabilities to abuse.

  * The Marketplace bills all access to a single account – the owner of the account key – probably you.

  * Removing access for one user (by changing the account key) removes access for all users.

  * Only datasets subscribed to by the account key owner are available to users.

  * If you want individual users to pay for their usage you must manage their individual use and bill them.


**See Implement HTTP Basic Auth in your Marketplace App.**

## OAuth
The Marketplace implementation of OAuth leverages the user’s Windows Live ID and password and the application’s registration key (client_id) to authenticate and grant access to datasets. Using OAuth provides some additional security benefits, such as the ability to authenticate the client and user and issue an access token directly to the client without potentially exposing it to others, including the resource owner. 

If your application uses the OAuth protocol to access the Marketplace:

  * The application must be registered with the Marketplace.

  * Each user must have a Windows Live ID.

  * All access is through the user’s individual account. 

  * Billing is to the individual user’s account.

  * Removing access for one user does not affect any other user.
 
  * Any dataset subscribed to by the user is accessible (if the application supports this scenario).
 
  * The Marketplace manages the user’s account and billing.

**See Implement OAuth in your Marketplace App.**

Given the above it is reasonable to ask, “Why would anyone use HTTP Basic Authentication?” There are two reasons: 1) the code required to implement HTTP Basic Authentication is shorter and simpler than the code to implement OAuth, and 2) if you are the only one that is going to use the application, you don’t need the flexibility and complexity of OAuth.
