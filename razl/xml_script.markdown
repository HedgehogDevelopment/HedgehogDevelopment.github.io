---
title: Sitecore Razl - Scripts
layout: RazlLayout
---

# Sitecore Razl

## Sitecore Razl Script

Sitecore Razl allows the user to to create XML documents that define connections to Sitecore servers and the operations Sitecore Razl should perform on those servers. These can then be executed from the Command Prompt or build scripts.


### Command line parameters

The command line parameters Sitecore Razl accepts from the command line are as follows:

1. **/script** Specifies the path to the script file
2. **/TLS12** when passed the value "true", Sitecore Razl enables the TLS 1.2 protocol when communicating with the webserver

To run a Sitecore Razl script with TLS 1.2 enabled, use a command similar to:

    Razl.exe /script:Migrate.xml /TLS12:true

### Running a Sitecore Razl Script

A Sitecore Razl script can be run from the command line with the following parameter:

    Razl.exe /script:"{path to script file}"

The value {path to script file} should be replaced with the path to the XML file that contains the Sitecore Razl script to run, for example:

    Razl.exe /script:Migrate.xml
    Razl.exe /script:"c:\Site Migration\Razl.xml"

### Sitecore Razl Script XML

The XML for Sitecore Razl scripts is very simple and is made up of connections and operations, by combining connections with operations Sitecore Razl will perform tasks on the intended Sitecore instances. Below is an overview of the entire Sitecore Razl XML:

    <razl>
      <connection name="" readOnly ="" install="true|false">
        <url></url>
        <accessGuid></accessGuid>
        <database></database>
        <path></path>
	    <readThreads></readThreads>
	    <writeThreads></writeThreads>
      </connection>
      <connection name="">
        <url></url>
        <guid></guid>
        <database></database>
	    <readThreads></readThreads>
	    <writeThreads></writeThreads>
      </connection>
      <connection name="" preset="" />
      <operation name="CopyHistory" source="" target="">
        <parameter name="from">[date|integer days]</parameter>
        <parameter name="to">[date|integer days]</parameter>
        <parameter name="recycle">true|false</parameter>
        <parameter name="lightningMode">true|false</parameter>
        <parameter name="include">
          <value></value>
        </parameter>
        <parameter name="exclude">
          <value></value>
        </parameter>
      </operation>
      <operation name="CopyAll" source="" target="">
        <parameter name="itemId"></parameter>
        <parameter name="overwrite">true|false</parameter>
        <parameter name="lightningMode">true|false</parameter>
        <parameter name="continueOnError">true|false</parameter>
      </operation>
      <operation name="CopyItem" source="" target="">
        <parameter name="itemId"></parameter>
      </operation>
      <operation name="CopyVersion" source="" target="">
        <parameter name="itemId"></parameter>
        <parameter name="languageId"></parameter>
        <parameter name="versionNum">number or [blank]</parameter>
        <parameter name="folderType">shared, unversioned or [blank]</parameter>
        <parameter name="removeVersion">true|false</parameter>
      </operation>
      <operation name="DeleteItem" source="" target="">
        <parameter name="itemId"></parameter>
        <parameter name="recycle">true|false</parameter>
      </operation>
      <operation name="MoveItem" source="" target="">
        <parameter name="itemId"></parameter>
        <parameter name="newItemPath"></parameter>
        <parameter name="newParentId"></parameter>
      </operation>
      <operation name="SetFieldValue" source="" target="">
        <parameter name="itemId"></parameter>
        <parameter name="fieldId"></parameter>
        <parameter name="fieldName"></parameter>
        <parameter name="fieldValue"></parameter>
        <parameter name="languageId"></parameter>
        <parameter name="versionNum"></parameter>
      </operation>
      <operation name="SetPropertyValue" source="Sitecore7.local.master" target="Sitecore7.Local.Web">
        <parameter name="itemId"></parameter>
        <parameter name="propertyName">Template Id</parameter>
        <parameter name="propertyValue"></parameter>
      </operation>
    </razl>


### Sitecore Razl XML Connections

Connections define how Sitecore Razl should connect to a Sitecore instance. Connections can be fully defined in the XML or can be preset connections that have been defined in the Sitecore Razl GUI. The connection XML with all options looks like this:

	  <connection name="" readOnly="" install="true|false" preset="">
	    <url></url>
	    <accessGuid></accessGuid>
	    <database></database>
	    <path></path>
	    <readThreads></readThreads>
	    <writeThreads></writeThreads>
	  </connection>

Summary of attributes and elements:

* **connection** - Containing element for the connection definition
* **name** - The name of the connection. This will be used by operations to identify the connection they should use
* **install** - Indicates if the Sitecore Razl connector should be installed at the target location
* **preset** - The name of the pre-configured connection defined using the Sitecore Razl GUI
* **url** - The URL to the Sitecore instance. Must start with http or https.
* **accessGuid** - The Guid used by Sitecore Razl to access the Sitecore instance.
* **database** - The database on the Sitecore instance Sitecore Razl should interact with.
* **path** - The path to the Sitecore instance. Used when installing the Sitecore Razl service.
* **readThreads** - The number of threads to use while looking for differences in a copyAll operation. The default value is 4.
* **writeThreads** - The number of threads to use while copying differences in a copyAll operation. The default value is 4.

At least two connections should be defined in a Sitecore Razl script.

#### Defined Connections

A defined connection is a connection that has the URL, AccessGuid and Database   and name defined in the XML. The minimum XML required is:
  
	  <connection name="">
	    <url></url>
	    <accessGuid></accessGuid>
	    <database></database>
	  </connection>

