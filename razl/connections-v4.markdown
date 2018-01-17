---
title: Razl - Connections
layout: RazlLayout
---

# Razl

## Connections

Razl allows you to save multiple connections to instances of Sitecore. You connect to two instances of Sitecore and view the differences side-by-side in Razl.

### Creating a Connection

Before connecting to a Sitecore instance a connection has to be created. To create a connection the URL of the Sitecore instance and the name of the Sitecore database (master, web, core) must be known. The developer will also need access to either file system the instance is on or to the Sitecore shell.

To communicate to the Sitecore server Razl installs a web service in a directory called “_CMP” beneath the root of the Sitecore website. There are two options to install the required files, either directly via the file system if Razl has access or by creating a Sitecore package which can  be installed on the target server. For Razl to work the machine that Razl is on MUST be able to communicate to the Sitecore server over HTTP or HTTPs.

Once a connection has been created it is saved between Razl sessions so that the details do not have to be re-entered.

#### Creating a Connection using Direct Connection

If the machine Razl is running on has access to the Sitecore web root via the file system then it is recommended to use this installation method:

1. Click the **Connection Manager** button in the toolbar (see Toolbar section for the button)

![](/Images/Razl-v4/ConnectionManager.PNG)

1. Next click the "Add" button in the lower left side of the Connection Manager dialog.
1. The connection wizard will appear.
1. Enter a name into the **Connection Name** field: <br /> <br /> ![](/Images/Razl-v4/wizard1.PNG) <br /> <br /> The screen also gives the option of making the connection read only, this means that items can not be written or deleted from this connection. This option is highly recommended for scenarios where the Sitecore server is a live instance. This will help prevent any accidental updates of the live server data. <br /> <br /> Click **Next**<br /> <br /> 
1. The next screen will ask what type of connection to use, select **Direct Connection**:  <br /> <br /> ![](/Images/Razl-v4/wizard2.PNG) <br /> <br /> Click **Next** <br /> <br />
1. Enter the connection details for the server, enter the URL to server (this can be HTTP or HTTPs) and select the path to the web root: <br /> <br /> ![](/Images/Razl-v4/wizard3.PNG) <br /> <br /> You may also enter a Guid used to secure the connection. If multiple developers are accessing the instance of Sitecore using Razl, you will have to use the same Guid. By default, Razl chooses a random Guid for you. <br/><br />Before clicking Next you will need to test the connection by clicking the **Test Connection** button. If the test is successful click **Next**.
1. The Multi-Thraded screen allows you to choose the number of read threads and write threads when copying large amounts of items.<br /> <br /> ![](/Images/Razl-v4/wizard8.PNG) <br /> <br />Choosing a large number of threads could cause performance problems on the server(s) you are working with. The default of 4 threads is a good balance between performance of the copy operation and server load. Choosing numbers greater than 15 is unlikely to yield performance benefits.
1. On the next screen select the Sitecore database to use with this connection:<br /><br />  ![](/Images/Razl-v4/wizard4.PNG) <br /><br />  Select a database and  click **Next**.
1. The wizard will close and the new connection will be shown in the connection manager dialog:<br /><br />  ![](/Images/Razl-v4/wizard9.PNG) <br /><br />The new connection will also be accessible in both the left and right connection dropdowns after the connection manager dialog is closed:<br /><br /> ![](/Images/Razl-v4/wizard5.PNG)


#### Creating a Connection using Packaged Connection

If the machine running Razl does not have access to the Sitecore web root via the file system then use this installation method:

