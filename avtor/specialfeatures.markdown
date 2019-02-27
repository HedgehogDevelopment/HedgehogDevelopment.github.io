---
title: Editing items with Avtor
layout: AvtorLayout
---

# Special Features
Avtor contains a number of features that do not immediately fit in to any of the other broad categories. These features are documented here.

## Character counts
Avtor assists the content editor by optionally showing character counts for text fields. This is very useful for content, like SEO fields, where the number of characters in the content is significant. 

To activate the Avtor character count display, select the "Options" ribbon and enable the "Character Count" check-box.

![Character Count](/Images/Avtor/SpecialFeatures_CharCount.png)
<br/><br/>

Each text field will show the current character count. As the user updates a field, the character count will automatically be updated.

## Gutters
The gutter of content tree in Avtor works exactly the same as the gutter in the Sitecore content editor. The gutter is activated by right clicking on the gutter area to the left of the content tree.

![Gutter](/Images/Avtor/SpecialFeatures_Gutter.png)
<br/><br/>
The user can select any of the gutter widgets in the list and the gutter will be updated.

![Gutter widgets](/Images/Avtor/SpecialFeatures_GutterSelected.png)

## Right-click menus
Avtor supports all of the normal Sitecore right-click menus in the content tree. Each of the right-click menu items function exactly as the content editor would expect from using the Sitecore Content Editor.

![Right click](/Images/Avtor/SpecialFeatures_RightClick.png)
<br/><br/>

Custom right-click menu items will not show up in Avtor because Avtor manages its right click menu separately from the normal Sitecore content editor.

### Item links
Avtor adds additional right click menu options to the default Sitecore content editor menu. These allow the user to find items the current item links to or items linked to the current item. 

The custom item links menu is opened by right clicking on the desired item in the content tree and selecting "Item Links". This opens a fly-out menu containing link options.
<br/><br/>
![Item Links](/Images/Avtor/SpecialFeatures_ItemLinks.png)
<br/><br/>
The menu choices perform the following tasks:

- **Items linked to this** - Highlight items in the content tree with links to the selected item.
- **Items this links to** - Highlight items in the content tree the current item has links to. 

The links could be links from any link field, data source or links in rich text fields.

The following is an example of items the home page links to:

![Home Links](/Images/Avtor/SpecialFeatures_HomeLinks.png)
<br/><br/>

This example shows that /Avtor-Beta and /Free-Trial are linked from the home page. Also, there is a link under /Download since it has the ![Child Result](/Images/Avtor/Icon_ChildResults.png) icon.

## Check in on save
Avtor can also automatically check in an item when it is saved. This is enabled by activating the "Check-in on save" check-box in the options ribbon.

![Check in on save](/Images/Avtor/SpecialFeatures_CheckInOnSave.png)

When selected, Avtor automatically checks in an item the content editor has updated and has checked out.
