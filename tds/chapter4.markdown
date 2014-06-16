---
title: Chapter 4 - TDS Documentation
layout: TdsLayout
---

# Team Development for Sitecore 

## Chapter 4 – Using TDS for Sitecore Development

Hedgehog Development originally developed TDS as an internal project to help our own development teams build Sitecore implementations. TDS was developed for Sitecore developers, by Sitecore developers. The guidelines documented in this manual are the best practices we have built around using TDS as a development platform for many Sitecore implementations. We recognize that not all development projects are organized the same way, and TDS was designed to allow as many different ways of developing Sitecore sites as possible.

The primary goal of TDS was to allow developers to manage their Sitecore schema (Templates, Layouts, Sublayouts, Taxonomy and meta-data items) the same way they manage source code. The Software development field has, over the years, built many exceptional tools and practices for managing and deploying source code, but Sitecore developers were not able to leverage things like Source Control, automated builds and automated deployments for their Sitecore items.

### The Sitecore database(s)

When developing a website, it makes sense for developers to build the implementation on a local IIS instance and commit the result to source control. Since Sitecore is a platform built on IIS, the practice of developing on a local IIS instance is a given. 

Before TDS was developed, Sitecores' recommended development environment was a local IIS and a shared database. This worked reasonably well, but there was always a chance that developers would introduce conflicting changes to the database, and resolving these conflicts could cause delays in the development process.

One of the reasons Hedgehog Development created TDS was to easily allow developers to build a Sitecore implementation in an isolated development environment. This would mean each developer would have their own instance of the Sitecore databases on their local machine and could work without fear of causing problems for other developers on the team. TDS allows developers to bring their changes into a Visual Studio project and, much like source code, the changes made to Sitecore can be committed to source control. 

### Working outside the web root

One of the practices we use at Hedgehog Development is to locate all source files and projects outside of the Sitecore web root. TDS has a built in process that allows the compiled solution to be copied to the target Sitecore website at build time. This allows the developer to easily keep track of items in their project. This arrangement is also advantageous when using file system based source control systems like GIT. There is no longer a need to exclude Sitecore components from Source Control, since the source control system does not see them in the file system. This arrangement also closely resembles the deployment process and configuration used in production environments, which leads to more stable releases.

### Solution Structure

TDS, much like other Visual Studio projects, allows developers to create both simple and very complex Visual Studio solutions. Since solutions tend to grow in both size and complexity over time, it makes sense to start with a very simple and flat file structure. As the solution grows, keeping the solution files as flat as possible makes it easier to work with, build and deploy.

A typical simple Sitecore solution consists of a Web Project, one or more Class Libraries and one or two TDS projects. There are other possible project types that may be added to the solution as needed. As a starting point, only these three will be covered.

* **Web Project** – The web project holds web assets, configuration files and UI code. These will be deployed to theSitecore web folder by TDS when the project is built. This is controlled by setting the Source Web Project in the General project property page. For more information on TDS project property pages, please see below.
* **Class Libraries** – The Class Libraries contain APIs that are used by the UI layer. These usually consist of ORM layers, data access layers, interfaces to other applications and any API's that may be reused across Sitecore solutions. Adding additional class libraries is the most common way a project grows.
* **TDS Projects** – The TDS projects are used to hold Sitecore items and deploy the project. TDS can only deploy Sitecore items to a single Sitecore database. Having multiple projects allows TDS to manage and deploy to multiple databases (e.g. core and master). When there are multiple TDS projects in a solution, the Sitecore Access Guid must be the same for all project configurations pointing at a specific Sitecore instance.

| Sample Visual Studio Project | Solution File Structure. |
| -------- | -------- |
| ![](/Images/chapter4-vsproject.png) | ![](/Images/chapter4-solutionproject.png) |
| An example of a simple Sitecore solution. | The folder structure for this solution. The file structure closely resembles the solution in Visual Studio. |

<br />

In the example above, there is a \Lib folder in the file system. This contains any reference DLL's needed to build the project. By keeping all resources needed for the project under a single folder, the development team can easily leverage advanced source control features like branching, merging and labeling. Additionally, this structure lends itself to setting up automated builds.

### TDS project property pages

