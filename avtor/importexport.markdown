---
title: Editing items with Avtor
layout: AvtorLayout
---

# Importing and Exporting items
Avtor allows the content editor to export their fields to Excel. This allows the content editor to perform much more sophisticated analysis of their content than Avtor provides. One of the unique features of Avtor is the ability to import exported data back into Sitecore. This offers the content editor very powerful editing and analysis tools.

## Exporting items
Avtor allows the content editor to export items from their Sitecore content tree. When exporting items, Avtor will start at the item in the top of the Avtor content tree find all items the content editor has access to. This can create very large exports if the content editor starts Avtor at the top of all content. When exporting items from Avtor, it is a good practice to open Avtor as the top of the items the user wants to export. For more information on opening Avtor at a specific location, please see [Starting in the Content Editor](/avtor/gettingstarted.html#starting-in-the-content-editor).

Avtor only exports field values from the current Field Set. This allows the content editor to limit the fields in the export to the ones they are interested in.

Once Avtor has been opened at the appropriate export location and the appropriate Field Set is selected, click on the Export Items ribbon button and choose the desired options from the Export Items dialog.

![Export Items Ribbon](/Images/Avtor/ImportExport_ExportItemsRibbon.png)

Clicking this button will open the Export Dialog:

![Export Items Dialog](/Images/Avtor/ImportExport_ExportItemsDialog.png)

Avtor offers a number of options for the user when exporting items from Sitecore. The following section explains the options available in the Export Items dialog.

- **Export Language**: The content editor can choose to export item values from one or more languages in their Sitecore database. 
- **Only export items with fields in the Field Set**: Checking this check box will reduce the number of items exported by only exporting items with at least one field in the Field Set with a value. When exporting items in an Item Bucket, this option will remove the Sitecore items used to create the internal structure of the Item Bucket.
- **Include latest publishable version in export**: Avtor will export the most recent version of an item. In some cases, the content editor may wish to compare the values of an item with the values being used on the public facing website. If this check box is selected, Avtor will determine if an older version of the item is currently published and will include that older version in the export.
- **Additional Columns**: Avtor can include additional columns in the export to help the content editor edit the item. These additional columns are:
	- **Display Name**: The Sitecore display name. This is the name shown to the editor in the content tree. It may be different than the actual name of the item.
    - **Template Name**: This is the name of the Sitecore items Template.
    - **Statistics**: 4 columns containing the Sitecore login name of the creator, the person who last modified the item, the create date and last modification date.
	- **Publishable**: A yes/no value indicating if the version of the item in the export is publishable.
	- **Workflow State**: The name of the current workflow state for the item.
    - **Preview Url**: A url the content editor can use to preview the page. To use this url, the user must be logged in to Sitecore and have access to the items that make up the page.
    - **Edit Url**: A url the content editor can use to open the page in the experience editor. To use this url, the user must be logged in to Sitecore and have access to the items that make up the page.
- **File Format**: The user can choose what format to use when generating the file. Please see below for details on each of the formats.

### Export items as CSV
Avtor can generate an export using the CSV or Comma Separated Values format. This format is a text file where the first line contains column names separated by commas followed by a single line for each item with the values of each field seperated by commas.

This format is relatively primitive and is not importable back into Avtor. It is easily opened in Excel or other spreadsheet programs, but doesn't handle complex types like Rich Text fields or link fields very well.

Here is an example of opening an exported CSV in Excel:

![Excel CSV](/Images/Avtor/ImportExport_ExcelCSV.png)

With a few simple clicks, the items can be cleaned up into a useful report:

![Excel CSV Clean](/Images/Avtor/ImportExport_ExcelCSVClean.png)

### Export items as XML
Avtor can export items as an XML or Extensible Markup Language file. For more information on the XML specification, please see this [Wikipedia article](https://en.wikipedia.org/wiki/XML).

Avtor allows XML files to be imported back into Sitecore because the robust nature of XML allows field values to be associated together as Items. This is very important for ensuring the accuracy of the items when importing them back into Sitecore.

### Using Exported XML data in Excel
Using the Exported XML data in Excel isn't as easy as using the CSV data described above. A few additional steps are required to allow Excel to accurately read and edit the XML file.

To use the Exported XML file in Excel, perform the following steps:

1. Save the exported file to a folder on your computer.
2. Open Excel
3. Use Excel to open a workbook by browsing to the Export file in excel. The default name is **ItemExport.Xml**
4. Excel will present a dialog similar to this: <br/>![Excel Open XML](/Images/Avtor/ImportExport_ExcelOpenXML.png)<br/><br/>
5. Choose "As an XML Table" and click OK.
6. Excel will open the spreadsheet. 

The first 3 columns in the spreadsheet contains values Avtor uses to import the items back into Sitecore, and those values must remain associated with the field values in the spreadsheet. The first 3 columns may be hidden, but may not be removed if you wish to import the field values back into Sitecore.

![Excel XML](/Images/Avtor/ImportExport_ExceXML.png)

To import items, you must save the Excel spreadsheet as an XML file. This is done using the Save As function in Excel and choosing "XML Data" in the SAve as type dropdown on the Save As dialog.

![Excel Save XML](/Images/Avtor/ImportExport_ExcelSaveXML.png)

## Importing items
Avtor can import items from an 

