---
title: Chapter 2 - TDS Documentation
layout: TdsLayout
---

# Team Development for Sitecore 

## Chapter 2 – Getting started with TDS

### System Requirements

* Team Development for Sitecore has been fully tested with Team Foundation Server and Subversion, but will also work with any Microsoft compliant source control system. 
* Visual Studio 2010, 2012 or 2013 .
* Sitecore version 6.1 and higher. 
* Sitecore Xpress is not supported by Team Development for Sitecore.

### Installation

Installing TDS is a quick and easy process.  It is recommended that you shut down all running applications prior to beginning the install process.
The zip file you downloaded from the [Hedgehog Development](http://hhogdev.com) website contains a version of TDS to match up with the version of Visual Studio that you are running.

| **Visual Studio version	Team** | **Development for Sitecore version** |
| ------------- | ----------- |
| Visual Studio 2010 | HedgehogDevelopmentTDS_2010.msi |
| Visual Studio 2012 | HedgehogDevelopmentTDS_2012.msi |
| Visual Studio 2013 | HedgehogDevelopmentTDS_2013.msi |
|                    |                                 |
\s\s
Unzip the files to a directory of your choice to install from. Once you selected the version of TDS that matches the version(s) of Visual Studio you work with you are ready to install. 

<div class="panel">
 <div class="panel-header bg-lightBlue fg-white">
 NOTE
 </div>
 <div class="panel-content">

<p>
By default TDS wants to install the project templates (TDSProject.zip) in the My Documents folder on your C: drive. Located at:
</p>

<pre>
C:\Users\[Username]\AppData\Local\Microsoft\VisualStudio\11.0\ProjectTemplates
</pre>

<p>
If you have relocated the My Documents folder to a different directory, the Visual Studio path does not get updated.
</p>
<p>
You should make sure that the Visual Studio User Project Template Location in Visual Studio is pointing to the desired location. You can do so by:
</p>
<p>
In Visual Studio go to <strong>Tools &gt; Options menu.</strong>
</p>
<p>
Under the Projects and Solutions highlight the General settings
</p>
<p>
Locate the Visual Studio user project template location. Verify that this path is correct. For example in VS 2012 it should be: <strong>Path to directory\Visual Studio 2012\Templates\ProjectTemplates</strong>
</p>
<p>
Click OK when you are done and now you should see the TDS Project Template when you try to create a new project.
</p>
<p>
Also, please note that if Visual Studio is running in Safe Mode add-ins are NOT loaded.
</p>
 </div>
</div>

#### Step-by-Step Instructions 

Once you have downloaded the TDS .zip package and extracted the version(s) you wish to install you may begin to install TDS.

1. Start by double-clicking the .msi file to begin the installation
2. Click **Next** to begin the process of installing TDS
3. Read and accept the license agreement. Then click **Next**.\s\s

![](/Images/chapter2-license.png)
4. Enter the license key provided by Hedgehog Development. Make sure the company name is spelled exactly as specified with your license key. Do not put quotes around the company name or the license key.
5.Select the path where you want TDS installed. Typically, the default value is acceptable.
6. Confirm the installation by clicking Next.
7. When the installation is complete the following will appear.


#### Updateing the TDS License

After you have installed TDS you may need to update the license you are using, e.g. when moving from a trial license to a full license. You can do this by opening Visual Studion and click on the **Help** menu then **View TDS License**:

The TDS License dialog will appear showing you your current license:
 
Enter your new license details and click update to change the license.

### Initial Configuration

We will now show how to configure TDS for an existing Sitecore project. Syncing TDS with an existing Sitecore project is quick and simple. There is no need to start a Sitecore project over, or laboriously move existing code just because you’ve downloaded a new plug in. 
Integrating an existing Sitecore project with a new TDS project is extremely easy. Once TDS is configured, Sitecore items are added through the “Get Sitecore Items” option. Before we begin configuring TDS, there are some assumptions that we need to consider.

There are two mandatory conditions that must be met. They are as follows:

1. TDS has been installed.
2. There is an existing Sitecore installation with a project currently under development. The team wishes to use TDS to gain more control over their Sitecore Items.

(Optional) There is an existing solution with custom application code in a Web Application Project.

#### Create the TDS Project

Adding TDS to your development process is extremely simple. To create a new TDS project, follow these simple steps:

1. In Visual Studio open the “**New Project**” dialog. You may want to add this new project to your existing solution, or create it stand alone.
2. Choose Project type: “**TDS Project**” and choose the template: “**TDS Project**” then specify the desired name, location and Source Code Control (SCC) options (if applicable). For more information on the different project types see the TDS Project Types section.
 

### Connect the TDS Project to Sitecore

TDS installs a web service on the Sitecore server to communicate with the Sitecore database. There are a number of installation options and settings that will be covered in a later chapter. The steps below outline how to quickly get TDS setup with a development server.

1.	Locate the TDS project in the Solution explorer, right-click on it and select “**Properties**”. This opens the TDS project property page.
2.	On the left side of the property page, click on “**Build**” to open the build property tab.
3.	There are three settings that need to be configured to tell TDS how to find the Sitecore server.
	1.	**Sitecore Web URL** – This specifies the URL to local Sitecore install. This is the URL to the root of your Sitecore environment (not the /Sitecore folder). TDS installs a web service to your Sitecore Deploy Folder and then communicates through that web service to push your changes to Sitecore. It finds the service via this URL.
	2.	**Sitecore Deploy Folder** – This specifies the absolute path to the web root. This is the UNC path to the web root of the Sitecore instance you are connecting TDS to. This tells TDS where you want it to place the web service and copy the supporting DLL and configuration file to.
	3.	**Install Sitecore Connector** – Checking this will allow TDS to install the Sitecore Connector web service in your Sitecore instance. This allows access to Sitecore items on the server. **This check box must be checked to complete this example.**
4.	The last step is to right-click on the TDS project and select “**Install Sitecore Connector**”. This installs the service to the target Sitecore instance specified in the build property page.

#### Adding Sitecore Items to the TDS Project 

Items are initially added to the TDS project using the “**Get Sitecore Items**” dialog. This allows you the browse the items in your Sitecore content tree and pick the items to add to the project.
To add a few items to your TDS project, follow the steps below.

1. Right-click on the TDS project in the Solution Explorer and choose “**Get Sitecore Items**”.
2. The Get Sitecore Items dialog will open and show the Sitecore items in the root of the content tree.
3. Expand the template folder where you have created a few templates for your Sitecore solution. In the example below, it is /Template/MvcNewsApp.
4. Check the check-box next to an item to bring it into Sitecore. The dialog is aware of parent-child relationships, so checking a child item will automatically select the parents.
5. If you want to bring all templates under the template folder you are using to hold your custom templates, you can right-click on the template and choose “Select all children”.
6. Once you have selected the templates you wish to bring into your TDS project, click “Get Items” and TDS will begin getting the items

#### Choosing which items to bring into a TDS porject

TDS allows you to bring any Sitecore item into your TDS project. It is NOT best practice to bring every Sitecore item into the TDS project for the following reasons:

1. The source control system becomes a content management system.
2. The source control repository becomes bloated with lots of files that are not part of the project. 
3. Media items tend to be large and are not handled well by source control.
4. When upgrading to a new version of Sitecore, Sitecore may change many of their items. All of the changes made by Sitecore need to be merged and resolved in source control. This task is made more difficult because the developer may not be familiar with all of the changes or the reason the changes were made.
5. Having many thousands of items in a TDS project causes TDS to require more memory and processor resources to keep track of the items. In some cases, that may cause performance issues within Visual Studio.

At Hedgehog Development, we try to determine the ownership of a given item to help us decide if the item should be included in the TDS project. There are three roles we commonly find TDS items falling into.

1. **Items owned by Sitecore** – These are usually items that are in the /System or /Templates/System folder. They are usually part of the base install of Sitecore, or are installed as part of an add-in modules like Web Forms for Marketers. These items are not normally brought into TDS because they are part of the infrastructure of Sitecore.
2. **Items owned by Developers** – These items are almost always brought into TDS. They are the “schema” of the Sitecore solution. These are items created by the developers such as Templates, Layouts, Sublayouts, Taxonomy and Metadata. These are items that are not edited by content editors.
3.	**Items owned by Content Editors** – These items contain actual content for the site. This is the data that drives the front end. In most cases, these items should not be in the TDS project since they will be edited by the content editors outside of the deployment schedule.

The above roles are to be used as guidelines for determining which items should be included in the TDS projects. In some cases, it may be necessary to bring Sitecore items into the TDS project. This is usually done when the development team needs to make a change to a Sitecore owned item. After changing the item, it is owned by the development team. The item can now be easily managed by the development team, and if there is a conflict with the item after a Sitecore upgrade, it can easily be located and resolved.

### TDS Project Types

TDS comes with different project types from which to create your TDS projects. To access the different project types open the New Projects dialog in Visual Studio and select TDS Project from the Templates list:
 
#### TDS Project

Creates a new TDS Project as part of your solution, you will then need to configure the connection to your Sitecore instance in the project property pages.

#### TDS Project with wizard

Creates a new TDS Project as part of your solution but then runs you through a wizard to help setup a Sitecore instance. The first screen in the wizard will ask you for the basic connection information:


* Sitecore Web Url – the URL to the Sitecore instance that TDS will connect to.
* Sitecore Deploy Folder – the path to the Sitecore instance specified in the Sitecore Web Url field.
* Source Web Project – the web project to use if you have one.
* Sitecore Database  - the Sitecore database to read and write items to.

If you have multiple TDS Projects in you solution and you enter a Sitecore Web Url used by another project the wizard will fill in the other fields automatically. Clicking ok will configure the project and install the Sitecore Connector if you checked it.