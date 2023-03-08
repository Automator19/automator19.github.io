---
layout: post
title: UPN and SPN explained
category: [Windows]
---

- Kerberos defines two different type of accounts ( or Principals). The two different names given to these types of account are 
  
  1. User Principal Name (UPN)
  2. Service Principal Name (SPN)

- We would typically relate these types to Active Directory Users (UPN) and Computers (SPN)
- UPN is assigned to a User . This unique across the forest
- SPN is assigned to a user or a computer. This is unique across the forest
- SPN define what services run under the accounts security context.
	- SPN records for computers gets created when it is joined to the domain. 
- A common example of delegation is the WEB BROWSER-to-IIS-to-SQL-Server
- In this scenario user navigates to a web based reports server hosted on Microsoft IIS
- The IIS Server need to authenticate to a SQL server on behalf of the end user.
- Through Kerberos delegation, The IIS server ( Front end web server ) can request a service ticket for any service (backend) on behalf of the user. e.g SQLserver, Fil Server or a web service.

- Using Constrained delegation , You can limit the IIS Server so that it can authenticate user only to a SQL server and no other backend services.

## Useful commands

- How to ADD SPN ? 
```powershell
Setspn -s "service\hostname: Port" "domain\Service account"
```
- How to Remove SPN ? 
```powershell
Setspn -D "service\hostname: port" "domain\service account
```
- How to view SPN ? 
```powershell
Setspn -L "domain\service account
```
- How to view SPN for a computer ? 
```powershell
setspn -l "computername"
```



