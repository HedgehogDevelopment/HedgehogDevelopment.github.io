---
title: Razl - Connections
layout: RazlLayout
---

# Razl

## Connections

### Creating a Connection

Before connection to a Sitecore instance a connection has to be created. To create a connection the URL of the Sitecore instance and the name of the Sitecore database (master, web, core) must be known. The developer will also need access to either file system the instance is on or to the Sitecore shell.

To communicate to the Sitecore server Razl installs a web service in a directory called “_CMP” beneath the root of the Sitecore website. There are two options to install the required files, either directly via the file system if Razl has access or by creating a Sitecore package which can  be installed on the target server. For Razl to work the machine that Razl is on MUST be able to communicate to the Sitecore server over HTTP or HTTPs.

Once a connection has been created it is saved between Razl sessions so that the details do not have to be re-entered.

#### Creating a Connection using Direct Connection

If the machine Razl is running on has access to the Sitecore web root via the file system then it is recommended to use this installation method:

1. Click the **Create Connection** button in the toolbar (see Toolbar section for the button)
2. The connection wizard will appear.
3. Enter a name into the **Connection Name** field: <br /> ![](/Images/Razl/wizard1.PNG) <br /> The screen also gives the option of making the connection read only, this means that items can not be written or deleted from this connection. This option is highly recommended for scenarios where the instance being connected to is a live instance and where data is only being pulled. This will stop any accidental overwrites of the live server data. <br /> Click **Next**
4. The next screen will ask what type of connection to use, select **Direct Connection**:  <br /> ![](/Images/Razl/wizard2.PNG) <br /> Click **Next**
5. Enter the connection details for the server, enter the URL to server (this can be HTTP or HTTPs) and select the path to the web root: <br /> ![](/Images/Razl/wizard3.PNG) <br /> Before clicking Next you will need to test the connection by clicking the **Test Connection** button. If the test is successful click **Next**.
6. On the next screen select the Sitecore database to use with this connection:<br /> ![](/Images/Razl/wizard4.PNG) <br /> Select a database and  click **Next**.
7. The wizard will close and the new connection will be accessible in both the left and right connection dropdowns:<br /> ![](/Images/Razl/wizard5.PNG)


#### Creating a Connection using Packaged Connection

If the machine running Razl does not have access to the Sitecore web root via the file system then use this installation method:

1. Click the **Create Connection** button in the toolbar (see Toolbar section for the button)
2. The connection wizard will appear.
3. Enter a name into the **Connection Name** field:<br /> ![](/Images/Razl/wizard1.PNG) <br /> The screen also gives the option of making the connection read only, this means that items can not be written or deleted from this connection. This option is highly recommended for scenarios where the instance being connected to is a live instance and where data is only being pulled. This will stop any accidental overwrites of the live server data. <br /> Click **Next**
4. The next screen will ask what type of connection to use, select Package Connections: <br /> ![](/Images/Razl/wizard6.PNG)<br /> Click **Next**
5. Enter the connection details for the server, enter the URL to server (this can be HTTP or HTTPs): <br /> ![](/Images/Razl/wizard7.PNG)<br /> Clicking **Pick Package Location** will open a dialogue that will save the Sitecore package to disk. This package will need be deployed to the Sitecore solution. Save the zip file to a convenient location on the computer. Install this package on the target Sitecore instance and after installation click  the **Test Connection** button. If the test is successful click **Next**.
6. On the next screen select the Sitecore database to use with this connection: <br /> ![](/Images/Razl/wizard4.PNG) <br /> Select a database and  click **Next**.
7. The wizard will close and the new connection will be accessible in both the left and right connection dropdowns: <br /> ![](/Images/Razl/wizard5.PNG)

### Editing a Connection

Once a connection has been created it can later be edited:

1. Click either the left or right connection drop down
2. Click the pencil icon that is next to the connection you want to edit:<br /> ![](/Images/Razl/editconn1.PNG)
3. The edit connection screen will appear, you will see different edit screens depending on the connection being used. For Direct Connections you will see:<br /> ![](/Images/Razl/editconn2.PNG) <br /> For Package Connections you will see:<br /> ![](/Images/Razl/editconn3.PNG)
4. If you make any changes you must click **Test Connection** before you can save the settings.
5. Update the settings you want to change and click **Ok**.

### Deleting a Connection
Once a connection has been created it can later be deleted:
1. Click either the left or right connection drop down
2. Click the cross icon that is next to the connection you want to delete:  ![](/Images/Razl/deleteconn.PNG)
3. The connection will now be removed.

### Connection Information

Beside each connection in the toolbar is the connection info icon, when hovering over this icon information about the current connection will be displayed:

![](/Images/Razl/conn1.PNG)

The following information is displayed:

* Database - The database the connection uses
* Version - The Sitecore version number
* Machine - The name of the machine hosting the Sitecore instance
* Razl Version - The version of the web service used by the connection
* Sites - A list of sites available on the Sitecore instance
