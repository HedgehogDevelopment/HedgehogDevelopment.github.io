---
title: Using Feydra
layout: FeydraLayout
---

# Using Feydra
A front-end developer needs to be able to copy files to the web server to work with 
the website. There are a number of ways this can happen (Unc path, remote access, 
FTP, etc.). The choice of the technology for copying files to the server is left 
up to the end user.

### The Feydra Dashboard
Feydra is controlled through the Feydra dashboard. The Feydra dashboard is accessed 
by the url **http:&#47;&#47;[WebServer]/Feydra** where [WebServer] is the domain name of the 
web server. The dashboard has the following functions:

- **Status** – Shows the number of users, licenses and the latest log entries.
- **Users** – Allows users to be added and removed. Users can also obtain a link to 
activate Feydra.
- **Licenses** – Allows the licenses for Feydra to be updated. Viewing and adding 
licenses can only be performed on the local server. Remote viewing of the license screen 
is not permitted.
- **Settings** – Allows some of the settings controlling Feydra to be updated. The 
initial files a user sees when their username is created can be updated here.

![](/Images/Feydra/FeydraStatus.png)

There is a dropdown link in the menu bar of the website that will allow a user to 
activate Feydra for any of the registered users.

### Activating Feydra
The web application behaves normally when the front-end developer has not activated 
Feydra. To activate Feydra, the user can open the dashboard and use the dropdown link 
in the menu bar to activate Feydra by selecting their username. 

![](/Images/Feydra/ActivationDropdown.png)

The user can also obtain an activation link from the users page by clicking on the 
“![](/Images/Feydra/ActivationLink.png)” icon in the row for the user.

![](/Images/Feydra/UsersScreen.png)

### Deactivating Feydra
When the front end developer is finished using Feydra, they can deactivate their virtual
sandbox by going to the dashboard and clicking on the link "Deactivate Feydra". 

![](/Images/Feydra/DeactivateLink.png)

The user can also browse to the target of that link without going to the dashboard. The 
url is http://[Webserver domain]/Feydra/FyUser/Deactivate

## Updating the front-end assets
When the front-end developer activates Feydra, they will see a copy of the application 
running application. We call this the users’ virtual sandbox. This virtual sandbox uses 
all of the deployed front-end assets (cshtml, js, css, etc…) to run the application. If 
the user copies a front-end asset into their personal folder under **/FeydraRoot**, the 
front-end asset from the personal folder replaces the file of the same name and relative 
path in the deployed web application.

An example of this is a web application with the following folder structure:

    [WebRoot]
    ├───Areas
    │   └───Products
    │       ├───Index.cshtml
    │       └───View.cshtml
    └───Include
        ├───css
        │   └───site.css
        └───js
            └───site.js

When User1 is created, a personalized sandbox folder for that user will be created 
under the FeydraRoot folder:

    [WebRoot]
    └───FeydraRoot
        └───User1

Now, User1 can use their personal Feydra activation link to activate Feydra. The web 
application will look exactly as it did if Feydra isn’t activated since they have no 
files in their sandbox. 

If the user creates a file called **Index.cshtml** in **/FeydraRoot/User1/Area/Products**, 
the file will override the **Index.cshtml** file used to render the products page on the 
website. This allows the front-end developer to update the front-end functionality of 
the web application, while allowing other parts of the application to function with 
existing front-end assets.

The user may also update the Site.js file in the folder /Include/js by placing a new 
**Site.js** file in **/FeydraRoot/User1/Include/js**. The new **Site.js** will be sent 
to the browser in place of the existing one when the page is refreshed. 

If there are other users of the site who have not activated as User1, they will not see 
any of the changes made by User1 until the changes are deployed as part of the normal 
deployment process. Additional users may be created to allow multiple developers to work 
with the website. Each developer will only see the changes in their virtual sandbox while 
Feydra is activated.

If the front-end developer views the page source when Feydra is activated, they will see 
comments around various parts of the code indicating where the .cshtml files exist on the 
file system. 

![](/Images/Feydra/ExampleHtml.png)

This will provide hints to the front-end developer for manipulating various components 
on the page.

## Adding Licenses

Licenses are added to Feydra using the license management screen. This screen may only 
be accessed when logged into the console of the local server. 

![](/Images/Feydra/LicensesScreen.png)

Feydra will not allow users to activate their virtual sandbox if there aren’t enough 
CAL’s for all of the created users.

The user can add new license keys by selecting Add License.

The “![](/Images/Feydra/Refresh.png)” (Refresh) action will contact the Hedgehog License Server and update the 
number of CAL’s (Client Access License) or license type if it has changed.

The “![](/Images/Feydra/Delete.png)” (Delete) action will remove a license and its associated CAL’s from the server.

## Feydra Settings
The Feydra settings screen allows the developer to view and/or change the settings 
Feydra uses on the server. 

![](/Images/Feydra/SettingsScreen.png)

To use this screen, simply make the changes needed to the settings and click 
“Update Settings”

The settings the user can update are as follows:

- **Cookie Name** – The name of the cookie Feydra uses to maintain the current user 
activation.
- **Root Folder** – The name of the Feydra root folder. If this is changed after 
users are created, the developer is responsible for moving the users files into the 
new location.
- **User Create Actions** – This allows the developer to specify files to copy 
(relative to the web root) into each virtual sandbox when the user is created. 
This is useful for setting up files like the **/Views/web.config**, since these files are 
needed by MVC to build the views correctly.

## Conclusion
Feydra supports multiple user sandboxes, allowing multiple front-end developers to work 
with a single web application. This will dramatically reduce the costs of maintaining 
development and test environments for front-end developers while allowing them to complete 
their task more efficiently.