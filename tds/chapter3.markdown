---
title: Sitecore TDS - Architecture
layout: TdsLayout
---

## Sitecore TDS Architecture

Sitecore TDS is a Visual Studio add-in that allows developers to pull Sitecore items in to their local file system as files. Since the Sitecore items are files, they can easily be tracked using all common source control systems available in the marketplace.

In addition to being tracked in source control, Sitecore TDS uses an MSBuild project file to group the Sitecore items into a deployable project. The Sitecore TDS deployment process allows the development team to automatically build and deploy items to an instance of Sitecore. Since the deployment of items is done using automated scripts instead of being a manual process, it is much more reproducible.

### Sitecore TDS Add-in

The Sitecore TDS add-in is compatible with Visual Studio 2013, 2015, 2017 and 2019. The operation of the add-in across the different versions of Visual Studio is, in most cases, exactly the same.

The Sitecore TDS add-in communicates with Sitecore using a web service. The web service uses the Sitecore Serialization API to convert Sitecore items to files. These files are stored in the /Data/Serialization folder in Sitecore. The service locates these files and passes them back to Sitecore TDS. Sitecore TDS adds/updates the files in a folder structure very similar to other Visual Studio projects. This allows Sitecore TDS projects to be compatible with all major Source Code management systems in use today.

### Sitecore TDS Web Service

Sitecore TDS installs a web service on the target Sitecore instance to communicate with Sitecore. The service is installed in the /_Dev folder and a .dll is copied to the /bin folder. Sitecore TDS uses the active project configuration to determine which Sitecore server, if any, to communicate with.

All interactions with the Sitecore TDS service require a valid Access Guid for the service to fulfill the request. This access Guid is stored in the Sitecore TDS project file when the user chooses to install the Sitecore connector.

The settings that Sitecore TDS uses to communicate with Sitecore are the **Sitecore Web Url** and the **Sitecore Deploy Folder**. These settings are located in the Build tab of the Sitecore TDS project properties. The build tab can be accessed by right clicking on the Sitecore TDS project and selecting “Properties”. Selecting the “Build” tab along the left side of the property window shows the build properties.

The “Configuration” drop down at the top left of the Build Property Page shows which project configuration the dialog is showing/editing.

![/Images/Tds/chapter3-build.png](/Images/Tds/chapter3-build.png)

The (A) and (B) arrows point to the **Sitecore Web Url** and **Sitecore Deploy Folder** settings. The (C) arrow is pointing at the **Install Sitecore Connector** setting. This controls how Sitecore TDS installs the service. If this is checked, the service is installed permanently, and Sitecore TDS can use the Sync Window to compare the Sitecore server items to the project items.