The TDS project property pages are used to connect the TDS project to a Sitecore instance and to control how the TDS project interacts with other projects in the solution during the build. 


#### General

Contains settings that are common to all project configurations.

![](/Images/chapter4-general.png) 

* **Source Web Project** – This dropdown selects the web project to copy to Sitecore when the TDS project is built. This may be set to &lt;None&gt; if there is no need to copy files to Sitecore.
* **Source Web Physical Path** – For information only. This shows the path to the web project.
* **Source Web Virtual Path** – For information only. This shows the path within the solution to the web project.
* **Sitecore Database** – Configures the Sitecore database the TDS project will use.
* **Assemblies** – When deploying to Sitecore, TDS can skip the deployment of certain assemblies. These assemblies may be referenced by one or more projects in the solution. Excluding/including static assemblies from the build will reduce the size of the packages TDS generates and improve deployment time. By default, TDS excludes assemblies beginning with "Sitecore.". Selecting **Exclude** from the dropdown will cause TDS to skip these files and not add them to the deployment. Selecting **Include** from the dropdown will only include the files listed and cause TDS to skip all the files not listed.

#### Code Generation
 
Used to turn on and control TDS Code Generation. 
 
![](/Images/chapter4-codegeneration.png)

* **Target Project** – The target project in which the generated code file will be generated.
* **Code Generation Target File** – the name of the file that will contain the generated code. Remember to add the appropriate extension, e.g. ".cs" for c-sharp files.
* **Base Namespace** – The namespace that class will be generated in.
* **Header Transform File** – The TT file used to generate the header of the generated file.
* **Base Project Transform File** – The TT file used to generate output for each item in the generated file.
* **Sitecore Fields to Pass to Code Generation** – Standard Sitecore fields that should be passed to the code generation template. By default standard Sitecore fields are skipped but developer created fields are always passed to the code generator.

Please see the code generation section below for more information on the Code Generation property page.

#### Multi-Project Properties

The Multi-Project properties page allow you to setup dependencies between projects within the same solution.

![](/Images/chapter4-multiproject.png)


##### Base Template Reference

The Base Template Reference section can be used to tell a TDS project where it should look for base templates when generating code for templates in the current project:
 
![](/Images/chapter4-basetemplates.png)

For example, imagine the there is the following project setup with templates T1 and T2. Template T2 inherits template T1 but they are in different Tprojects.
 
![](/Images/chapter4-basetemplatesprojects.png)

When TDS performs code generation we want templates generated by the TdsDemo.Layouts project to be used by the TdsDemo.Templates project.

The generated class for TdsDemo.Layouts will look like this:

    namespace TdsDemo.Layouts.sitecore.templates.TDS.Set1
    {
        public partial interface IT1
        {
            string F1 { get; set; }
        }
    }

And the generated glasses for  TdsDemo.Templates will be:

	namespace TdsDemo.Templates.sitecore.templates.TDS.Set2
	{
	    public partial interface IT2 :   
	                    global::TdsDemo.Layouts.sitecore.templates.TDS.Set1.IT1
	    {
	        string F2 { get; set; }
	    }
	}

Notice that the second code generated file references the classes generated by the first. 

*If the two generated files are in different projects then a reference to the project with the first generated file will need to be added to the second project.*

The referencing project must know how to generate the namespaces required by the referenced project. For example if the referenced and referencing project use different methods of generating namespaces then the referencing project may not be able to find the classes in the referenced project.

##### Package Bundling

The Package Bundling section can be used to tell a TDS to pull in items from another project when creating an Update Package. When TDS builds the current project it will automatically add any items in the referenced projects to the update package.

![](/Images/chapter4-packagebundling.png) 

If the referencing and referenced project both contain the same item, the item in the
referencing project is used.

Package bundling only works when the Update Package has been configured, see the Update Package section below.

#### Build
 
Contains settings used to connect TDS to a Sitecore instance. The settings on this page are different for each project configuration, allowing TDS to easily work with multiple Sitecore instances.

![](/Images/chapter4-build.png) 

*	**Build Output Path** – Sets the location TDS will use to collect the files to be deployed or packaged.
*	**Edit user specific configuration** – When this checkbox is checked, the user will edit the settings in the .user file instead of the project (.csproj) file. This allows developers to have specific settings for their local TDS deployment that are different than other developers on the team without creating a configuration that is specifically for that user.
 