Using a defined connection it is possible to install the Sitecore Razl service required by Sitecore Razl to communicate with Sitecore. The additional attribute install and the path element a required for this to work:

	<connection name="" install="true">
	    <url></url>
	    <accessGuid></accessGuid>
	    <database></database>
	    <path></path>
	</connection>

A connection can also be made read only by adding the readOnly attribute:

	<connection name="" readOnly="true">
	    <url></url>
	    <accessGuid></accessGuid>
	    <database></database>
	</connection>

#### Preset Connections

Preset connections are connections that have been defined in the Sitecore Razl GUI first. The XML for a preset connection is:

	<connection name="" preset="" />

The value for the preset connection should be save value shown in the Sitecore Razl Connections dropdown. For example if in the Sitecore Razl GUI the following connections are defined:

![](/Images/Razl/script1.PNG)

The configuration to use the **Awesome** connection would be:

	<connection name="" preset="Awesome" />

Preset connections can not be made read only from the XML or be installed by the XML, these tasks should be performed in the Sitecore Razl GUI.

### Operations

Operations define the actions that Sitecore Razl should perform. The basic XML structure for an operation is:
   
   <operation name="" source="" target="">
   </operation>

Summary of attributes and elements:

* **operation** - the containing element that defines an operation
* **name** - the name of the operation to perform. The supported values are CopyHistory, CopyAll, CopyItem
* **source** - the name of the connection that will act as the source for the operation. The name should match the connection name.
* **target** - the name of the connection that will act as the target for the operation. The name should match the connection name.

An operation can have 0 or more child parameters. Parameters have the following basic XML structures:

  	<parameter name=""></parameter>

Or
	  <parameter name="">
	       <value></value>
	       <value></value>
	  </parameter>

Summary of attributes and elements:

* **parameter** - the containing element that defines a parameter
* **name** - the name of the parameters. See individual operation definitions for support parameters.
* **value** - the element that contains the parameter value. A parameters can contain 0 or more values.

If a parameters contains a single value it is possible to define the parameter without a value element, e.g:

	<parameter name="example">a value</parameter>

If the parameters required multiple values these can be defined using the value child element:

	<parameter name="example">
	    <value>a value  1</value>
	    <value>a value  2</value>
	</parameter>

#### CopyHistory Operation

The CopyHistory operation will replay the actions recorded in the Sitecore history engine on one instance on another instance. The full XML for the CopyHistory operation is:

	  <operation name="CopyHistory" source="" target="">
	    <parameter name="from"></parameter>
	    <parameter name="to"></parameter>
	    <parameter name="recycle">true|false</parameter>
        <parameter name="lightningMode">true|false</parameter>
	    <parameter name="include">
	      <value></value>
	    </parameter>
	    <parameter name="exclude">
	      <value></value>
	    </parameter>
	  </operation>

Summary of parameters:

* **from** - the date from which Sitecore Razl should start copying the history. The date should be defined in the format yyyy-MM-ddThh:mm:ss, e.g. 2014-05-08T03:48:57. This parameter may also be an integer representing the number of days to look back in the history. This is a required parameter.
* **to** - the date which Sitecore Razl should stop copying the history. The date should be defined in the format yyyy-MM-ddThh:mm:ss, e.g. 2014-05-08T13:48:57. This parameter may also be an integer representing the number of days to look back in the history. This is an optional parameter.
* **recycle** - indicates what should happen to an item that is deleted by Sitecore Razl. If set to true the item is sent to the recycle bin on the target Sitecore instance, if set to false the item is removed from the Sitecore instance. Default value is true. This parameter is optional.
* **lightningMode** - Enables or disables lightning mode when moving items.
* **include** - the path to items to include when copying history. Only actions on items that exist beneath the defined paths will be performed on the target instance. Multiple paths can be defined. If this parameter is absent then all actions are performed. This parameter is optional.
* **exclude**  - the path to items to exclude when copying history. Actions on items that exist beneath the defined paths will be ignored. Multiple paths can be defined. If this parameter is absent then all actions are performed. Excludes take precedence over includes. This parameter is optional.

#### CopyItem Operation

The CopyItem operation will copy an item from the source Sitecore instance to the target Sitecore instance. The full XML for the CopyItem operation is:

	  <operation name="CopyItem" source="" target="">
	    <parameter name="itemId"></parameter>
	  </operation>

Summary of parameters:

* **itemId** - the ID of the item to copy. This parameter is required.

#### CopyAll Operation

The CopyAll operation will copy an item from the source Sitecore instance to the target Sitecore instance and all child items. The full XML for the CopyAll operation is:

	  <operation name="CopyAll" source="" target="">
	    <parameter name="itemId"></parameter>
	    <parameter name="overwrite">true|false</parameter>
        <parameter name="lightningMode">true|false</parameter>
	  </operation>

Summary of parameters:

* **itemId** - the ID of the item to start coping from. This parameter is required.
* **overwrite** - indicates if the operation should remove items that exist in the target instance but don’t exist in the source instance. If set to true items in the target instance that are missing in the source instance will be removed, if set to false  items in the target instance that are missing in the source instance are skipped.
* **lightningMode** - Enables or disables lightning mode when moving items.
* **continueOnError** - Default is false. If set to true, the CopyAll command will log the error and attempt to continue copying items.

### Logging
Sitecore Razl Script mode will output actions as they happen to the command prompt, this output can be piped to a text file if required.

If a log folder has been set in the Sitecore Razl GUI then Script mode will also write to the log folder.
