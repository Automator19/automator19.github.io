---
layout: post
title: Activating Windows via KMS
category: [Windows]
---

- You will require KMS server if remote servers don't have access to internet for activation
- Change server activation key to GVLK from MS Link then run 
```bat
slmgr.vbs /ipk XXXXX-XXXXX-XXXXX-XXXXX-XXXXX
```
- Check VLMCS DNS record. 
```bat
nslookup -type=srv _vlmcs._tcp
```
- Update KMS server
```bat
slmgr.vbs /skms KMS_server_name_or_IP:1688
```
- Check if KMS server is set 
```bat
slmgr.vbs /dlv
```
- Check Port 
```powershell
Test-NetConnection -ComputerName KMS_server_name_or_IP -Port 1688
```
- Activate Windows
```bat
Slmgr.vbs /ato
```
- Check Activation Status 
```bat
slmgr.vbs /dli
```
	
Note: To supress slmgr output run

```bat
cscript c:\windows\system32\slmgr.vbs
```