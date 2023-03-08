---
layout: post
title: SSO and SAML explained
category: [Windows, Linux]
---

**SSO Analogy**

When you are attending a weeding, You will probably have to show your invitation card at the gate for the entry. Meaning authentication is successfully for the entry, Now what if you have to authenticate again at the food counter or to get drinks. This becomes irritating as you have to provie who you are again. 

This is where SSO comes handy where security person will check your invitation (username and password)  and gives you a token ( like a wrist band or a stamp ) which validates that your identity has been proven. Then you can access all services without reauthenticating. 

# What is SAML ? 
Security Assertion Markup Language is an open standard for exchanging authentication and authorization data between Identity Provider and Service Provider.
SAML is an XML based markup language for security assertions (statements that service providers use to make access-control-decisions)

- The Process
  
  There are 3 parties involved in the process
	1. The user
	2. Service Provider (SP)
	3. Identity Provider (IDP)
	
The user will initiate the request , which will be directed to service provider. 
However SP needs to know if the user is legitimate or not. 
Then user will be redirected to IDP for authentication. 

## Diagram

![saml-auth-process](/assets/images/saml-auth-process.jpg)