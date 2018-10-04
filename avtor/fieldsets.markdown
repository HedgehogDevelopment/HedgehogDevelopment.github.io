---
title: Editing items with Avtor
layout: AvtorLayout
---

# Field Sets
Avtor uses Field Sets to group a small number of fields together for the editor to review and/or update. The Field Set is named and saved as part of the content editors profile so they can quickly re-select those fields for editing. Avtor makes creating and managing the fields in a Field Set very simple. The user simply selects an item they want to update and all editable fields are presented to the user. They can choose the fields for the fields set and then save the fieldset for future use.

## Creating a Field Set
Before the content editor can begin updating Sitecore content, they must create at least one Field Set. This is done by selecting an item in the content tree having the fields they would like to edit and selecting "Add Field Set". Add Field Set can be found on the ribbon bar or in the right click content menu for an item.

![Add Field Set](/Images/Avtor/FieldSets_AddFieldSet.png)

Selecting either option in the above image will open the Manager Field Set dialog. This is where the user will select the fields for the Field Set and choose a name.

![Empty Field Set Dialog](/Images/Avtor/FieldSets_EmptyFieldSet.png)

In this dialog, the content editor can choose a name for the Field Set and select the fields to edit.

The fields are selected by moving fields from the list on the left side list to the right. This can be done a few different ways.

- Selecting a section name and clicking the Move Right ![Move right](/Images/Avtor/Icon_NavigateRight.png) icon. The section names have a dark background and light text. 
- Selecting a single field and clicking the Move Right ![Move right](/Images/Avtor/Icon_NavigateRight.png) icon.
- Double clicking on a section name.
- Double clicking on a field name.

Any one of these actions will add a field into the list of fields in the Field Set. If the field or fields are already in the Field Set, they will not be added.

The content editor can change the order of fields in the Field Set by selecting a field and using the Move Up ![Move up](/Images/Avtor/Icon_NavigateUp.png) and ![Move down](/Images/Avtor/Icon_NavigateDown.png) Move Down icons on the right side of the dialog.

Fields in the Field Set can be removed by selecting a field and using the Delete Field ![Delete Field](/Images/Avtor/Icon_Delete.png) icon or double clicking on the field in the right side list.

**Please Note:** Avtor allows a maximum of 8 fields in the Field Set. This is done to ensure the best possible editing experience for the user. By limiting the number of fields, we can ensure the browser and server don't get overloaded by the complexities of editing the fields and we can also reduce the amount of scrolling the user needs to perform to view or edit the selected fields. 

### Saving the new Field Set
Before saving the new Field Set, it must be given a name so it can be selected again. The name must be unique, and is entered in the Field Set Name text box at the top of the dialog.

After the Field Set has been named, clicking OK at the bottom of the screen will save the Field Set and select the fields for editing in the Avtor edit pane.

This is an example of the Field Set dialog where OpenGraph fields have been selected and is ready to be saved.

![New Set Dialog](/Images/Avtor/FieldSets_NewFieldSet.png)

### Including System Fields
Avtor Field Sets can also include Sitecore internal fields as fields in the Field Set. These can be shown in the Manage Field Set dialog by checking the "Include system fields in search results" check box. 

## Editing a Field Set
Avtor allows the content editor to add or remove fields from a Field Set. The editing process uses the same dialog as Add Field Set. The dialog is pre-populated with the fields currently in the Field Set.

Editing a Field Set is very similar to Adding a Field Set. The field set is selected, and optionally, an item in the content tree. The user can right-click on an item or use Edit Field Set in the Home ribbon.

![Edit Set Dialog](/Images/Avtor/FieldSets_EditFieldSet.png)

The Manage Field Set dialog will open with the fields in the current item shown on the left side of the dialog and the fields in the Field Set on the right. If no item was selected from the content tree, the left side of the dialog will be left blank and the user can only re-order or remove items from the Field Set.

Editing a Field Set allows the user to add fields from different items for editing.

## Selecting an existing Field Set
Avtor allows the content editor to create as many Field Sets as they need to manage their content. To select an existing FieldSet, the user can choose a Field Set from their list of Field Sets in the Field Set Selector in the Home ribbon.

![Field Set Selector](/Images/Avtor/FieldSets_FieldSetSelector.png)

The content editor can use the arrows to scroll through the field sets, or use the open drop down button to open a larger list of available Field Sets.

![Field Set Selector Dropdown](/Images/Avtor/FieldSets_FieldSetSelectorDropdown.png)

Clicking on one of the Field Sets in the dropdown will select those fields for review/update.

## Copying a Field Set
To copy an existing Field Set, select the Field Set in the Field Set Selector and click the Copy Field Set button in the Home ribbon.

![Copy Field Set](/Images/Avtor/FieldSets_CopyFieldSet.png)

This will open the Manage Field Set dialog, allowing the user to edit the copy of the Field Set before saving the copy.

## Removing a Field Set
To remove a Field Set, select the Field Set in the Field Set Selector and click the Remove button in the Home ribbon.

![Remove Field Set](/Images/Avtor/FieldSets_RemoveFieldSet.png)

This will open a confirmation dialog, verifying the intention to remove the Field Set. Clicking OK, removes the Field Set from the list of Field Sets available to the user.
