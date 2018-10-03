---
title: Editing items with Avtor
layout: AvtorLayout
---

# Editing items with Avtor
Avtor is a very powerful tool for creating and editing Sitecore items. Like every tool, it is designed for specific uses, and using it inappropriately will lead to an unsatisfactory user experience.

## When to use Avtor
Avtor is designed to allow the user to update a small number of fields on a large number of content items at once. Avtor is very good at creating and updating parts of content items where there isn't a need to adjust the presentation of the page in the Experience Editor. Examples of this are large amounts of editorial content, SEO, meta-data for social media and pages that follow a predefined template. Essentially, anytime the user finds themselves clicking from item to item in the content editor to review and/or update the same fields, Avtor is the perfect tool for the job.

This means it may not be the best tool to create lots of new pages if the new pages require large amounts of customization in the Experience Editor, or if the new pages have much of their content spread across multiple data items. Once the pages are created, Avtor can be used to quickly review and update the content.

## The Avtor editor
The Avtor editor is designed to look familiar to any Sitecore user, while offering powerful new functionality. The image below shows a typical Avtor editor screen.

![](/Images/Avtor/EditingItems_AvtorEditor.png)

The top portion of the screen is a standard Sitecore ribbon bar. The functionality of the components on this bar are explained in other parts of this documentation.

The left 1/4 of the screen is the Sitecore content tree. This should be familiar to any content editor and behaves exactly as the content tree in the Sitecore Content Editor tool. One of the features of Avtor is to allow the user to start editing the content tree at a location that is convenient for their task. This means that the content tree doesn't have to start at the root /Sitecore node. This saves space on the screen and allows the user to get to the items they are interested in more quickly.

The right 3/4 of the screen contains the fields the user is editing. Each field has the same editing interface and rules found in the Sitecore content editor. This includes user security rules and work flow, making the field editing experience exactly the same as the user is familiar with.

The actual fields on the example screen will be different, since each Sitecore implementation is unique. To find out how to choose fields to edit, see the [getting started](./gettingstarted.html#selecting-fields-to-edit-in-avtor) guide or [managing field sets]() for more information.

### Editing fields
Avtor implements all of the same security work flow rules as the Sitecore content editor, so the user needs to follow a similar work flow to edit an item.

If the user is a content editor, they may be presented with a screen similar to the one above depending on their permissions and the status of the items. In this example, we are starting with a locked item, and the user will check out the item and update a few fields.

A locked item looks like:

![Locked Item](/Images/Avtor/EditingItems_LockedRow.png)

The column next to the content tree shows the version number of the current item and any item actions the user can perform on the item. Depending on the item state and user permissions, these may be check-out, check-in or add new version. The user may also use the version drop-down to select a different version for the item.

If the user clicks on the row, it will be selected and look like:

![Selected Row](/Images/Avtor/EditingItems_SelectedRow.png)

This allows the user to easily see which fields are associated with which item in the content tree.

Since the row is locked, the fields are read only, and are shown as grayed out. Clicking on the ![](/Images/Avtor/Icon_EditInWorkflow.png) icon in the version column will check out the item to the current user.

![Checkout Row](/Images/Avtor/EditingItems_CheckoutRow.png)

Once the row is checked out, we can see the version number has been incremented, as expected, and the ![](/Images/Avtor/Icon_EditInWorkflow.png) icon hash changed to a ![](/Images/Avtor/Icon_Check.png), which allows the user to check-in the item when they have finished editing it.

The user can now click on any of the fields and update its value. When a field is updated, it will look like:

![Updated Field](/Images/Avtor/EditingItems_UpdatedField.png)

There are two changes to the field in the field edit area. The first is the outline of the field indicates it has been edited. An "Undo" ![Undo](/Images/Avtor/Icon_Undo.png) icon has been added to the top left. The icon is small, but if you mouse over it, it will grow to a more appropriate size.

Clicking the Undo icon will revert the change to the current value in the database. This will allow you to undo any changes you may have made in error.

The user can continue to edit any items on the screen. Expanding the item in the content tree will expose more items for the user to edit.

Once the user has completed their changes, clicking the "Save" ![Save](/Images/Avtor/Icon_Save.png) icon will write their changes back to the Sitecore database.

