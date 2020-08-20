---
title: Sitecore Razl - Scripts
layout: RazlLayout
---

## Sitecore Razl Script

The Sitecore Razl scripting engine has been completely re-designed. Sitecore Razl now uses PowerShell to script Razl operations. All operations available in the old scripting engine have been implemented as PowerShell cmdlets. In addtion to the high-level operation cmdlets, Sitecore Razl provides PowerShell cmdlets to perform all low-level operations Sitecore Razl uses. This allows the developer to create very robust scripts to manipulate the Sitecore items as they are copied between servers.

### Sitecore Razl PowerShell Connections

Connections define how Sitecore Razl should connect to a Sitecore instance. The connections are created with a PowerShell Cmdlet and are stored in a variable for later use.

Summary of Parameters:

- **-SitecoreWebUrl** [Required] - The URL to use to contact the Razl service on the Sitecore server.
- **-DatabaseName** [Required] - The Sitecore database the connection uses when executing commands on the server.
- **-AccessGuid** [Required] - Guid used to access the service installed on the Sitecore server.
- **-SitecoreServerRoot** [Optional] - The UNC Path to the webroot of the Sitecore server. If this is specified, the service will be reinstalled, causing a server recycle.
- **-ReadOnly** [Optional Switch] - The connection is read only when this switch is present.
- **-Username** [Optional] - The username to use when connecting to the server.
- **-Password** [Optional] - The password to use when connecting to the server.
- **-ReadThreads** [Optional] - The number of read threads to use when copying a tree from one server to another.
- **-WriteThreads** [Optional] -The number of write threads to use when copying a tree from one server to another.

The following is an example of creating a connection to Sitecore:

    $sitecoreServer = Get-RazlConnection -SitecoreWebUrl <string> -DatabaseName <string> -AccessGuid <Guid>

This command creates a connection to the server specified by the **-SitecoreWebUrl** parameter. The connection object is stored in the $sitecoreServer variable and can be used as a parameter for other Sitecore Razl cmdlets.

#### Removing a connection

In some cases, there may be a need to remove the connection from the Sitecore server. The cmdlet Remove-RazlConnection is provided to remove the connection from a server. This will remove the Service folder and the Sitecore Razl service assembly from the /bin folder, so it will cause the AppPool to recycle.

Summary of Parameters:
- **-Connection** [Required] - The Razl connection object to remove. Please note: Razl needs to know where the service is located in the file system. Therefore, the connection must be created with the **-SitecoreServerRoot** parameter specified.

Here is an example of removing the connection from an existing connection

	Remove-RazlConnection -Connection $connection

This assumes that $connection contains a properly initialized connection object where the **-SitecoreServerRoot** parameter was specified.

#### Get-RazlConnectionStatus
The Get-RazlConnectionStatus function allows the script to determine if a connection object is available for use.

Summary of Parameters:
- **-Connection** [Required] - A Razl connection onject.

The Get-RazlConnectionStatus returns on of the following values:

Ready, NotInstalled, OldVersion, InvalidAccessGuid, Deactivated,
    NeedCredentials, AccessDenied, ServerNotFound

### Operations
Razl Operations are high-level functions that can be performed on a server or between two servers. Most operations are the same as tasks that can be added to the Task List in the Sitecore Razl UI. The full list of supported operations is:

- **CopyHistory** - Copies items that have changed based on the history of the changes on the source server.
- **CopyItem** - Copy a single item from one server to another.
- **CopyItems** - Copy a tree of items from one server to another.
- **CopyVersion** - Copy all fields in a specific version.

#### Copy-RazlItemsUsingHistory Operation

The Copy-RazlItemsUsingHistory operation will replay the actions recorded in the Sitecore history engine on one instance on another instance. Razl uses the history engine or the search indexes to determine what has changed on the server. If these features are disabled or modified, the Copy-RazlItemsUsingHistory operation may not be able to acurately determine what has changed.

Summary of parameters:
- **-Source** [Required] - A Razl connection to the source Sitecore server. Items will be copied from this server based on the history of changes.
- **-Target** [Required] - A Razl connection to the target Sitecore server.
- **-From** [Required] - The DateTime to use to start looking for changes on the source server. Any changes before this DateTime will be ignored.
- **-To** [Optional] - The DateTime to use to stop looking for changes. Any changes after this DateTime will not be copied. Do not specify this parameter to copy everything up to the present.
- **-IncludePaths** [Optional] - An array of paths to copy items from. Only items under these paths will be copied. If left blank, all item changes will be copied.
- **-ExcludePaths** [Optional] - An array of paths to NOT copy items from. If left blank, all item changes will be copied.
- **-LightningMode** [Optional Switch] - If specified, perform a fast compare instead of a field-by-field compare of items to copy.
- **-PermanentlyDelete** [Optional Switch] - If specified, permantely delete items if the history change specifies an item should be deleted. Otherwise, items will be moved to the recycle bin.
- **-ContinueOnError** [Optional Switch] - Continue processing history if there are any errors.
- **-Description** [Optional] - The description shown in progress status messages.

