---
title: Razl - Comparing Databases
layout: RazlLayout
---

# Razl

## Comparing Sitecore Databases

Once you have two Sitecore connections setup (see Creating a Connection) you can start to compare Sitecore instances.

### Setting up for comparison

To setup Razl for comparison select a connection in the Left Connection dropdown and the Right Connection dropdown. Razl will automatically start loading items from each Sitecore instance in the Content Trees:

![](/Images/Razl/compare1.PNG)

### Comparing Items

As you explorer the Sitecore content tree Razl will automatically load and start to compare items in both trees:

![](/Images/Razl/compare2.PNG)

There are several basic symbols pairs in Razl when comparing an items. Each symbol :


| Symbol | Description |
|---- |---- |
| | **Same** - If no symbols are displayed both sides are considered the same. |
| ![](/Images/Razl/compare3.PNG) | **Different** - This pair are display when the items in each database contain different data in their fields. You can then choose which side to copy all field values from. |
| ![](/Images/Razl/compare4.PNG) <br /> or <br /> ![](/Images/Razl/compare5.PNG) | **Deleted** - This pair are displayed when an item exists in one database but not in the other. The side that contains the item will display the red cross and allow you to remove it, the side that doesn’t contain the icon will display the black arrow and allow you to copy over. |
| ![](/Images/Razl/compare6.PNG) | **Moved** - An item this moved will have this symbol next to is't name: <br /> ![](/Images/Razl/compare7.PNG) <br /> The item that is out of position (i.e. in another location) will be in light grey.  To see where each item exists click on the item itself and use the Field Information panels to see each sides path. |

### Lightning Mode

When you click the Lightning Mode ![](/Images/Razl/LightningMode.PNG) button, Lightning Mode will be toggled on and off. When Lightning Mode is enabled, Razl only compares the revision ID's of the items, making the compare very quick. If the revision ID's are different, then an Item is considered different regardless of your filter settings. Razl is much faster when Lightning mode is enabled because all items in the folder are retrieved at once, and the comparison doesn't look at all fields.

The main disadvantage to Lightning Mode is that your filters are ignored. This means that items may be consdered different even though your filter specification would indicate that they aren't. 

When an item is clicked on in the tree, a full compare of the item is done and filters applied even if lightning mode is enabled. This may cause the item to loose it's difference arrows if your filters exclude the changed fields.

### Deep Compare

A new feature of Razl 5.1 is Deep Compare. This allows all items in a tree to be compared. You can deep compare a folder by right clicking on the item in the tree and choosing **Deep Compare**

![](/Images/razl/DeepCompareMenu.png)

Deep Compare looks at all items under a folder on both sides and shows differences in the change detail view. 

![](/Images/razl/DeepCompareView.png)

Deep Compare will compare all fields or just Revision Id's depending on your Lightning Mode setting. Lightning Mode can be 3-5 times faster when comparing many items.

### Comparing Fields

When you click on an item in the Content Tree Razl will load the fields and information about the item and display the in the Field Information panes. Razl will then show you the individual fields differences, you can then select each fields to move across:

![](/Images/Razl/compare8.PNG)

Fields are grouped together based on the following rules:

* Shared fields
* Language/Unversioned
* Language/Version

The Field Information pane also displays information about an item beneath the "Name" node:

![](/Images/Razl/compare9.PNG)

There are several basic symbols pairs in Razl when comparing fields. Each symbol :

| Symbol | Description |
|---- |---- |
| | **Same** - If no symbols are displayed both sides are considered the same. |
| ![](/Images/Razl/compare3.PNG) | **Different** - This pair are display when the field values don’t match. You can then choose which side to copy the value from. |
| ![](/Images/Razl/compare4.PNG) <br /> or <br /> ![](/Images/Razl/compare5.PNG) | **Deleted**  - This pair are displayed when an field exists in one database but not in the other. The side that contains the item will display the red cross and allow you to remove it, the side that doesn’t contain the icon will display the black arrow and allow you to copy over. |
| ![](/Images/Razl/compare10.PNG) | Block - No action can be performed. This is normally due to a field existing in one instance but not the other instance. |

### Controlling Comparison

By default Razl will compare all the fields on an item and all languages of that item, however it is possible to control which fields and languages are compared by Razl. This can be useful in scenarios where you might want ignore the updated date on an item or certain languages because they aren’t used.