<div class="panel">
 <div class="panel-header bg-lightBlue fg-white">
 NOTE
 </div>
 <div class="panel-content">

  For this feature to work correctly, the .user file must not be committed to source control.
</div>
</div>

* **Sitecore Web URL** – Contains the URL of the Sitecore instance TDS is connected to. This URL must be the ROOT of the Sitecore instance.
* **Sitecore Deploy Folder** – Contains the path to the ROOT of the Sitecore instance on the file system. This setting is used to install the TDS service when needed and to deploy the compiled code when the TDS project is built. 

<div class="panel">
 <div class="panel-header bg-lightBlue fg-white">
 NOTE
 </div>
 <div class="panel-content">
TDS uses standard windows file operations to copy files to Sitecore. Therefore, the identity of the process executing the TDS build must have write access to this folder for TDS to function correctly.
</div>
</div>

* **Recursive Deploy Action** – This setting controls how TDS responds to Sitecore items in the target Sitecore instance but not in the TDS project. By default, TDS will ignore any items in the target Sitecore instance. Changing this configuration setting will allow TDS to use an items deployment properties to determine if items in the target Sitecore instance can be deleted. For more information, please see deployment properties below.
* **Sitecore Access Guid** – Contains the Guid passed to the TDS service for all actions involving the service. This Guid must match the configured Guid in the service configuration file located at **/_DEV/web.config**. When setting up multiple TDS projects in a single solution, it is recommended that the Sitecore Access Guid be the same for each project configuration that is connected to a Sitecore instance.
* **Install Sitecore Connector** – When checked, TDS can install the Sitecore service permanently on the configured Sitecore instance. This is needed for the developer features of TDS to work correctly. In a configuration that is only used to build or deploy items, this can be left unchecked. If TDS needs to install the service, TDS will pick a random Access Guid at install time. 
* **Disable File Deployment** – Stops TDS deploying files to the directory specified in the **Sitecore Deploy Folder**.

**Sitecore Deploy Folder** should point at the location that the **Sitecore Web URL** is running from. If you select a folder that TDS does not think it is a Sitecore web root a warning symbol next the **Sitecore Deploy Folder**:

![](/Images/chapter4-deployfolder.png)  

Once you have set the **Sitecore Web Url, Sitecore Deploy Folder** and checked the **Install Sitecore Connector** field you can test your settings using the **Test** button:
 
![](/Images/chapter4-testbutton.png)  

Clicking the **Test** button will bring up a second prompt that will automatically check that you have configured you TDS project correctly:

![](/Images/chapter4-testdialog.png)  

#### Update Package 
Contains the settings needed to build Sitecore Update Packages. 

<div class="panel">
 <div class="panel-header bg-lightBlue fg-white">
 NOTE
 </div>
 <div class="panel-content">
TDS generates Sitecore Update Packages. These packages are not the same as the packages generated with the Package Builder on the Sitecore Desktop. To install these packages, you need to use the Update Installation Wizard located at http://[site]/sitecore/admin/UpdateInstallationWizard.aspx.
</div>
</div> 

![](/Images/chapter4-updatepackage.png) 
 
* **Generate Package During Build** – Enables package generation for the selected build configuration.
* **Package Name** – The name of the package to generate.
* **Package Author** – Sets the author field in the generated package.
* **Package Publisher** – Sets the publisher field in the generated package.
* **Package Version** – Sets the version number in the generated package.
* **Package Readme** – Sets the readme field in the generated package.
* **Generate separate code and item packages** – When checked, the build will generate two separate update packages. These packages separate the output of the build into a package just for items, and another that contains only code. Breaking up the packages this way facilitates some more advanced deployment scenarios.
* Append the current date and time to the package name – When checked, the package name has the current date and time. This is sometimes useful for associating the package with a specific version or build.
* **Sitecore Assembly Path** – TDS needs to use the Sitecore Update Package Builder to create a package. To do this, TDS needs to know where to find the four Sitecore assemblies that make up the Package Builder. These are **Sitecore.Kernel.dll, Sitecore.Logging.dll, Sitecore.Update.dll** and **Sitecore.Zip.dll**. This path can be a relative, absolute or network path to these four Dlls.

