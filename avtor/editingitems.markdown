---
title: Editing items with Avtor
layout: AvtorLayout
---

## Editing items with Avtor
Avtor is a very powerful tool for creating and editing Sitecore items. Like every tool, it is designed for specific uses. This document will help content editors understand how to best use Avtor, and how it will make editing Sitecore items easier.

## When to use Avtor
Avtor is designed to allow the content editor to update a small number of fields across the entire content tree. Avtor is very good at creating and updating parts of content items where there isn't a need to adjust the presentation of the page in the Experience Editor. Examples of this are editorial content, SEO, meta-data for social media and pages that have static presentation with dynamic content. Essentially, anytime the user finds themselves clicking from item to item in the content editor to review and/or update the same set of fields on items, Avtor is the perfect tool for the job.

Avtor may not be the best tool to create lots of new pages if the new pages require large amounts of customization in the Experience Editor, or if the new pages have their content spread across multiple data items. Once the pages are created though, Avtor can be used to quickly review and update the content.

## The Avtor editor
The Avtor editor is designed to look familiar to any Sitecore user, while offering powerful new functionality. The image below shows a typical Avtor editor screen.

![](/Images/Avtor/EditingItems_AvtorEditor.png)

The top portion of the screen is a standard Sitecore ribbon bar. The functionality of the components on this bar are explained in other parts of this document.

The left 1/4 of the screen is the Sitecore content tree. This should be familiar to any content editor and behaves exactly the same as the content tree in the Sitecore Content Editor tool. Avtor allows the user to start editing the content tree at a location that is convenient for their task instead of always starting at the Sitecore content root. This leads to a more efficient use of limited screen space and allows the user to get to the items they are working with more quickly.

The right 3/4 of the screen contains the fields the user will be reviewing or updating. Each field has the same editing interface and rules found in the Sitecore Content Editor. This includes security rules and work flow, making the field editing experience exactly the same as the familiar Sitecore Content Editor.

The actual fields on the example screen will be different, since each Sitecore implementation is unique. To find out how to choose fields to edit, see the [getting started](./gettingstarted.html#selecting-fields-to-edit-in-avtor) guide or [managing field sets](./fieldsets.html) for more information.

### Editing fields
Avtor implements all of the same security rules as the Sitecore content editor, so the user needs to follow the same workflow they normally use to edit an item.

If the user is a content editor, they may be presented with a screen similar to the one above. There may be minor differences depending on their permissions and the status of the items. In this example, we are starting with a locked item, and the user will check out the item and update a few fields.

A locked item looks like:

![Locked Item](/Images/Avtor/EditingItems_LockedRow.png)

Note the column next to the content tree. This is the version columns, and it shows the version number of the current item and any item actions the user can perform on the item. Depending on the item state and user permissions, these may be check-out, check-in or add new version. The user may also use the version dropdown to select a different version of the fields for review and editing.

If the user clicks anywhere on the row, it will be selected and look like:

![Selected Row](/Images/Avtor/EditingItems_SelectedRow.png)

This allows the user to easily see which fields are associated with an item in the content tree.

Since the row is locked, the fields for the item are read only, and are shown as grayed out. Clicking on the ![](/Images/Avtor/Icon_EditInWorkflow.png) icon in the version column will check out the item to the current user.

![Checkout Row](/Images/Avtor/EditingItems_CheckoutRow.png)

Once the row is checked out, we can see the version number has been incremented, as expected, and the ![](/Images/Avtor/Icon_EditInWorkflow.png) icon hash changed to a ![](/Images/Avtor/Icon_Check.png), which allows the user to check-in the item when they have finished editing it.

The user can now click on any of the fields and update its value. When a field is updated, it will look like:

![Updated Field](/Images/Avtor/EditingItems_UpdatedField.png)

There are two changes to the presentation of the field in the field edit area after the user edits the field. 

- The edited field gets a bold outline of the to indicate it has been edited.
- An "Undo" ![Undo](/Images/Avtor/Icon_Undo.png) icon has been added to the top left of the edited field. The icon is small, but if you mouse over it, it will grow to a more appropriate size.

The Undo icon allows the user to revert any change they have made to the field before saving it. This will allow you to undo any changes you may have made in error without losing changes to other fields.

Avtor allows the user to edit multiple items at one. The user can also expand items in the content tree to expose more items for the user to edit. After editing each field, it will be highlighted until it is saved.

Once the user has completed their changes, clicking the "Save" ![Save](/Images/Avtor/Icon_Save.png) icon will write their changes back to the Sitecore database.

## Switching Languages
Avtor allows the user to quickly switch between the languages installed on their server. This is done by choosing the new language from the Selected Language dropdown in the Home ribbon.

![Updated Field](/Images/Avtor/EditingItems_SelectLanguage.png)

**Please Note:** You must save any changes made to fields in the Avtor editing pane before switching languages.

## Missing fields
When editing a complex content tree, there may be items missing one or more fields in the field set. This doesn't present a problem for Avtor. The missing fields will simple be rendered without a field in the Avtor field editor.

![Updated Field](/Images/Avtor/EditingItems_MissingFields.png)

In the above image, the "Company" folder does not have any of the fields being edited, and therefore there is no field editor present on the screen.

## Editing more complex field types
Avtor allows a user to edit more than just text fields. Users can edit many of the different types of fields by Sitecore. This includes:

- Rich Text
- Images
- Multi-list
- Links
- Drop-links
- Date/Time
- Check boxes

This is an example of a few of the different types of fields users can edit:

![Other Fields](/Images/Avtor/EditingItems_OtherFields1.png)

This screen shot shows some additional fields by scrolling the edit pane to the left:

![Other Fields](/Images/Avtor/EditingItems_OtherFields2.png)


## Editing fields as an Administrator
In most cases, the content editor shouldn't be an administrator when working on the website. Since administrators occasionally edit content in Sitecore, Avtor is aware of administrator's special capabilities and allows them to edit content as well.

The biggest change for administrators is they do not need to "Check out" a version of the item before editing it. When an administrator is using Avtor, the check-out button is removed and replaced with an "add version" ![Add Version](/Images/Avtor/Icon_Plus.png) button. This allows the administrator to add a new version of the item if needed. Otherwise, the administrator can edit the selected version of the item without checking it out.

![Edit as Administrator](/Images/Avtor/EditingItems_Administrator.png)

Administrators do not need to check-in items after editing, so in most cases, the check-in button will not be present. If an item is locked by someone else, the check-in button will be shown, giving the administrator the opportunity to unlock the item.

![Unlock Item](/Images/Avtor/EditingItems_UnlockItem.png)

## Editing items in a Sitecore workflow
Avtor supports Sitecore workflow by allowing the content editor to see the workflow actions available to the editor on each item in the Avtor editor pane. This option is disabled by default, but can easily be enabled by selecting the Options ribbon and enabling the "Show workflow column" checkbox.

![Enable Workflow](/Images/Avtor/EditingItems_EnableWorkflow.png)

This creates a column in the editor pane called "Workflow on Save", which will show any available workflow actions, and if selected, the action will take place when the items are saved.

![Workflow](/Images/Avtor/EditingItems_Workflow.png)

Only one workflow action may be selected for a given item. If a workflow action is selected in error, the selected workflow action can be deselected before saving, by clicking on the selected workflow again.

If any validation errors occur during saving, the user will be presented with validation error dialogs for each of the items failing validation.