---
title: Razl - Scripts
layout: RazlLayout
---

# Razl

## Razl Script

Start from version 2.1 of Razl it is possible to create XML documents that define the connections and operations Razl should perform. These can then be executed from the Command Prompt or build scripts.

### Running a Razl Script

A Razl script can be run from the command line with the following parameters:

    Razl.exe /script:"{path to script file}"

The value {path to script file} should be replaced with the path to the XML file that contains the Razl script to run, for example:

    Razl.exe /script:Migrate.xml
    Razl.exe /script:"c:\Site Migration\Razl.xml"

### Razl Script XML

The XML for Razl is very simple and is made up primarily of connections and operations, by combining connections with operations Razl will perform tasks on the intended Sitecore instances. Below is an overview of the entire Razl XML:

	<razl>
	  <connection name="" readOnly ="" install="true|false" preset="">
	    <url></url>
	    <accessGuid></accessGuid>
	    <database></database>
	    <path></path>
	  </connection>
	  <operation name="CopyHistory" source="" target="">
	    <parameter name="from"></parameter>
	    <parameter name="recycle">true|false</parameter>
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
	  </operation>
	  <operation name="CopyItem" source="" target="">
	    <parameter name="itemId"></parameter>
	    <parameter name="overwrite">true|false</parameter>
	  </operation>
	</razl>

### Razl XML Connections

Connections define how Razl should connect to a Sitecore instance. Connections can be fully defined in the XML or can be preset connections that have been defined in Razl GUI previously. The connection XML with all options looks like this:

	  <connection name="" readOnly ="" install="true|false" preset="">
	    <url></url>
	    <accessGuid></accessGuid>
	    <database></database>
	    <path></path>
	  </connection>

Summary of attributes and elements:

* **connection** - containing element for the connection definition
* **name** - the name of the connection. This will be used by operations to identify the connection they should use
* **install** - indicates if the Razl connector should be installed at the target location
* **preset** - the name of the pre-configured connection defined using the Razl GUI
* **url** - the URL to the Sitecore instance. Must start with http or https.
* **accessGuid** - the Guid used by Razl to access the Sitecore instance.
* **database** - the database on the Sitecore instance Razl should interact with.
* **path** - the path to the Sitecore instance. Used when installing the Razl service.

At least two connections should be defined in a Razl script.

#### Defined Connections

A defined connection is a connection that has the URL, AccessGuid and Database   and name defined in the XML. The minimum XML required is:
  
	  <connection name="">
	    <url></url>
	    <accessGuid></accessGuid>
	    <database></database>
	  </connection>

Using a defined connection it is possible to install the Razl service required by Razl to communicate with Sitecore. The additional attribute install and the path element a required for this to work:

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

Preset connections are connections that have been defined in the Razl GUI first. The XML for a preset connection is:

	<connection name="" preset="" />

The value for the preset connection should be save value shown in the Razl Connections dropdown. For example if in the Razl GUI the following connections are defined:

![](/Images/Razl/script1.PNG)

The configuration to use the **Awesome** connection would be:

	<connection name="" preset="Awesome" />

Preset connections can not be made read only from the XML or be installed by the XML, these tasks should be performed in the Razl GUI.

### Operations

Operations define the actions that Razl should perform. The basic XML structure for an operation is:
   
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
	    <parameter name="include">
	      <value></value>
	    </parameter>
	    <parameter name="exclude">
	      <value></value>
	    </parameter>
	  </operation>

Summary of parameters:

* **from** - the date from which Razl should start copying the history. The date should be defined in the format yyyy-MM-ddThh:mm:ss, e.g. 2014-05-08T03:48:57. This parameter is required.
* **to** - the date which Razl should stop copying the history. The date should be defined in the format yyyy-MM-ddThh:mm:ss, e.g. 2014-05-08T13:48:57. This parameter is optional.
* **recycle** - indicates what should happen to an item that is deleted by Razl. If set to true the item is sent to the recycle bin on the target Sitecore instance, if set to false the item is removed from the Sitecore instance. Default value is true. This parameter is optional.
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
	  </operation>

Summary of parameters:

* **itemId** - the ID of the item to start coping from. This parameter is required.
* **overwrite** - indicates if the operation should remove items that exist in the target instance but don’t exist in the source instance. If set to true items in the target instance that are missing in the source instance will be removed, if set to false  items in the target instance that are missing in the source instance are skipped.

### Logging
Razl Script mode will output actions as they happen to the command prompt, this output can be piped to a text file if required.

If a log folder has been set in the Razl GUI then Script mode will also write to the log folder.
