---
title: Installing Avtor
layout: AvtorLayout
---

# Introduction
Avtor is a tool designed to streamline editing of a field or fields across many items at once. It needs to be installed in Sitecore by an administrator using the Sitecore Update Installation Wizard tool. This document will demonstrate how to choose the correct version of Avtor to install and how to install it on a Sitecore server.

## Choosing the right package
Each major release of Sitecore has its own Avtor installation package, so it is very important the correct package is installed on the Sitecore server. Avtor is compatible with Sitecore 8.0, 8.1, 8.2 and 9.0. The Avtor update package are distributed in a .zip file and are named:

    Hedgehog.Avtor_8.0.update
    Hedgehog.Avtor_8.1.update
    Hedgehog.Avtor_8.2.update
    Hedgehog.Avtor_9.0.update

The Sitecore version number in the filename specifies the Sitecore major release the package is designed to be installed on.

## Installing Avtor
Avtor is installed using the Sitecore Update Installation Wizard. Access to the wizard is limited to Sitecore Administrators. When installing on Sitecore 8.0 and 8.1, the user must manually enter the url for the Update InstallationWizard after logging in as an admin. Sitecore 8.2 and above have made this process a bit easier. Please see the section below for step-by-step instructions for your version of Sitecore

### Sitecore 8.0, 8.1 and 8.2
1. Log in to Sitecore as an administrator.
2. Open a new browser tab and browse to the url http://[server]/sitecore/admin/UpdateInstallationWizard.aspx
3. Click "Choose a package"
4. Click "Browse" to select the update package and then click "View package information"
5. Click "Analyze and install the package"
6. Click "Install"
7. When the package is done installing, click "Installation result"

### 9.0
1. Log in to Sitecore as an administrator
2. Click "Control Panel" on the launch pad.
3. Click "Administration tools" under "Administration"
4. Click "Update Installation Wizard" under Auxilary
5. Click "Select a package"
6. Click "Browse" to select a package and then click "Package information"
7. Click "Analyze the package"
8. Click "Analyze"
9. When the analysis is complete, click "Analysis result"
10. Click "Apply and install package"
11. When the package is done installing, click "Installation result"

## Installing the License
Avtor licenses are installed using the license manager application. This application is found on the desktop "Start Menu" for an administrator. Please note, when installing an Avtor license, the browser being used to add the license must have access to the internet so the license can be validated.

1. Log into Sitecore as an administrator
2. Click on "Desktop" on the launch pad

![](/Images/Avtor/LicMan_1.png)

3. Open the start menu and select Security Tools > Avtor License Manager

![](/Images/Avtor/LicMan_2.png)

4. Click "Add License"

![](/Images/Avtor/LicMan_3.png)

5. Enter your license key in the popup and click "OK"

![](/Images/Avtor/LicMan_4.png)

6. The license will be validated and the number of users and expiration date will be filled in on the dialog.
7. Click "OK" to close the dialog

Your content editors are now rady to start using Avtor.

*** Please note: Users are added to Avtor automatically as they start using Avtor. Your organization is allowed the number of users specified in the Avtor license. Once the number of users using Avtor reaches the number of users specified by the license, new users of Avtor will not be allowed to use Avtor. For more information, please see the documentation for the license manager.