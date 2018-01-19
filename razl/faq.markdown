---
title: Razl - Comparing Databases
layout: RazlLayout
---

# Razl

## FAQ

**How do I change the Access Guid used by the Razl Application?**

> Razl uses an Guid to act as the authentication token between the Razl application and the Razl web service. You will need this Guid
for script mode or if you are using Razl on multiple machines to connect to a single Sitecore instance. To find the Access Guid 
browse to **C:\Users\{username}\AppData\Local\Hedgehog_Development\Razl.exe_Url_????** and open the 
**user.config** file. You will find your connections in this file and the Access Guids they are using. Before altering
any values in this file ensure that Razl is NOT running.
