---
title: Razl - History
layout: RazlLayout
---

# Razl

## Using the History View

The history view allows you to review entries in the Sitecore history databases and then navigate to those items in the Content Tree. The Sitecore history database stores a record of items events, for example save, add version, delete and created.

The history engine used by Sitecore may not be turned on by default, if Razl does not display any history items check your Sitecore configuration for the following in the database you are targeting:
  &lt;Engines.HistoryEngine.Storage&gt;
&lt;obj type="Sitecore.Data.$(database).$(database)HistoryStorage, Sitecore.Kernel"&gt;
  &lt;param connectionStringName="$(id)" /&gt;
  &lt;EntryLifeTime&gt;30.00:00:00&lt;/EntryLifeTime&gt;
&lt;/obj&gt;
  &lt;/Engines.HistoryEngine.Storage&gt;

Also notice that the history engine specifies a lifetime to retain this data which by default is 30 days, Razl won’t be able to display any information before this time.

### Opening the History View

To open the history view follows these instructions:

1. Connect to a Sitecore instance
2. Click the history button next to the appropriate connection.

### The History View

When you open the history view you will be presented with the following screen:

![](/Images/Razl/history1.PNG)

This history list appears above the Content Tree and displays the the date and time of the latest entry with the path to the item. Entries made on the same day are grouped under a day separator. To keep the list simple Razl shows only the latest entry for an item, older changes to an item can be seen by hovering over it's entry in the history table:

![](/Images/Razl/history2.PNG)

When you hover over an entry the following information is displayed:

* Date and time of the latest entry
* Path to the item
* List of previous entries with the following information
 * Date and time of entry
 * Action performed
 * User who made the action
 * Language
 * Version

When hovering over an entry you may see "Item history incomplete" at the bottom of the previous entries list:

![](/Images/Razl/history3.PNG)

This is displayed for the following two reasons:

* The history for the item is no longer in the database, i.e. the item is more than 30 days old so some of it's history has been deleted.
* Razl hasn't loaded all the history for that item yet. To reduce the amount of data Razl has to process data is loaded into Razl as you scroll down the list and therefore back in time.

### Navigating to Item

To navigate to an item displayed in the history list click on the desired item and Razl will find the item in the Content Tree.

### Loading More History

Razl does not load the entire history database when you open the history view, instead this data is loaded as you scroll through the history list. When you approach the bottom of the loaded list of item Razl will automatically try to retrieve more data.

If you scroll back to the top of the history list Razl will try to load any new history entries or you can right click on the history list and click the **Get Latest History** option.
