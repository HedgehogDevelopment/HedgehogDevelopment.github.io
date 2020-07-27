---
title: Sitecore Razl - Advanced Scripts
layout: RazlLayout
---

## Sitecore Razl Advanced Scripting

The Sitecore Razl scripting engine has been completely re-designed. Sitecore Razl now uses PowerShell to script Razl operations. In most cases, the hig-level Razl script functions will allow developers to accomplish everything they need to. Sitecore Razl offers developers the oppertunity to directly interface with the Sitecore Razl service through PowerShell. This offeres developers the oppertunity to script complex migration scenarios using Powershell.

It is recommended that the developer is familiar with creating connections described in [Sitecore Razl PowerShell Connections](./script.html#sitecore-razl-powershell-connections) before attempting to use any of these Cmdlets.

### Getting Sitecore Item Information 

Sitecore Razl provides the developers with a number of functions used to get items and information about the items from a Sitecore server. The Cmdlets return data structures that can be manipulated by PowerShell script to provide the developer with nearly unlimited flexibility in handling Sitecore items.

#### Get-RazlChildItems
The Get-RazlChildItems Cmdlet queries the Sitecore database for items under an item. The result of the Cmdlet is an array of ItemProperties objects. These objects refer to the items under the item specified by the **-ParentItemID** parameter.

Summary of parameters:
- **-Connection** [Required] - A Razl connection to the Sitecore server.
- **-ParentItemId** [Required] - A Guid or Array of Guids representing the top level items to get child items for.

The resulting ItemProperties object has the following properties:

- **BranchId** - ID of the branch the item was created from (if applicable).
- **Database** - Name of the database that contains the item.
- **HasChildren** - Boolean indicating the item has children.
- **Icon** - Url for the items Icon.
- **Id** - The ID of the item.
- **ItemCRC** - CRC for the item.
- **LastUpdateDate** - Last update date of the item.
- **Name** - The name of the item.
- **ParentId** - ID of the items parent.
- **Path** - Full path of the item.
- **StandardValuesId** - ID of the standard values item in the items - template.
- **TemplateId** - ID of the template of the item.
- **TemplateName** - Friendly name of the template.
- **TemplatePath** - Full path to the template.
- **Version** - The most recent version of the item.

The following is an example of using the Get-RazlChildItems Cmdlet to get items under Home:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	Get-RazlChildItems -Connection $connection -ParentItemID "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}"

#### Get-RazlField
The Get-RazlField Cmdlet gets a FieldData object for a field on an Item on the Sitecore server.

Summary of parameters:
- **-Connection** [Required] - A Razl connection to the Sitecore server.
- **-ItemID** [Required] - The ItemID to get the field for.
- **-FieldId** [Required] - The Field ID to retrieve.
- **-LanguageId** [Optional] - The Language for the field.
- **-VersionNum** [Optional] - The Version for the field.

The Cmdlet returns a FieldData object. The FieldData object has the following properties:

- **Blob** - Boolean indicating if the field is a blob field. The blob value must be retrieved using Get-RazlFieldBlob.
- **Id** - ID of the field.
- **IsShared** - Boolean indicating the field is a shared field.
- **IsUnversioned** - Boolean indicating the field is unversioned.
- **Value** - String value of the field.
- **ValueBytes** - The value of the field expressed as an array of bytes.

The following is an example of using the Get-RazlField Cmdlet to the the Text field on the Home item:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	Get-RazlField -conection $connection -ItemID "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -FieldID "{A60ACD61-A6DB-4182-8329-C957982CEC74}" -LanguageId "en" -VersionNum 1 -verbose

#### Get-GetFieldBlob
The Get-RazlFieldBlob Cmdlet gets the value of a Blob field. The result can be returned as a byte array or stored in a file.

Summary of parameters:
- **-Connection** [Required] - A Razl connection to the Sitecore server.
- **-ItemID** [Required] - The ItemID to get the field for.
- **-FieldId** [Required] - The Field ID to retrieve.
- **-LanguageId** [Optional] - The Language for the field.
- **-VersionNum** [Optional] - The Version for the field.
- **-Filename** [Optional] - File name to store the blob in. If not specified, the blob will be returned as the result of the cmdlet in an array of bytes.

The following is an example of using the Get-RazlFieldBlob Cmdlet to get the Blob field on the Google Plus media item:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	Get-RazlField -conection $connection -ItemID "{A5A23083-C229-47EC-B1BC-445F8BBB55AB}" -FieldID "{40E50ED9-BA07-4702-992E-A912738D32DC}" -verbose

#### Get-RazlItem
The Get-RazlItem Cmdlet gets an ItemDetails object or an array of ItemDetails objects from a server. The ItemDetails object contains all information about an item. This includes all fields for all languages and versions. The ItemDetails object is the object used to copy items between servers.

Summary of parameters:
- **-Connection** [Required] - A Razl connection to the Sitecore server.
- **-ItemID** [Required] - An ItemID or Array of ItemIDd to get the ItemDetails object(s) for.

See [Manipulating ItemDetails](#manipulating-itemdetails) below for the ItemDetails structure.

The following is an example of using the Get-RazlItem cmdlet to get the ItemDetails for the Home item:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	Get-RazlItem -Connection $source -ItemID "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}"


#### Get-RazlReferencedItems
The Get-RazlReferencedItems cmdlet returns an array of ItemProperties objects representing the items referenced by the specified item.

Summary of parameters:
- **-Connection** [Required] - A Razl connection to the Sitecore server.
- **-ItemID** [Required] - The ItemID to get the referenced items for.

The following is an example of using the Get-RazlReferencedItems cmdlet to get the referenced items for the Home item:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	Get-RazlReferencedItems -Connection $source -ItemID "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}"

#### Get-RazlReferredItems
The Get-RazlReferredItems cmdlet returns an array of ItemProperties objects representing the items referring to the specified item.

Summary of parameters:
- **-Connection** [Required] - A Razl connection to the Sitecore server.
- **-ItemID** [Required] - The ItemID to get the items referring to.

The following is an example of using the Get-RazlReferredItems cmdlet to get the items referring to the Home item:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	Get-RazlReferredItems -Connection $source -ItemID "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}"

### Setting Sitecore Item Information
Sitecore Razl offers the developer the ability to update items on a Sitecore server through a number of cmdlets. These cmdlets accept data structures that could be manipulated by the PowerShell script.

#### Set-RazlField
The Set-RazlField cmdlet accepts a FieldData object and uses the information in the FieldData object to update an item on a Sitecore server.

Summary of parameters:
- **-Connection** [Required] - The RazlConnection to a Sitecore server.
- **-ItemId** [Required] - Item to set field information for.
- **-FieldId** [Required] - The Field ID to set.
- **-LanguageId** [Optional] - The Language for the field.
- **-VersionNum** [Optional] - The Version for the field.
- **-FieldData** [Optional] - The FieldData object that contains the information about the field.

The following is an example of using the Set-RazlField cmdlet to update the Text field of the Home item:

	$source = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"
	$target = Get-RazlConnection -SitecoreWebUrl http://target.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Target Sitecore"

	$fieldData = Get-RazlField -Connection $source -ItemID "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -FieldID "{A60ACD61-A6DB-4182-8329-C957982CEC74}" -LanguageId "en" -VersionNum 1 -verbose
	Set-RazlField -Connection $target -ItemID "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -FieldID "{A60ACD61-A6DB-4182-8329-C957982CEC74}" -LanguageId "en" -VersionNum 1 -FieldData $fieldData -verbose

#### Set-RazlFieldBlob
The Set-RazlFieldBlob cmdlet accepts a byte array or filename updates a blob field on an item on a Sitecore server.

Summary of parameters:
- **-Connection** [Required] - The RazlConnection to a Sitecore server.
- **-ItemId** [Required] - Item to set field information for.
- **-FieldId** [Required] - The Field ID to set.
- **-LanguageId** [Optional] - The Language for the field.
- **-VersionNum** [Optional] - The Version for the field.
- **-Filename** [Optional] - The File name to set the blob from. This must be specified if FieldBytes is empty.
- **-FieldBytes** [Optional] - Array of bytes that represents the field blob. If this is empty, a filename must be specified.

The following is an example of using the Set-RazlFieldBlob cmdlet to update the Blob field of the Google Plus media item:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	Set-RazlFieldBlob -Connection $source -ItemID "{A5A23083-C229-47EC-B1BC-445F8BBB55AB}" -FieldID "{40E50ED9-BA07-4702-992E-A912738D32DC}" -FieldBytes $bytes -verbose

#### Set-RazlItem
The Set-RazlItem cmdlet pushes an ItemDetails object or an array of ItemDetails objects to a server. This allows the PowerShell script to update multiple items on the target server with a single command.

Summary of parameters:
- **-Connection** [Required] - The RazlConnection to a Sitecore server.
- **-ItemDetails** [Required] - The ItemDetails object(s) to send to a server.

See [Manipulating ItemDetails](#manipulating-itemdetails) below for the ItemDetails structure.

The following is an example of using Set-RazlItem to copy the Home item from the source server to the target server:

	$source = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"
	$target = Get-RazlConnection -SitecoreWebUrl http://target.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Target Sitecore"

	$itemDetails = Get-RazlItem -Connection $source -ItemID "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -verbose
	Set-RazlItem -Connection $target -ItemDetails $itemDetails -verbose

#### Set-RazlItemTemplate
The Set-RazlItemTemplate updates the Template ID of the item specified by the ItemID on the server.

Summary of parameters:
- **-Connection** [Required] - The RazlConnection to a Sitecore server.
- **-ItemId** [Required] - Item to update the TemplateID for.
- **-TemplateId** [Required] - New Template ID for the item.

The following is an example of using Set-RazlItemTemplate to update the Template Id of the Home item:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	Set-RazlItemTemplate -ItemID "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -TemplateID "{76036F5E-CBCE-46D1-AF0A-4143F9B557AA}"

### Manipulating Sitecore Items

Sitecore Razl provides some cmdlets to manipulate items on a Sitecore server. 

#### Move-RazlItem
The Move-RazlItem moves a Sitecore item from one location in the content tree to another.

Summary of parameters:
- **-Connection** [Required] - The RazlConnection to a Sitecore server.
- **-ItemId** [Required] - ItemID of the item to move.
- **-NewParentId** [Required] - Item ID of the new parent item

The following is an example of using Move-RazlItem the Home item to the root of the Media Library folder:

	Move-RazlItem -connection $connection -ItemId "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}" -NewParentId "{3D6658D8-A0BF-4E75-B3E2-D050FABCF4E1}"

#### Remove-RazlItem
The Remove-RazlItem removes a Sitecore item from the target server. The item can be moved to the recycle bin or permenantly deleted.

Summary of parameters:
- **-Connection** [Required] - The RazlConnection to a Sitecore server.
- **-ItemId** [Required] - ItemID or ID's of the item to remove.
- **-DoNotRecycle** [Optional Switch] - If present, the item is deleted instead of moved to the recycle bin.

The following is an example of using Remove-RazlItem the Home item from the server:

	Remove-RazlItem -connection $connection -ItemId "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}"

### Querying Sitecore using Razl
Sitecore Razl uses a number of different queries to assist the developer. Those queries have been exposed to PowerShell with the cmdlets below.

#### Get-RazlDeepCompareResults
The Get-RazlDeepCompareResults cmdlet performs the same comparison as the Razl Deep Compare function. It starts at a single Sitecore item and compares the item and all items below it in the content tree. The results are returned as an array of DeepCompareResult objects. These objects can be passed to other PowerShell cmdlets using the pipeline functions.

Summary of parameters:
- **-Source** [Required] - A Razl connection to the source Sitecore server. Items will be compared between this server and the target server.
- **-Target** [Required] - A Razl connection to the source Sitecore server. Items will be compared between this server and the source server.
- **-RootItemId** [Required] - The item to start the comparison between the two servers.
- **-Description** [Optional] - The description shown in progress status messages.

The cmdlet returns an array of DeepCompareResult objects. The DeepCompareResult  object has the following properties:

- **ItemID** - The Guid of the item that is different
- **CompareState** - One of (Different, SourceMissing, TargetMissing, SourceDisconnected, TargetDisconnected, MovedOnTarget, MovedOnSource)
- **Path** - The Sitecore path of the object

The following is an example of comparing everything under the default Home item on two servers.

    Get-RazlDeepCompareResults -source $source -target $target -RootItemId "{110D559F-DEA5-42EA-9C1C-8A5DF7E70EF9}"

#### Get-RazlHistory
The Get-RazlHistory cmdlet returns a list of recent changes to the server. These changes are determined by looking at the history table, if enabled, or looking at the updated field on items. The change list can be filtered by date. The results are returned as an array of ChangeHistoryDetails objects.

Summary of parameters:

- **-Connection** [Required] - The RazlConnection to a Sitecore server.    
- **-From** [Optional] - The - DateTime to start getting the history of changes. No changes made before this date will be returned. If not specified, returned changes will start at the oldest avaialble change in the history table.
- **-To** [Optional] - Date time to stop getting the history of changes. No changes made after this date will be returned. If not specified, changes up to the most recent change will be returned.

The cmdlet returns an array of ChangeHistoryDetails objects. The ChangeHistoryDetails  object has the following properties:

- **Action** - The change action. Possible values are (AddedVersion, Copied, Created, Deleted, Moved, Saved, RemovedVersion)
- **Created** - When the change entry was created.
- **ID** - The ID of the changed item.
- **Language** - The language of the changed item.
- **Path** - Sitecore path of the changed item.
- **Username** - The username who made the change.
- **Version** - Version of the changed item.  

The following is an example of getting the history of changes over the last 5 days:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	$last5Days = (Get-Date).AddDays(-5)
	Get-RazlHistory -connection $connection -from $last5Days

#### Search-RazlItems
The Search-RazlItems cmdlet uses the content index of the target Sitecore server to search for items on the server. Found items are returned as an array of ItemProperties.

Summary of parameters:
- **Connection** [Required] - The Sitecore server to search.
- **SearchText** [Required] - The text value to search the content index for.

Please see [Get-RazlChildItems](#get-razlchilditems) for more information about the ItemProperties object.

The following is an example of searching for some text in Sitecore:

	$results = Search-RazlItems -Connection $connection -SearchText "Sitecore Rules!"

### Manipulating ItemDetails
The [Get-RazlItem](#get-razlitem) and [Set-RazlItem](#set-razlitem) cmdlets use the ItemDetails object to get and set items on the server. The ItemDetails object contains all field values for an item along with any known item meta-data. The ItemDetails object can be used to create or update existing items.The ItemDetails object returned by the the Get-RazlItem cmdlet contains everything needed by the Set-ItemDetails cmdlet to update an item on a server.

The Razl scripting library provides a few simple cmdlets to allow the developer to manipulate the ItemDetails object. This allows the developer virtually unlimited flexibility to manipulate Sitecore items. This flexibility facilitates many upgrade/migration scenarios.

#### ItemDetails Object
The ItemDetails object contains the following properties:

- **ItemID** - The Sitecore item ID.
- **Properties** - An ItemProperties structure for item meta-data. Please see below for more information.
- **SharedFields** - An array of FieldInfo objects representing each non-null field in the item.
- **VersionedFields** - An array of FieldInfoVersioned objects representing each version of the item. Please see below for more information.
- **Unversioned** - An array of FieldLanguageInfo objects for each collection of unversioned fields in the object.

The ItemDetails object exposes the following methods:
- **Clone()** - Duplicates the ItemDetails object.
- **FindField(Guid fieldId, string language = null, int? version = null)** - Finds a FieldInfo object in the ItemDetails.

##### FieldInfo Object
The FieldInfo object contains the following properties:

- **Blob** - A boolean indicating the field is a blob field.
- **ID** - The FieldID of the field.
- **IsShared** - A boolean indicating the field is a shared field.
- **IsUnversioned** - A boolean indicating the field is an unversioned field.
- **Language** - The language of the field. Note: This is not set if the field is returned from Get-ItemDetails. This is used when adding fields to an ItemDetails object.
- **Name** - The name of the field.
- **Type** - The Sitecore field type of the field.
- **Version** - The Version of the field.Note: This is not set if the field is returned from Get-ItemDetails. This is used when adding fields to an ItemDetails object.
- **Value** - The string value of the field.
- **ValueBytes** - An array of bytes representing the value of the field.

The FieldInfo object exposes the following methods:
- **Clone()** - Duplicates the FieldInfo object.

##### FieldInfoVersioned Object
The FieldInfoVersioned object holds all field values for all languages for a specific version. The object contains the following properties:

- **Number** - The version number of the fields contained by the object.
- **Languages** - An array of FieldLanguageInfo objects that contain the fields for each language for the version of the object.

The FieldInfoVersioned object exposes the following methods:
- **Clone()** - Duplicates the FieldInfoVersioned object.

##### FieldLanguageInfo Object
The FieldLanguageInfo object holds all field values for a specific language. The object containes the following properties:

- **Name** - The name of the language the object has fields for.
- **DisplayName** - The (long) display name of the language the object has fields for.
- **Fields** - An array of FieldInfo objects representing the non-null fields for the Langugage and Version.

The FieldLanguageInfo object exposes the following methods:
- **Clone()** - Duplicates the FieldInfoVersioned object.

##### ItemProperties Object
The ItemProperties object contains the following properties:

- **BranchId** - ID of the branch the item was created from (if applicable).
- **Database** - Name of the database that contains the item.
- **HasChildren** - Boolean indicating the item has children.
- **Icon** - Url for the items Icon.
- **Id** - The ID of the item.
- **ItemCRC** - CRC for the item.
- **LastUpdateDate** - Last update date of the item.
- **Name** - The name of the item.
- **ParentId** - ID of the items parent.
- **Path** - Full path of the item.
- **StandardValuesId** - ID of the standard values item in the items - template.
- **TemplateId** - ID of the template of the item.
- **TemplateName** - Friendly name of the template.
- **TemplatePath** - Full path to the template.
- **Version** - The most recent version of the item.

#### New-RazlItem
The New-RazlItem cmdlet creates a new ItemDetails object with the specified name, Template, Parent and ID. This object can be passed to Set-RazlItem to create/update an item on a Sitecore server.

Summary of parameters:
- **ItemID** [Optional] - The ID of the item to create or update. If this is omitted, the ID is generated randomly.
- **Name** [Required] - The name of the new Sitecore item.
- **ParentItemID** [Required] - The ID of the parent Sitecore item. The parent item must exist on the Sitecore server when the ItemDetails object is pushed to the server using Set-RazlItem.
- **TemplateID** [Required] - The ID of the items template. The template must exist on the Sitecore server when the ItemDetails object is pushed to the server using Set-RazlItem.

Returns an ItemDetails object. See above for more information about the ItemDetails object.

The following is an example of using the ItemDetails cmdlets to create a new item:

    #Create the new item
    $newItem = New-RazlItem -Name $csvRow."Display Name" -ParentItemID $rootFolderId -TemplateID $csvImportTemplateId

    # Add the fields to the item
    Add-RazlField -ItemDetails $newItem -FieldInfo $(New-RazlField -FieldID $csvTitleField -Value $csvRow.Title -Language "en" -Version 1)
    Add-RazlField -ItemDetails $newItem -FieldInfo $(New-RazlField -FieldID $csvContentField -Value $csvRow.Content -Language "en" -Version 1)

#### New-RazlField
The New-RazlField cmdlet creates a new FieldInfo object with the specified Field ID. 

Summary of parameters:
- **FieldID** [Required] - ID of the field used in the new FieldInfo.
- **Language** [Optional] - The language code for the field. If left blank, the field is assumed to be shared.
- **Value** [Optional] - The string value of the field. If left blank, the field value will be empty.
- **Version** [Optional] - The version number of the field. If left blank, the field is assumed to be unversioned or shared.

Returns a FieldInfo object. See above for more information about the FieldInfo object.

The following is an example of using the ItemDetails cmdlets to create a new item:

    #Create the new item
    $newItem = New-RazlItem -Name $csvRow."Display Name" -ParentItemID $rootFolderId -TemplateID $csvImportTemplateId

    # Add the fields to the item
    Add-RazlField -ItemDetails $newItem -FieldInfo $(New-RazlField -FieldID $csvTitleField -Value $csvRow.Title -Language "en" -Version 1)
    Add-RazlField -ItemDetails $newItem -FieldInfo $(New-RazlField -FieldID $csvContentField -Value $csvRow.Content -Language "en" -Version 1)

#### Add-RazlField
The Add-RazlField cmdlet adds a FieldInfo to an ItemDetails object. The field is added to the correct collection of fields based on the Language and Version of the field. i.e. if Language and Version of the field is null, it's a shared field. If language is "en" and version is 1, the item is added to the VersionedFields collection with a version of 1 and the english language.

Summary of parameters:
- **FieldInfo** [Required] - An array of FieldInfo objects representing the field(s) to add to the ItemDetails.
- **ItemDetails** [Required] - The ItemDetails object that will be updated to contain the new Field(s).

The following is an example of using the ItemDetails cmdlets to create a new item:

    #Create the new item
    $newItem = New-RazlItem -Name $csvRow."Display Name" -ParentItemID $rootFolderId -TemplateID $csvImportTemplateId

    # Add the fields to the item
    Add-RazlField -ItemDetails $newItem -FieldInfo $(New-RazlField -FieldID $csvTitleField -Value $csvRow.Title -Language "en" -Version 1)
    Add-RazlField -ItemDetails $newItem -FieldInfo $(New-RazlField -FieldID $csvContentField -Value $csvRow.Content -Language "en" -Version 1)

#### Remove-RazlField
The Remove-RazlField cmdlet removes a field from an ItemDetails object. It will field the field and remove it based on the search criteria supplied.

Summary of parameters:
- **-FieldID** [Optional] - An array of Guids indicating the FieldID(s) to remove. If this parameter is specified, all fields with the matching ID(s) will be removed.
- **-FieldInfo** [Optional] - An array of FieldInfo object(s) to remove. Only fields matching the FieldID, Version and Language specified in the FieldInfo will be removed.
- **-ItemDetails** [Required] - The ItemDetails object to remove the field from.

### Misc Sitecore Razl CmdLets
The cmdlets in the section provide some functionality used by Razl that could be useful in some scripts, but don't really fit into any specific category.

#### Clear-RazlCache
The Clear-RazlCache cmdlet executes a clear all Sitecore caches on the server. Pleae note: This operation can cause performance degradation of the server while the cache is re-populating, and should be used with care.

Summary of parameters:
- **-Connection** [Required] - A connection to a server.

This is an example of using Clear-RazlCache to clear caches on a server:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	Clear-RazlCache -Connection $connection

#### Get-RazlDatabaseNames
The Get-RazlDatabaseNames cmdlet retrieves an array of strings representing the names of the databases available on the Sitecore server.

Summary of parameters:
- **-Connection** [Required] - A connection to a server.

The result of the cmdlet is an array of strings representing the database names on the server.

This is an example of using Clear-RazlCache to clear caches on a server:

	$connection = Get-RazlConnection -SitecoreWebUrl http://source.sc.local -DatabaseName master -AccessGuid "00000000-1111-2222-3333-444444444444" -Name "Source Sitecore"

	Get-RazlDatabaseNames -Connection $connection