#### Ignoring a Field

Follow the following instructions to ignore a field:

1. Connect to a Sitecore instance
2. Select and item in the Content Tree
3. Using the Field Information pane find the field you wish to ignore
4. Right click on the field and a context menu will appear: <br />  ![](/Images/Razl/compare11.PNG)
5. Click the Ignore Field

When a field is ignored Razl will re-compare all loaded items and the fields name will have a strikethrough:

![](/Images/Razl/compare12.PNG)

#### Unignoring a field

Follow the following instructions to ignore a field:

1. Connect to a Sitecore instance
2. Select and item in the Content Tree
3. Using the Field Information pane find the field you wish to ignore
4. Right click on the field to unignore and a context menu will appear: <br /> ![](/Images/Razl/compare13.PNG)
5. Click the Unignore Field option

#### Ignoring a Language

Follow the following instructions to ignore a language:

1. Connect to a Sitecore instance
2. Select and item in the Content Tree
3. Using the Field Information pane find the language you wish to ignore
4. Right click on the language and a context menu will appear: <br /> ![](/Images/Razl/compare14.PNG)
5. Click the Ignore Field

When a language is ignored Razl will re-compare all loaded items and the language name will have a strikethrough:

 ![](/Images/Razl/compare15.PNG)

#### Unignoring a language

Follow the following instructions to ignore a language:

1. Connect to a Sitecore instance
2. Select and item in the Content Tree
3. Using the Field Information pane find the language you wish to ignore
4. Right click on the language to unignore and a context menu will appear: <br /> ![](/Images/Razl/compare16.PNG)
5. Click the Unignore language option

#### Hiding unchanged fields

The Hide Unchanged Fields ![](/Images/Razl/HideUnchangedFieldsOff.png) button will toggle showing/hiding fields that are different. 

When hide unchanged fields is off ![](/Images/Razl/HideUnchangedFieldsOff.png), the field window will show all fields even if they are the same.

![](/Images/Razl/HideUnchangedFieldsAllFields.png)

If hide unchanged fields is enabled [](/Images/Razl/HideUnchangedFieldsOn.png), the field window will show only fields with differences.

![](/Images/Razl/HideUnchangedFieldsDiffFields.png)


#### Compare Filters Dropdown

When you select to ignore either a field or language it is added to the compare filters dropdown in the toolbar:

![](/Images/Razl/compare17.PNG)

Fields and languages are identified by the different symbols.  By unchecking a field or language you will remove it from the filter and Razl will run the item comparisons again.

#### Filtering Effects

When you a field or language is ignored for comparison it stops the field/language from being compared when determining which symbols to display in the Content Tree. The field and language will still be compared in the Field Information pane when you select an item.

For example the English language is ignored in the image below, notice that the Content Tree shows that the item is the same but when the item is selected Razl shows that the English fields are actually different:

![](/Images/Razl/compare18.PNG)

### Content Tree Context Menu

If you right click on an item in the Content Tree a context menu will appear with the following options:

| Menu Item | Description | 
|-------------------|----| 
| Refresh | Forces Razl to refresh the item data and reload child items. | 
| Deep Compare | Compares all items under the selected item and shows the differences in the Change Details window. | 
| Go To Template | Go to the template the item is based on. | 
| Go To Branch | Go the the branch the item was created from. | 
| Left References | Only appears on the left hand side. Lists all items that reference the selected item. Clicking on an item in the list will take you to that item in the Content Tree | 
| Left Referrers | Only appears on the left hand side. Lists all items that the selected item refers to. Clicking on an item in the list will take you to that item in the Content Tree | 
| Right References | Only appears on the right hand side. Lists all items that reference the selected item. Clicking on an item in the list will take you to that item in the Content Tree | 
| Right Referrers | Only appears on the right hand side. Lists all items that the selected item refers to. Clicking on an item in the list will take you to that item in the Content Tree | 
| Get All From Right | Only appears on the left hand side. Copies all items from the right hand instance to the left hand instance including all children with merger and overwrite options. See Copy All in the Tasks Section. | 
| Get All From Left | Only appears on the right hand side. Copies all items from the left hand instance to the right hand instance including all children with merger and overwrite options. See Copy All in the Tasks Section. | 

