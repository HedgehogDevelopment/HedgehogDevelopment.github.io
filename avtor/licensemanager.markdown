---
title: Avtor License Manager
layout: AvtorLayout
---

<script>
	window.location.replace("https://doc.sitecore.com/users/100/sitecore-experience-platform/en/managing-licenses.html");
</script>

## Avtor License Manager
The Avtor license manager is useb by the Sitecore administrator to manage the licenses owned by your organization. The screen allows the administrator to apply new licenses, refresh expired licenses and manage users using Avtor.

## Starting the license manager
To start the Avtor License Manager, please follow these steps:

1. Log into Sitecore as an administrator
2. Click on "Desktop" on the launch pad
3. Open the start menu and select Security Tools > Avtor License Manager<br/><br/> ![](/Images/Avtor/LicMan_1.png)<br/><br/>

If this is the first time opening the license manager, you will be asked to accept the Avtor license agreement.

## Managing licenses
The License tab of the license manager allows the Sitecore administrator to add, refresh and remove Avtor licenses. 

<br/> ![](/Images/Avtor/LicMan_4.png)<br/><br/>

The screen will also display the total licenses installed on the server and how many licenses have been allocated to users.

### Adding a new license
To add a new license, Click "Add License" <br/><br/>![](/Images/Avtor/LicMan_2.png)<br/><br/>
Next, enter your license key in the popup and click "OK" <br/><br/> ![](/Images/Avtor/LicMan_3.png)<br/><br/>

Avtor will contact the hedgehog license service and validate the license. Once validated, the number of users and expiration date will be shown on the dialog.

### Refreshing the license
Avtor will contact the Hedgehog license server every few days to re-validate the license. If you have purchased additional seats for your license, you may want to refresh the license sooner. This can be done by clicking the "Refresh" (![](/Images/Avtor/Icon_Refresh.png)) button next to the license. This will cause Avtor to contact the server and download the new license information.

### Removing a license
To remove a license from Avtor, click on the "Remove" (![](/Images/Avtor/Icon_Delete.png)) button next to the license. This will remove the license from Avtor and reduce the number of available licenses for Avtor users. If you have more users than Avtor than licenses, you will need to go to the User tab and remove some users.

## Managing Users
Avtor users can be added or removed using the Users tab in the Avtor License Manager.
<br/><br/>
![](/Images/Avtor/LicMan_Users.png)
<br/><br/>
If the number of users in Avtor exceeds the number of licenses you have purchased, the users will not be allowed to use Avtor. To restore Avtor functionality, users must be removed from the user manager screen.

### Adding Users
Users can be added to Avtor two ways. They can be added manually, using the User manager, or automatically. 

#### Manually adding users
To add a user manually, click the "Add User" button on the User management tab. This will popup a dialog allowing the user to enter a username.
<br/><br/>
![](/Images/Avtor/LicMan_AddUser.png)
<br/><br/>
#### Automatically adding users
Users will automatically be added to Avtor when they try to start Avtor for the first time. This simplifies managing user licenses in Avtor, since the process is completely automated.

If there are no more available Avtor licenses, the user will be presented with a dialog telling them that they need more licenses or users need to be removed from the User tab in the Avtor license manager.

### Removing Users
Users can be removed by clicking the "Remove" (![](/Images/Avtor/Icon_Delete.png)) icon next to the username in the User management tab. This will free up licenses for other content editors.