#### File Replacement 
 
Allows the TDS project to be configured to automatically copy files into the build folder before deploying the built project. This is useful for managing environment specific configuration files. The File Replacement step runs after the web project has been built and copied, but before package generation and/or deployment to Sitecore.

<div class="panel">
 <div class="panel-header bg-lightBlue fg-white">
 NOTE
 </div>
 <div class="panel-content">
Many of the use cases for File Replacements have been superseded by the Configuration Transform feature that is now part of TDS 4.0.
</div>
</div>
 
![](/Images/chapter4-filereplacement.png) 

* **Type** – The type dropdown allows you to choose the type of the Source Location. If you choose "File", the individual file specified in the Source Location is copied to the Target location. Choosing "Folder" causes all items under the Source Location to be copied to the Target Location.
* **Source Location** – Specifies where to copy files from. The path can be relative to the project folder or an absolute path.
* **Target Location** – Specifies the location to copy files to. The path for the target location can be relative to the build output folder or an absolute path.


#### Validations

The Validations tab allows you turn on checks that TDS can perform on the project when it is built.

![](/Images/chapter4-validations.png) 
 
* **Enable Validators** – Turns on validation for this build configuration.
* **Validation Settings File Path** -  The path to the file containing the settings used by the validators.
* **Validators** – The list of validators that can be activated.
* **Action** – Determines if the selected validator should raise a build error or build warning.
* **Additional Properties** – Allows the setting of additional properties used by each validator, for example item path.

TDS supports the following validations:
* **Template Structure** – Validates that templates have only a single Standard Value template, field sections and sections only contain fields.
* **Should be Deploy Once** – Ensure that certain items are set to DeployOnce. The paths that the check will applied to can be configured in the Additional Propeties area.
* **Don't Sync Children** – Ensure that specific items don't have child synchronization set, this prevents the possible deletion of items. The paths that the check will applied to can be configured in the Additional Propeties area.
* **Ensure Parent Integrity** – Validates that the structure of the TDS project matches what will be deployed to Sitecore.
* **Should use .user file** -  TDS properties for DEBUG configurations should typically be stored in the .user file.
* **Prevent item by path** – Checks that items in the project are not found at or beneath the configured location.

### Deployment Properties

A TDS project contains many different types of Sitecore items. These items all serve different purposes in the Sitecore implementation, and it is likely they need to be treated differently at deployment time. Developers can easily manage how each Sitecore item in the TDS project is deployed through Deployment Properties.

Setting deployment properties can be time consuming. TDS was designed to help developers with this process by intelligently choosing default values for deployment properties. If an item is added under an existing item, TDS will set the new items deployment properties to have the same values as the parent item.

### Visual Studio Property Window

Deployment properties are managed for an individual item in the Visual Studio property window. The property window is opened by right-clicking on an item and selecting properties. It may also be opened by clicking on an item and pressing the F4 key. 

![](/Images/chapter4-properties.png) 

* **Child Item Synchronization** – Sometimes it is necessary to remove Items from Sitecore as part of a deployment. This property controls how TDS responds to Sitecore items in the target Sitecore that are not present in the Project. There are three choices for this property.
 * **NoChildSynchronization** – When this option is chosen, TDS will ignore any Sitecore items in the target Sitecore that are not in the TDS project.
 * **KeepAllChildrenSynchronized** – When this option is chosen, TDS will remove Sitecore items under the current item in the target Sitecore if the items don't exist in the TDS project. When set, this setting applies to the current item and all items under it.
 * **KeepDirectDescendantsSynchronized** – This option is very similar to **KeepAllChildrenSynchronized**. The main difference is that it applies to only the items directly under the current item, and will not be applied to items further down in the content tree.

<div class="panel">
 <div class="panel-header bg-lightBlue fg-white">
 NOTE
 </div>
 <div class="panel-content">
<p>
How items are removed from the project by the <strong>Child Item Synchronization</strong> settings are controlled by a project configuration setting on the Build property tab.
</p>
<p>
The <strong>Recursive Deploy Action</strong> setting determines the action TDS will take when an item should be removed. The default setting is to take no action, which effectively disables this feature. The recommended setting is "Move the item to the Sitecore Recycle Bin", which allows developers to easily recover from problems with these settings.
</p>
<p>
It is recommended that the Sitecore databases are backed up before beginning any deployment regardless of the <strong>Recursive Deploy Action</strong> setting.
</p>
</div>
</div>

