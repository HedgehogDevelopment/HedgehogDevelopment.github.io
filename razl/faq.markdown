---
title: Razl - Comparing Databases
layout: RazlLayout
---

# Razl

## FAQ

<dl>
	<dt>
		How do I change the Access Guid?
	<dt>
	<dd>
		Razl uses an Guid to act as the authentication token between the Razl application and the Razl web service. You will need this Guid
		for script mode or if you are using Razl on multiple machines to connect to a single Sitecore instance. To find the Access Guid 
		browse to <strong>C:\Users\{username}\AppData\Local\Hedgehog_Development\Razl.exe_Url_????</strong> and open the 
		<strong>user.config</strong> file. You will find your connections in this file and the Access Guids they are using. Before altering
		any values in this file ensure that Razl is NOT running.
	</dd>
</dl>