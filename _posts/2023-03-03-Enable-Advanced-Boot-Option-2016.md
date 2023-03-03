---
layout: post
title: How to Enable advanced boot option for 2016 ?
category: [WINDOWS, OS]
---

Follow these instructions to to enable advanced boot option on Windows VM ruinning on VMWare 

* Get into recovery mode via Automatic repair ( mount installation iso and launch repair )

* Click on Troubleshoot, then Command Prompt

* Run these command :
  
  ```cmd
  bcdedit /set {globasettings} advancedoptions true and bcdedit /set {default} recoveryenabled no
  ```

* Reboot the server. 

* You may get error bcdedit boot config could not be opened, this is due to pvscsi drivers are not loading, fix is below
     * Click on Re-Install Vmtools 
     * CD into CD-ROM drive
     * Browse to  Program Files\Vmware\VMWare Tools\Drivers\pvscsi\Win8\amd64
     * Find pvscsi.inf and type drvload pvscsi.inf 
     * Then run bcdedit commands

**Note:** Remember to revert changes or server will boot into repair every time it reboots. 

**bcdedit /set {globasettings} advancedoptions false**