* **Code Generation Template** – Allows the developer to specify a particular template to use for code generation with this item. See the Code Generation section for more information.
* **Custom Data** – metadata that will be passed to the code generator. See the Code Generation section for more information.
* **Deploy Always Fields** – In some cases, developers may want to deploy only a few fields for an item, and not the entire item. This is useful when a Sitecore item is acting as both taxonomy and content and the development team wants to update a field like insert options or permissions on the item.<br />![](/Images/chapter4-fields.png) <br /> When the developer edits the Deploy Always Field, the above dialog is opened. Any field on the item can be chosen to always be deployed from this dialog. This setting is only available if the item is set to Deploy Once (see Item Deployment below).
* **Exclude Item From** – This setting allows the developer to choose to exclude an item from a specific project configuration. This can be used to create test content items that the development team would use during development. The test items could be excluded from the production project configuration, preventing them from being deployed in that environment. This feature is very much like a conditional compilation directive in a code file.
* **File Name** – The name of the file that contains the item information on disk.
* **File System Alias** – The file system name to use when an items name is to long. This property is used to get around the file path limit in Windows by allowing the developer to specify a shorter name.
* **Full Path** – The full disk path to the file that contains the information about the item.
* **Item Deployment** – This setting determines if an item should be deployed to Sitecore based on its presence in the target Sitecore instance. 
 * **DeployOnce** – When this option is chosen, an item will not be overwritten during deployment. This is useful for setting up new sections of the content tree. A new section or meta-data could be created with the proper permissions and insert options during a deployment. Content editors can update the item and future deployments will not overwrite their changes.
 * **AlwaysUpdate** – When this option is chosen, the item will always be updated during deployment. This is normally used for Sitecore schema items like Templates, Layouts, Sublayouts and Renderings.
* **Namespace** – A custom namespace to use with code generation. See the code generation section for more information.
* **SitecorePath** – The path to the item within Sitecore.


### TDS Options Window

The TDS Options Window allows you to access global settings for TDS, these settings will apply across all Visual Studio instances.

To access the TDS Option Window click on the **Tools** menu then **Options**. **TDS Options** will be visible in the left hand list:
 
![](/Images/chapter4-options.png) 

#### General Options
 
![](/Images/chapter4-generaloptions.png) 

The following options are are available in the **General Options** screen:

* **Autorun Code Generation** – Indicates if code generation should automatically run when new items are added to a TDS project or an items custom properties / namespace change. Setting this value to false will required a developer to manually run code generation.
* **Autosave Project File** – When set to **true** the project file will automatically save when items are added to the TDS project file or items are synced.
* **Check for Updates** – When set to **true** TDS will check for updates when a solution is loaded and prompt the developer when an update is available.

#### Sync Window

![](/Images/chapter4-syncwindow.png) 

The Sync screen allows you to set a list of fields that should be ignored when comparing items. Items with differences only in these fields will not show up in the **Sync Window** as being different.

Checking the **Hide fields with the same value in the Sync Results** will stop fields with identical values from being displayed in the **Sync Window**, this can make it easier to compare items.

### Deployment Property Manager

The Deployment Property Manager allows developers to view and update deployment properties on many items at one time. This is a much more convenient way of managing deployment properties. 

The Deployment Property Manager can be opened by right-clicking on the TDS project or any Sitecore item in the Solution Explorer and choosing "**Deployment Property Manager**". This opens a window showing the **Exclude Items From, Child Item Synchronization** and **Item Deployment** properties for all the Sitecore items under the item selected in the Solution Explorer.

![](/Images/chapter4-propertymanager.png)  

For an explanation of the various options for each of the properties, please see the descriptions above. 

#### Keyboard Shortcuts

The Deployment Property Manager has the following keyboard shortcuts when you have selected an item(s):

| Key Combination |	Action |
| --- | --- |
| Shift + w | Current Config - Include |
| Shift + e	| Current Config – Exclude |
| Shift + s	| Child Sync – All Children |
| Shift + d	| Child Sync – Direct Descendants |
| Shift + f	| Child Sync – No sync |
| Shift + x	| Deploy – Always |
| Shift + c	| Deploy – Once |
<br />

