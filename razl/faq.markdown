---
title: Sitecore Razl - Comparing Databases
layout: RazlLayout
---

## FAQ

**How do I change the Access Guid used by the Sitecore Razl Application?**

> Sitecore Razl uses an Guid to act as the authentication token between the Sitecore Razl application and the Sitecore Razl web service. You will need this Guid
for script mode or if you are using Sitecore Razl on multiple machines to connect to a single Sitecore instance. To find the Access Guid 
browse to **C:\Users\{username}\AppData\Local\Hedgehog_Development\Razl.exe_Url_????** and open the 
**user.config** file. You will find your connections in this file and the Access Guids they are using. Before altering
any values in this file ensure that Sitecore Razl is NOT running.