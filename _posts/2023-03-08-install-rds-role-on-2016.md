---
layout: post
title: Installing RDS role on server 2016 (License and session host)
category: [Windows]
---

**For both Per Device and Per User CALs issuance to work, the RD Session Host and RD Licensing server in any one of the following three configurations:**
- Both in the same workgroup
- Both in the same domain
- Both in the trusted (Two-way trust) Active Directory Domains or Forest

**Firewall Ports Required**
- Ports: ICMP, TCP 135, TCP 139, TCP 445, UDP 137-138, TCP 49152 - 65535

## Install and Configure TS License Role (dedicated server)
```powershell
add-windowsfeature RDS-Licensing
add-windowsfeature RDS-Licensing-UI
```
## Activate Licensing server

1. Select Tools --> Remote Desktop Services --> Remote Desktop Licensing Manager--> Server --> Activate Server
2. Select " Automatic Connection " Connection Method. ( May need to change to different method if activation fails)
3. Complete the Installation "DO NOT START INSTALL LICENSES WIZARD" now
4. Right Click on Server and select "Review Configurations"
5. Make sure both option are green ( if not change scope to Domain)

## Install Licenses
 1. From Remote Desktop Licensing Manager , Right Click on the Server and Select " Install Licenses"
 2. Select Licensing Program and Number of CALs and Complete the wizard

## Configure RD Session Host server 

- This is the server which require more than 2 concurrent user logins
```powershell
add-windowsfeature RDS-Connection-Broker
add-windowsfeature RDS-RD-Server
add-windowsfeature RSAT-RDS-Licensing-diagnosis-ui
```
- Reboot the server.

## Configure License server 
```powershell
$obj = gwmi -namespace "Root/CIMV2/TerminalServices" Win32_TerminalServiceSetting
$obj.ChangeMode(4)
$obj.SetSpecifiedLicenseServerList("SSALS001.argon.local")
# Mode 4 is Per User License and Mode 2 is per device License
# Verify Changes 
$obj.GetSpecifiedLicenseServerList()
```