1. Click the **Connection Manager** button in the toolbar (see [Toolbar](/razl/screen-v4.html#toolbar) section for the button)

![Blank connection manager](/Images/Razl-v4/ConnectionManager.PNG)

1. Next click the "Add" button in the lower left side of the Connection Manager dialog.
1. The connection wizard will appear.
1. Enter a name into the **Connection Name** field:<br /><br />  ![](/Images/Razl-v4/wizard1.PNG) <br /><br />  The screen also gives the option of making the connection read only, this means that items can not be written or deleted from this connection. This option is highly recommended for scenarios where the instance being connected to is a live instance and where data is only being pulled. This will stop any accidental overwrites of the live server data. <br /> <br /> Click **Next**
1. The next screen will ask what type of connection to use, select Package Connections: <br /><br />  ![](/Images/Razl-v4/wizard6.PNG)<br /><br />  Click **Next**
1. Enter the connection details for the server, enter the URL to server (this can be HTTP or HTTPs): <br /> <br /> ![](/Images/Razl-v4/wizard7.PNG)<br /> <br /> Clicking **Pick Package Location** will open a dialog that will save the Sitecore package to disk. This package will need be deployed to the Sitecore solution. Save the zip file to a convenient location on the computer. Install this package on the target Sitecore instance and after installation click  the **Test Connection** button. If the test is successful click **Next**.
1. The Multi-Thraded screen allows you to choose the number of read threads and write threads when copying large amounts of items.<br /> <br /> ![](/Images/Razl-v4/wizard8.PNG) <br /> <br />Choosing a large number of threads could cause performance problems on the server(s) you are working with. The default of 4 threads is a good balance between performance of the copy operation and server load. Choosing numbers greater than 15 is unlikely to yield performance benefits.
1. On the next screen select the Sitecore database to use with this connection: <br /> <br /> ![](/Images/Razl-v4/wizard4.PNG) <br /> <br /> Select a database and  click **Next**.
1. The wizard will close and the new connection will be shown in the connection manager dialog:<br /><br />  ![](/Images/Razl-v4/wizard9.PNG) <br /><br />The new connection will also be accessible in both the left and right connection dropdowns after the connection manager dialog is closed:<br /><br /> ![](/Images/Razl-v4/wizard5.PNG)

### The Connection Manager
The connection manager allows the user to view and edit all of their connections in one place. Opening the connection manager is done by clicking the connection manager button in the toolbar:

![Connection maanger button](/Images/Razl-v4/ConnectionManagerButton.PNG)

When the connection manager opens, it will display a screen with all known connections listed on the left and the details of each connection shown on the right.

![Connection manager with connections](/Images/Razl-v4/ConnectionManagerWithConnections.PNG)

Clicking on a connection on the left side with select it and display its properties on the right.

![Connection manager with connections](/Images/Razl-v4/ConnectionManagerWithSelection.PNG)

Any of the fields in the connecton can be updated, and will automatically be updated in the connection.

#### Using the Connection manager
The fields in the connection manager have the following function:

- Connection Name - The name of the connection shown in the connection selection dropdown and in the connection list on the left.
- Read Only - When checked, the connection is read only, and Razl will not update or delete any items from the connection.
- Server Url - The url for the Sitecore server. This must be the root of the server. i.e. no path or query strings are allowed.
- Unc Path to Root - This is the path to the webroot in the file system. This can be a local path or a file system share. The user running Razl must have write access to the path to instal the Razl service. This field is displayed only for direct connections.
- Access Guid - The Guid Razl passes to the server on every request to ensure the request is comming from Razl. If more than one instances of Razl needs access to a server, the Access Guid needs to be the same on each instance.
- Database - Dropdown that allows the user to select the Sitecore database for the Razl connection. The list of databases in this dropdown can be refreshed by clicking the "Test Connection" button.
- Write Threads - The number of threads allowed to concurrently write items to the database when using the Razl bulk copy function.
- Read Threads - The number of threads allowed to read from the database looking for changes when using the Razl bulk copy function.

The buttons on the connection manager have the following function:

- Create Packages - Allows the user to select a location for the Razl service install and uninstall packages. This button only shows up if the selected connection was created as a package connection.
- Test Connection - Installs the service on the Sitecore server if the connection is a direct connnection and verifies that Razl can communicate with the service.
- Export - Allows the user to export the connection information to a file. This file can be imported into another install of Razl, duplicating the connection.
- Add - Allows the user to add a connection. Clicking this button will open the connection wizard shown above.
- Import - Allows the user to import a connection from another instance of Razl.
- Ok - Accepts the change the user made to the connections in the connection manager.
- Cancel - Reverts all changes made to the connections since the dialog was opened.

### Editing a Connection

The connection can also be edited right from the connection selection dropdown:

1. Click either the left or right connection drop down
1. Click the pencil icon that is next to the connection you want to edit:<br /> <br /> ![](/Images/Razl/editconn1.PNG)
1. The edit connection screen will appear, you will see different edit screens depending on the connection being used. For Direct Connections you will see:<br /> <br /> ![](/Images/Razl/editconn2.PNG) <br /> <br /> For Package Connections you will see:<br /> <br /> ![](/Images/Razl/editconn3.PNG)<br/> <br /> In either case, the **Export** button will allow you to export your connection so it may be used by other developers.
1. If you make any changes you must click **Test Connection** before you can save the settings.
1. Update the settings you want to change and click **Ok**.

### Deleting a Connection
The connection can be deleted from the connection selection dropdown without using the connection manager:
1. Click either the left or right connection drop down
1. Click the cross icon that is next to the connection you want to delete:  ![](/Images/Razl/deleteconn.PNG)
1. The connection will now be removed.

### Connection Information

Beside each connection in the toolbar is the connection info icon, when hovering over this icon information about the current connection will be displayed:

![](/Images/Razl/conn1.PNG)

The following information is displayed:

* Database - The database the connection uses
* Version - The Sitecore version number
* Machine - The name of the machine hosting the Sitecore instance
* Razl Version - The version of the web service used by the connection
* Sites - A list of sites available on the Sitecore instance

### Importing and Exporting connections

Sometimes multiple developers would like to connect to the same instance of Sitecore using Razl. A developer can now export a connection to Sitecore to a file. This file may be imported into another developers instance of Razl so the connection settings are shared between the developers. Please note, both developers need to be running the same version of Razl.
