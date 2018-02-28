---
title: Razl - History
layout: RazlLayout
---

# Razl

## Using the History View

The history view allows you to review entries in the Sitecore history databases and then navigate to those items in the Content Tree. The Sitecore history database stores a record of items events, for example save, add version, delete and created.

The history engine used by Sitecore may not be turned on by default, if Razl does not display any history items check your Sitecore configuration for the following in the database you are targeting:

	  <Engines.HistoryEngine.Storage>
		<obj type="Sitecore.Data.$(database).$(database)HistoryStorage, Sitecore.Kernel">
		  <param connectionStringName="$(id)" />
		  <EntryLifeTime>30.00:00:00</EntryLifeTime>
		</obj>
	  </Engines.HistoryEngine.Storage>

Also notice that the history engine specifies a lifetime to retain this data which by default is 30 days, Razl won’t be able to display any information before this time.

### Opening the History View

To open the history view follows these instructions:

1. Connect to a Sitecore instance
2. Click the history button next to the appropriate connection.

### The History View

When you open the history view you will be presented with the following screen:

![](/Images/Razl-V4/history1.png)

This history list appears above the Content Tree and displays the the date and time of the latest entry with the path to the item and the available move operations. Entries made on the same day are grouped under a day separator. To keep the list simple Razl shows only the latest entry for an item if the item is different between the two Sitecore databases.

You may click on one of the operations in the history view to add the operation to the task list. Clicking on the task icon in the History Change Detail view is the same as clicking on the task icon in the compare window.

The performance of the History Change Detail window may be improved by selecting Lightning Mode. This works the same way as Lightning Mode when comparing items.

### Navigating to an Item

To navigate to an item displayed in the history list double click on the desired item and Razl will find the item in the Content Tree.

### Loading More History

Razl does not load the entire history database when you open the history view, instead this data is loaded as you scroll through the history list. When you approach the bottom of the loaded list of item Razl will automatically try to retrieve more data.

If you scroll back to the top of the history list Razl will try to load any new history entries or you can right click on the history list and click the **Get Latest History** option.

### Exporting history changes
If you want a list of items in the history window, you can right click on the any item in the history list and select **Export changes to .csv file**. This will open a save dialog, allowing you to specify the location and name of the exporeted item list.

![](/Images/Razl-V4/HistoryExport.png)

The export will contain the item path, compare state, item id, left and right server names and the change date.
