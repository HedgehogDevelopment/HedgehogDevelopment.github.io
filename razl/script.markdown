---
title: Sitecore Razl - Scripts
layout: RazlLayout
---

## Sitecore Razl Script

The Sitecore Razl scripting engine has been completely re-designed. Sitecore Razl now uses PowerShell to script Razl operations. All operations available in the old scripting engine have been implemented as PowerShell cmdlets. In addtion to the high-level operation cmdlets, Sitecore Razl provides PowerShell cmdlets to perform all low-level operations Sitecore Razl uses. This allows the developer to create very robust scripts to manipulate the Sitecore items as they are copied between servers.

### Sitecore Razl PowerShell Connections

Connections define how Sitecore Razl should connect to a Sitecore instance. The connections are created with a PowerShell Cmdlet and are stored in a variable for later use.

    $sitecoreServer = Get-RazlConnection -SitecoreWebUrl <string> -DatabaseName <string> -AccessGuid <Guid>

This command creates a connection to the server specified by the -SitecoreWebUrl parameter. The connection object is stored in the $sitecoreServer variable and can be used as a parameter for other Sitecore Razl cmdlets.

Summary of Parameters:

- **-SitecoreWebUrl** [Required] - The URL to use to contact the Razl service on the Sitecore server.
- **-DatabaseName** [Required] - The Sitecore database the connection uses when executing commands on the server.
- **-AccessGuid** [Required] - Guid used to access the service installed on the Sitecore server.
- **-SitecoreServerRoot** [Optional] - The UNC Path to the webroot of the Sitecore server. If this is specified, the service will be reinstalled, causing a server recycle.
- **-ReadOnly** [Optional Switch] - The connection is readon only when this switch is present.
- **-Username** [Optional] - The username to use when connecting to the server.
- **-Password** [Optional] - The password to use when connecting to the server.

### Operations
Operations are high-level functions that can be performed on a server or between two servers. Most operations are the same as tasks that can be added to the Task List in the Sitecore Razl UI. The full list of supported operations is:

- **CopyHistory** - Copies items that have changed based on the history of the changes on the source server.
- **CopyItem** - Copy a single item from one server to another.
- **CopyItems** - Copy a tree of items from one server to another.
- **CopyVersion** - Copy all fields in a specific version.

#### CopyHistory Operation

The CopyHistory operation will replay the actions recorded in the Sitecore history engine on one instance on another instance. Razl uses the history engine or the search indexes to determine what has changed on the server. If these features are disabled or modified, the CopyHistory operation may not be able to acurately determine what has changed.

The CopyHistory operation has the following format:

    Copy-RazlItemsUsingHistory -Source <Connection> -Target <Connection> -From <DateTime> -Description <string>

Summary of Parameters:
- **-Source** [Required] - A Razl connection to the source Sitecore server. Items will be copied from this server based on the history of changes.
- **-Target** [Required] - A Razl connection to the target Sitecore server.
- **-From** [Required] - The DateTime to use to start looking for changes on the source server. Any changes before this time will be ignored.
- **-To** [Optional] - The DateTime to use to stop looking for changes. Any changes after this date will not be copied. Leave blank to copy everything up to the present.
- **-IncludePaths** [Optional] - An array of paths to copy items from. Only items under these paths will be copied. If left blank, all item changes will be copied.
- **-ExcludePaths** [Optional] - An array of paths to NOT copy items from. If left blank, all item changes will be copied.
- **-LightningMode** [Optional Switch] - If specified, perform a fast compare instead of a field-by-field compare of items to copy.
- **-PermanentlyDelete** [Optional Switch] - If specified, permantely delete items if the history change specifies an item should be deleted. Otherwise, items will be moved to the recycle bin.
- **-ContinueOnError** [Optional Switch] - Continue processing history if there are any errors.
- **-Description** [Optional] - The description shown in progress status messages.

The following is an example of using the CopyHistory Cmdlet to move items from the source to target that have changed in the last 5 days:

	$ErrorActionPreference = "Stop"
	$InformationPreference = "Continue"

	$source = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"
	$target = Get-RazlConnection -SitecoreWebUrl http://target.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Target Sitecore"

    $last5Days = (Get-Date).AddDays(-5)
	Copy-RazlItemsUsingHistory -source $source -target $target -from $last5Days -Description "Copy History" -verbose

#### CopyItem Operation

The CopyItem operation will copy an item from the source Sitecore instance to the target Sitecore instance. 

The CopyItem operation has the following format:

	Copy-RazlItem -Source <Connection> -Target <RazlConnection> [-ItemId] <Guid[]>

Summary of Parameters:
- **-Source** [Required] - A Razl connection to the source Sitecore server. Items will be copied from this server based on the history of changes.
- **-Target** [Required] - A Razl connection to the target Sitecore server.
- **-ItemID** [Required] - A single ItemID or an array of ItemID's to copy. This parameter can also use the PowerShell pipeline to get the array of ID's.
- **-Description** [Optional] - The description shown in progress status messages.

The following is an example of using the CopyItem Cmdlet to copy the Home item from the source to target:

	$ErrorActionPreference = "Stop"
	$InformationPreference = "Continue"

	$source = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"
	$target = Get-RazlConnection -SitecoreWebUrl http://target.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Target Sitecore"
    
	Copy-RazlItem -source $source -target $target -ItemId "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -verbose

This Example uses a PowerShell pipeline to copy all items under the home item:

	$ErrorActionPreference = "Stop"
	$InformationPreference = "Continue"

	$source = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"
	$target = Get-RazlConnection -SitecoreWebUrl http://target.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Target Sitecore"

	# Get-RazlChildItems returns an array of ItemProperty objects that contain basic information about each item under the ParentItemID. 
	# In this example, the array is converted into an array of ID's by pipeing it to the select statement.
	# Next, it is sent to the Get-CopyItem Cmdlet to perform the copy.

	Get-RazlChildItems -Connection $source -ParentItemID "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -verbose | `
		select -ExpandProperty Id | `
		Copy-RazlItem -source $source -target $target -verbose


#### CopyAll Operation

The CopyAll operation will copy an item and all child items from the source to the target.

 The CopyAll operation has the following format:

    Copy-RazlItemTree -Source <Connection> -Target <Connection> [-ItemId] <Guid[]> 

Summary of Parameters:
- **-Source** [Required] - A Razl connection to the source Sitecore server. Items will be copied from this server based on the history of changes.
- **-Target** [Required] - A Razl connection to the target Sitecore server.
- **-ItemID** [Required] - A single ItemID or an array of ItemID's to copy. This parameter can also use the PowerShell pipeline to get the array of ID's.
- **-Overwrite** [Optional Switch] -  If present, the entire tree will be overwritten. This means that any items in the target tree that are missing in the source will be removed from the target.
- **-LightningMode** [Optional Switch] - If present, lighting mode compare will be used. This is much faster than comparing every item field by field.
- **-ContinueOnError** [Optional Switch] - If present, Razl will continue to copy items even if an error occurs.
- **-Description** [Optional] - The description shown in progress status messages.


The following is an example of using the CopyAll Cmdlet to copy the Home item and all its children from the source to target:

	$ErrorActionPreference = "Stop"
	$InformationPreference = "Continue"

	$source = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"
	$target = Get-RazlConnection -SitecoreWebUrl http://target.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Target Sitecore"
    
	Copy-RazlItemTree -source $source -target $target -ItemId "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -verbose -Overwrite -LightningMode -ContinueOnError