### Adding Sitecore items to a project

TDS helps developers to manage their Sitecore items. To do this, the items the development team wants to manage must be brought into the TDS project. This can be done with the **Get Sitecore Items** dialog and the Sync Window (see below). 

The **Get Sitecore Items** dialog can be opened by right clicking on the TDS project or a Sitecore item in the Solution Explorer window. The dialog will show the Sitecore content tree. Developers can browse the tree and select items to bring into their project by using the check boxes to the left of the Sitecore item.

![](/Images/chapter4-getitems.png) 

The Get Sitecore Items dialog implements a number of features to make it easier to bring items into a project.
* Any items already in the project are shown with a light colored font. See "templates" and "content" in the sample image.
* If an item is selected in the tree, the dialog always selects all parent items.
* If an item in unselected in the tree, the dialog always unselects all child items.
* All items have a right click menu that allows the developer to select all child items.

<div class="panel">
 <div class="panel-header bg-lightBlue fg-white">
 NOTE
 </div>
 <div class="panel-content">
<p>
When an item has been selected using the right-click menu to select all child items, TDS will automatically set the <strong>Child Item Synchronization</strong> setting in the items to <strong>KeepAllChildrenSynchronized</strong>.
</p>
</div>
</div>

After selecting the items from the Sitecore content tree, the developer can click the "**Get Items**" button and the selected items will be added to the project.

<div class="panel">
 <div class="panel-header bg-lightBlue fg-white">
 NOTE
 </div>
 <div class="panel-content">
<p>
Correctly choosing the Sitecore items to bring into a project is very important. Adding the wrong items to a TDS project will make the project difficult to maintain and deploy. Please review the section Choosing which items to bring into a TDS project for guidelines on choosing which items to add to TDS.
</p>
</div>
</div>

### Updating Sitecore Items in a project

As a Sitecore implementation grows, developers will add or make changes to items in their Sitecore development environment. TDS offers developers a way to track these changes and bring them into their TDS project. This is done by using the Sync Window.

#### The Sync Window

To open the Sync Window, right click on the TDS project or any item in the Solution Explorer and select **Sync with Sitecore**,  the sync window will then begin comparing the item and its descendants in the TDS project to the Sitecore instance for the current project configuration.

When the compare process is complete, the sync window will show the items that are different between the project and Sitecore. You can compare just the select item by clicking **Sync this Item** instead of **Sync with Sitecore**.
 
![](/Images/chapter4-syncwindow1.png)

The Sync Window allows developers to inspect the differences between Sitecore and the TDS project and determine what to do about those changes. The developer may select individual items, or multi-select items using standard windows selection keys (<shift> and <ctrl>) and choose an operation to perform on the items. If an item is collapsed and selected, it will be assumed by the Sync Window that all items under the item are selected as well. Once the developer has selected the operation to perform on each item, they can click on "**Do Updates**" to perform the actions.

* A. If there is a difference between the TDS project and Sitecore, it will be noted here.
* B. The developer can select an action to perform by clicking on the text in this column and selecting the appropriate action from the dropdown. By default, TDS will always choose "No Action".
* C. The "**Make selected project items match Sitecore**" button causes all selected items to choose the action that would make the project items match the Sitecore items. 
* D. The "**Make selected Sitecore items match project**" button causes all selected items to choose the action that would make the Sitecore items match the project items.
* E. The "**Merge fields during update**" button causes a merge window to open when updating Sitecore. The merge window allows the developer to choose to update only selected field values instead of the whole item.
* F. The "**Hide fields with no changes**" check box causes the item differences pane in the lower half of the sync window to only show fields that are different.
* G. Highlights changes between the project and Sitecore. Missing fields are shown in red, different fields are blue.

<div class="panel">
 <div class="panel-header bg-lightBlue fg-white">
 NOTE
 </div>
 <div class="panel-content">
<p>
The Sync Window uses the **Child Item Synchronization** setting to determine if it should look for new items under an existing Sitecore item. This feature of TDS is an optimization to prevent large content trees that are not part of the TDS project from being scanned during a sync operation.
</p>
</div>
</div>
