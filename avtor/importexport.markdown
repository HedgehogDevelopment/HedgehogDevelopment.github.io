---
title: Importing and Exporting items with Avtor
layout: AvtorLayout
---

## Importing and Exporting items
Avtor allows the content editor to export items from Sitecore to an XML or CSV file. These files can be opened in spreadsheet programs like Excel to perform much more sophisticated analysis of Sitecore content than Avtor provides. One of the unique features of Avtor is the ability to import updated export files back into Sitecore. This offers the content editor very powerful editing and analysis tools.

## Exporting items
Avtor allows the content editor to export items from their Sitecore content tree. When exporting items, Avtor will start with the item at the top of the Avtor content tree and find all items the content editor has access to. This can create very large exports if the content editor starts Avtor at the top of all content. When exporting items from Avtor, it is a good practice to open Avtor at the top of the items the user wants to export. For more information on opening Avtor at a specific location, please see [Starting in the Content Editor](/avtor/gettingstarted.html#starting-in-the-content-editor).

Avtor only exports field values from the current Field Set. This allows the content editor to limit the fields in the export to the ones they are interested in updating or analyzing in Excel.

Once Avtor has been opened at the appropriate export location and the desired Field Set is selected, click on the Export Items ribbon button and choose the export options from the Export Items dialog.

![Export Items Ribbon](/Images/Avtor/ImportExport_ExportItemsRibbon.png)

Clicking this button will open the Export Dialog:

![Export Items Dialog](/Images/Avtor/ImportExport_ExportItemsDialog.png)

Avtor offers a number of options for the user when exporting items from Sitecore. The following section explains the options available in the Export Items dialog.

- **Export Language**: The content editor can choose to export item values from one or more languages in their Sitecore database. 
- **Only export items with fields in the Field Set**: Checking this check box will reduce the number of items exported by only including items with at least one field in the Field Set with a non-empty value. This setting is very useful when exporting items in an Item Bucket. This will remove the Sitecore items used to create the internal structure of the Item Bucket while exporting the data items in the bucket.
- **Include latest publishable version in export**: Avtor will always export the most recent version of an item. In some cases, the content editor may wish to compare the current values of an item with the values being used on the public facing website. If this check box is selected, Avtor will determine if an older version of the item is currently published and will include that older version in the export.
- **Additional Columns**: Avtor can include additional columns in the export to help the content editor edit the item. These additional columns are:
	- **Display Name**: The Sitecore display name. This is the name shown to the editor in the content tree. It may be different than the actual name of the item.
    - **Template Name**: This is the name of the Sitecore template used to define the fields in the Sitecore item.
    - **Statistics**: Includes 4 additional columns containing the Sitecore login name of the creator, the login name of the editor who last modified the item, the create date and last modification date of the item.
	- **Publishable**: A yes/no value indicating if the version of the item in the export is publishable.
	- **Workflow State**: The name of the current workflow state for the item.
    - **Preview Url**: A url the content editor can use to preview the page. To use this url, the user must be logged in to Sitecore and have access to the items that make up the page.
    - **Edit Url**: A url the content editor can use to open the page in the experience editor. To use this url, the user must be logged in to Sitecore and have access to the items that make up the page.
- **File Format**: The user can choose what format to use when generating the file. Please see below for details on each of the formats.

### Export items as CSV
Avtor can generate an export using the CSV or Comma Separated Values format. This format is a text file where the first line contains column names separated by commas, followed by a single line for each item, with the values of each field separated by commas.

Because the CSV format is relatively primitive, it is not importable back into Avtor. It is easily opened in Excel or other spreadsheet programs, but doesn't handle complex types like Rich Text fields or link fields very well.

Here is an example of opening an exported CSV in Excel:

![Excel CSV](/Images/Avtor/ImportExport_ExcelCSV.png)

With a few simple clicks, the spreadsheet can be cleaned up:

![Excel CSV Clean](/Images/Avtor/ImportExport_ExcelCSVClean.png)

### Export items as XML
Avtor can export items as an XML or Extensible Markup Language file. For more information on the XML specification, please see this [Wikipedia article](https://en.wikipedia.org/wiki/XML).

Avtor allows XML files to be imported back into Sitecore because the robust nature of XML allows field values to be associated together as items. This is very important for ensuring the accuracy of the items when importing them back into Sitecore.

### Using Exported XML data in Excel
Using the Exported XML data in Excel isn't as easy as using the CSV data described above. A few additional steps are required to allow Excel to accurately read and edit the XML file.

To use the Exported XML file in Excel, perform the following steps:

1. Save the exported file to a folder on your computer.
2. Open Excel.
3. Use Excel to open a workbook and browse to the Export file in excel. The default name is **ItemExport.Xml**.
4. Excel will present a dialog similar to this: <br/><br/>![Excel Open XML](/Images/Avtor/ImportExport_ExcelOpenXML.png)<br/><br/>
5. Choose "As an XML Table" and click OK.
6. Excel will open the spreadsheet. 

The first 3 columns in the spreadsheet contains values Avtor uses to import the items back into Sitecore, and those values must remain associated with the field values in the spreadsheet. The first 3 columns may be hidden, like in the example below, but may not be removed if you wish to import the field values back into Sitecore.

![Excel XML](/Images/Avtor/ImportExport_ExcelXML.png)

To import items updated in Excel, you must save the Excel spreadsheet as an XML file. This is done using the Save As function in Excel and choosing "XML Data" in the "Save as type" dropdown in the dialog.

![Excel Save XML](/Images/Avtor/ImportExport_ExcelSaveXML.png)

Excel will warn you about losing Worksheet features when you save the file. This is OK, since that information should not be included in an import. Clicking "Continue" will save the new XML file.

## Importing items
Avtor can import items from an XML file previously exported from Avtor. This file must contain the field values for **Item URI** and **Item Revision**. Avtor uses these values to correctly match items in the Sitecore database to items in the import file. Without these values, Avtor would have no way to ensure updated field values are being stored in the correct item.

To import a file, click Import Items on the Home ribbon.

![Import Items Ribbon](/Images/Avtor/ImportExport_ImportItemsRibbon.png)

This will open the import wizard. The Avtor import wizard allows the user to choose a file to import and then shows the status of the import.

![Import Wizard 1](/Images/Avtor/ImportExport_ImportWizard1.png)

The file will be uploaded and Avtor will begin importing the updated items. 

Once the import is complete, Avtor will show the status of the import in the Import Results screen.

![Import Wizard 1](/Images/Avtor/ImportExport_ImportResults.png)

The Import Results screen allows the user to download the detailed log and also provides summary details of the import. The summary shows the number of items imported, updated, unchanged and skipped.

#### Skipped import items
An item may be skipped if the value for **Item Revision** in Sitecore doesn't match the value for **Item Revision** in the Import. This check is done to prevent overwriting changes that may have occurred since the item was exported.

#### Downloading a new export
The import wizard will also allow the content editor to download a new export file by checking the "Download a new export file" checkbox. This file will contain updated values from the Sitecore database. This file should be used to edit the items if further updates are required.

