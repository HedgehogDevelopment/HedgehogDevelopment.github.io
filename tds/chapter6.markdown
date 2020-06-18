---
title: Sitecore TDS - Code Generation
layout: TdsLayout
---

## Code Generation

Code generation is the process by which a data model and one or more templates are passed through a template engine. The model is transformed and the resulting output of this process would be code that can be compiled and used within your application.

![](/Images/Tds/chapter6-codegenprocess.png)

Sitecore TDS code generation is composed of models of the Sitecore items within your project, transformation templates and a template engine within Sitecore TDS. The process works by Sitecore TDS parsing each .item file within your project and passing it to a transformation template. Once all of the items have been transformed an additional template may be executed being passed a model representation of the project.

When an item changes, either by a sync or by Rocks, Sitecore TDS will call the transformation template to re-generate the appropriate items. At the end of each item generation event, Sitecore TDS runs a template that generates the "header" and then combines all the generated code files into a single code file. This code file is located in another project in your solution. It can be either a web application or a class library.

Right clicking on the Sitecore TDS project and choosing "Re-generate code for all items" will run the template against all .item files in your project.

### Data Models

There are four types of models available for the code generation process. These types are **ProjectHeader**, **SitecoreItem**, **SitecoreTemplate** and **SitecoreField**.

#### ProjectHeader

The ProjectHeader model is a representation of the Sitecore TDS project and the code generation settings. This model is used within the "Header Transformation File" as configured on the Code Generation settings of your Sitecore TDS project.

#### SitecoreItem

This model is the default representation of the Sitecore item within your Sitecore TDS project. It is also the basis for the other two Sitecore models.

#### SitecoreTemplate

This model represents a Sitecore template item. It has all of the properties of a SitecoreItem model in addition to a list of base template, fields and its path segments. If Sitecore TDS determines that the .item file represents a Sitecore template then this is the type of model that is passed to the T4 template.

#### SitecoreField

This model represents a Sitecore field item. It has all of the properties of a SitecoreItem model in addition to the type of field it is.

### Transformation Templates

The Text Template Transformation Toolkit (T4) is a template based code generation engine built into Visual Studio. A T4 text template is a text file, with a .tt extension, that contains a mixture of text blocks and control logic that can generate a text file. The control logic is written as fragments of C# or VB.NET code. The generated file can be text of any kind, such as a Web page, or a resource file, or program source code in any language.

#### Header Transformation File

The header transformation template is passed the ProjectHeader model. This transformation template is typically used to generate ‘using' statements or common code shared amongst the rest of the generated code.

## Item Transformation File

Each item in your project can be configured with a transformation template. In most cases, you don't want to run code generation for all .items, only your Sitecore templates. To allow you the most flexibility, an inheritance model for determining the T4 template exists. Each .item file has a property in the items property page that allows you to set a t4 template for that item and all its descendants. It can be overridden at any level.

### Sample Transformation Templates

Once code generation is enabled, a new folder will show up in the Sitecore TDS project within solution explorer. It is called "Code Generation Templates". Right click on this and choose "Add -> New Item…". You have 4 possible templates to start from. The "document" templates are provided to help you see what is available to you in the T4 templates. These will generate text output containing all the fields passed into the T4 template. They are a good place to start for seeing all the information provided. The other two are empty templates that you can use to start writing your own T4 transforms.

Sample T4 templates are available on GitHub and there is a link to them on the code generation property page. The sample templates cover different types of code generation scenarios, and provide a great way to see what a real code generation template looks like.

### Setup

#### Project Level Setup

To setup Code Generation follow the following steps:
1.	Open the Properties tabs of a Sitecore TDS Project
2.	Select the **TDS Code Generation** properties tab
3.	Check **Enable Code Generation**.
4.	Choose a target project where the generated file will be written.
5.	Name the target file where the generated code will sit. Make sure to give it an extension of .cs (assuming you are generating C#)
6.	Create the Header and Base Project Transform files.
7.	Set the Header and Base Project Transform files to use.

#### Creating Header and Base Project Transformation Files

Once code generation has been enabled on a project it is possible to add TT files to the Sitecore TDS project. After enabling Code Generation the **Code Generation Templates** node will appear in the Sitecore TDS  project:


![](/Images/Tds/chapter6-codegennode.png)

Right clicking on this node and select **Add > New Item**:

![](/Images/Tds/chapter6-codegennewitem.png)

This will open the Add New Item  dialog:

![](/Images/Tds/chapter6-codegendialog.png)

The dialog allows you to create the following file types:

* **Blank Template** – A blank TT file that contains no code, for use when building code generation from scratch.
* **Document Header Template** – Used to generate documentation about the items in Sitecore TDS. This file is used as the Header Transform File.
* **Document Item Template** – Used to generate documentation about the items in Sitecore TDS. This file is used as the Base Project Tranform File.
* **Header Template** – Contains scaffolding for creating custom Code Generated files. This file is used as the Header Transform File.
* **Item Template** – Contains scaffolding for creating custom Code Generated files. This file is used as the Base Project Tranform File.

### Item Level Properties

Item level properties allow a developer to override the global item settings. Properties set on an item are inherited by all items beneath the item being set.

* **Code Generation Template** - Allows a different code generation file to be set for items beneath the current item.
* **Custom Data** -We allow you to add custom metadata to be passed into the SitecoreItem model for each .item in the property page. This is useful for things such as:
 *  Ignoring items for code generation
 *  Controlling the generated output such as
  *  Generating an interface vs. a class
  *  Controlling access modifiers of classes or properties
  *  Controlling the names of the generate code
  *  Generating strongly typed properties on your classes.
* **Namespace** – Set a custom namespace for this item and all child items. This namespace will be from the root of the target project and does not include any parent or project namespaces.

### Namespaces

Sitecore TDS will automatically create namespaces based on where a template is within Sitecore. For example if the Sitecore TDS project is setup as below where T2 is a template:

![](/Images/Tds/chapter6-codegenname.png)

If the Namespace setting on the Code Generation tab has the value "MyNamespace" Sitecore TDS will generate the following Namespace:

	namespace TdsDemo.MyNamespace.sitecore.templates.TDS.Set2
	{
	    public partial interface IT2                    
	    {
	        string F2 { get; set; }
	    }
	}

The namespaces of individual items can be controlled as well. See the Item Level Properties section.
