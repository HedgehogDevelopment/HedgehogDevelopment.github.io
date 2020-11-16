---
title: Getting started with Avtor
layout: AvtorLayout
---

<script>
	window.location.replace("https://doc.sitecore.com/users/100/sitecore-experience-platform/en/introduction-to-editing-in-avtor.html");
</script>


## About Avtor ![](/Images/Avtor/Avtor.png)
Avtor adds a new dimension to editing content on Sitecore websites. Before Avtor, making changes to multiple Sitecore items could take many steps. Avtor allows the content editor to choose the fields they are interested in editing and presents them with a view of those fields across all Sitecore items in the content tree. This allows the content editor to quickly review and update those fields.

Avtor can create new content items, but it is best suited to reviewing and updating existing content. This tutorial will show how to quickly get started with Avtor.

## Starting Avtor
Avtor is easily accessible from a number of different places in Sitecore depending on how the content editor works with Sitecore. 

### Starting in the launchpad
Avtor can be found in the Sitecore launch pad located in the same area as the other content editor tools.

![](/Images/Avtor/GettingStarted_LaunchPad.png)

### Starting in the desktop
Avtor can be started directly from the start menu in the Sitecore desktop.

![](/Images/Avtor/GettingStarted_Desktop.png)

### Starting in the content editor
Avtor can also be stated directly from the content editor. This is the preferred way of starting Avtor, since the content editor can easily choose the starting location in the content tree closest to the content they wish to edit using Avtor.

![](/Images/Avtor/GettingStarted_ContentEditor.png)

In the above screenshot, clicking the Avtor icon, will open Avtor at the /content/TDS/Home item. This will save the content editor from browsing to those items within Avtor.

### Starting in the content editor tree
Avtor can also be started by right-clicking on an item in the content editor and selecting the Avtor right-click menu item.

![](/Images/Avtor/GettingStarted_ContentEditorTree.png)
 
<hr/>

## Editing fields in Avtor
The fields being edited by the content editor are selected and managed in Avtor "Field Sets". Field Sets are a collection of fields chosen by the content editor to view and update. The content editor can create as many Field Sets as they need. 

The content editor needs to choose which fields they wish to edit before they can begin to update content items.

### Selecting Fields to edit in Avtor
When the content editor starts Avtor for the first time, they will be presented with an empty Avtor editor pane.

![](/Images/Avtor/GettingStarted_EmptyEditPane.png)
<br/><br/>
The content editor can quickly create their first Field Set by choosing an item from the content tree they wish to edit fields from and clicking on "Add Field Set" in the Home toolbar.

![](/Images/Avtor/GettingStarted_AddFirstFieldSet.png)
<br/><br/>
 This will open the Manage Field Set dialog where the user can select the fields they wish to edit and also a name for the Field Set.

![](/Images/Avtor/GettingStarted_ManageFieldSet.png)
<br/><br/>
The content editor can select a few fields to edit by double clicking on the fields in the left side list. They can also select the field in the left and click on the ![Navigate right](/Images/Avtor/Icon_NavigateRight.png) icon. This will move the selected fields to the right-side list, where the list of fields being edited is kept.

**Please Note**: The fields shown in this example are specific to the Sitecore implementation used for this tutorial. The names of fields in your instance of Sitecore will be different, but should be familiar to the content editor, since they are fields they have been working with in the Sitecore content editor.

![](/Images/Avtor/GettingStarted_SelectedFields.png)
<br/><br/>
Once the fields are selected, the Field Set needs to have a name so the content editor can select these fields to edit again.

![](/Images/Avtor/GettingStarted_NameFieldSet.png)
<br/><br/>
Clicking OK will close the Manage Field Set window.

### Updating items in Sitecore
After creating or selecting an existing Field Set, the user can begin reviewing items in the content tree and making changes.

Users of Avtor will follow all of the same content editor rules they have followed when editing individual items in the content tree. They have the same permissions and need to follow the same workflow as they normally would. The Advantage to Avtor is they can perform these operations on many items at once.

Here is an Avtor edit pane where a few fields have been added to a Field Set.

![](/Images/Avtor/GettingStarted_EditFields.png)
<br/><br/>
The fields in this screenshot are "read-only" because the items have not been locked for editing by the current user. If the current user already has items locked for editing, they will be immediately editable. To lock an item for editing, the user needs to click the ![](/Images/Avtor/Icon_EditInWorkflow.png) icon to start editing the item. This icon is located in the "Version" column.

![](/Images/Avtor/GettingStarted_StartEditing.png)
<br/><br/>
The content editor can click on any of the editable fields in the Avtor edit pane and begin updating the fields. As the fields are changed, they are highlighted so the user can track which fields have been edited. The screenshot below shows how the pane would look after a few fields have been updated.

![](/Images/Avtor/GettingStarted_EditedFields.png)
<br/><br/>
If the user makes a mistake editing a field, they can click the "Undo" icon at the top left of the field container. This will undo their changes.

![](/Images/Avtor/GettingStarted_EditedFieldsUndo.png)
<br/><br/>
Once the user has completed editing of the items in the tree, the user can click the "Save" button at the top left of the screen to save all changes to Sitecore.

![](/Images/Avtor/GettingStarted_StartEditingSave.png)
<br/><br/>
After saving the item, the user can check the item back into Sitecore by clicking the ![](/Images/Avtor/Icon_Check.png) icon. This will allow the item to be updated by other users and/or published.

![](/Images/Avtor/GettingStarted_CheckIn.png)
<br/><br/>
<hr/>

## Going further
This tutorial shows the content editor how to get started with Avtor. There are many other features of the tool like:

- Workflow
- Automatic check-in
- Item buckets
- Export to Excel
- Import from Excel
- Search for items

Please see our documentation topics for additional information on these features.