The following is an example of using the Copy-RazlItemsUsingHistory cmdlet to move items from the source to target that have changed in the last 5 days:

	$ErrorActionPreference = "Stop"
	$InformationPreference = "Continue"

	$source = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"
	$target = Get-RazlConnection -SitecoreWebUrl http://target.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Target Sitecore"

    $last5Days = (Get-Date).AddDays(-5)
	Copy-RazlItemsUsingHistory -source $source -target $target -from $last5Days -Description "Copy History" -verbose

#### Copy-RazlItem Operation

The Copy-RazlItem operation will copy an item from the source Sitecore instance to the target Sitecore instance. 

Summary of Parameters:
- **-Source** [Required] - A Razl connection to the source Sitecore server. Items will be copied from this server based on the history of changes.
- **-Target** [Required] - A Razl connection to the target Sitecore server.
- **-ItemID** [Required] - A single ItemID or an array of ItemID's to copy. This parameter can also use the PowerShell pipeline to get the array of ID's.
- **-Description** [Optional] - The description shown in progress status messages.

The following is an example of using the Copy-RazlItem cmdlet to copy the Home item from the source to target:

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

#### Copy-RazlItemTree Operation

The Copy-RazlItemTree operation will copy an item and all child items from the source to the target.

Summary of Parameters:
- **-Source** [Required] - A Razl connection to the source Sitecore server. Items will be copied from this server based on the history of changes.
- **-Target** [Required] - A Razl connection to the target Sitecore server.
- **-ItemID** [Required] - A single ItemID or an array of ItemID's to copy. This parameter can also use the PowerShell pipeline to get the array of ID's.
- **-Overwrite** [Optional Switch] -  If present, the entire tree will be overwritten. Any items in the target tree that are missing in the source will be removed from the target.
- **-LightningMode** [Optional Switch] - If present, lighting mode compare will be used. This is much faster than comparing every item field by field.
- **-ContinueOnError** [Optional Switch] - If present, Razl will continue to copy items even if an error occurs.
- **-Description** [Optional] - The description shown in progress status messages.

The following is an example of using the Copy-RazlItemTree cmdlet to copy the Home item and all its children from the source to target:

	$ErrorActionPreference = "Stop"
	$InformationPreference = "Continue"

	$source = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"
	$target = Get-RazlConnection -SitecoreWebUrl http://target.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Target Sitecore"
    
	Copy-RazlItemTree -source $source -target $target -ItemId "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -verbose -Overwrite -LightningMode -ContinueOnError

#### Copy-RazlItemVersion Operation

The Copy-RazlItemVersion operation will copy all fields in a specific version from an item on one server to another.

Summary of Parameters:
- **-Source** [Required] - A Razl connection to the source Sitecore server. Items will be copied from this server based on the history of changes.
- **-Target** [Required] - A Razl connection to the target Sitecore server.
- **-ItemID** [Required] - A single ItemID or an array of ItemID's to copy. This parameter can also use the PowerShell pipeline to get the array of ID's.
- **-LanguageId** [Optional] - The LanguageId to copy. If this isn't specified, CopyVersion assumes you are copying the Shared fields.
- **-VersionNum** [Optional] - The Version to copy if copying a verison. If this isn't specified, CopyVersion assumes you are copying the Unversioned or Shared fields based on the presense of the -Language Id parameter.
- **-TargetVersionNum** [Optional] - The Version number on the item on the target server. If this isn't specified, the source version number is used.
- **-TargetLanguageId** [Optional] - The Language on the item on the target server. If this isn't specified, the source language id is used.
- **-RemoveVersion** [Optional Switch] - If specified, the version is removed from the target.
- **-VersionType** [Optional] - Type of versioned item (Shared, Unversioned or [blank]) to copy.
- **-Description** [Optional] - The description shown in progress status messages.

The following is an example of using the CopyVersion Cmdlet to copy version 1 of the Home item from source to target:

	$ErrorActionPreference = "Stop"
	$InformationPreference = "Continue"

	$source = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"
	$target = Get-RazlConnection -SitecoreWebUrl http://target.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Target Sitecore"
    
	Copy-RazlItemVersion -source $source -target $target -ItemId "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -verbose -LanguageId "en" -VersionNum 1


