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

In the example above, there is a \Lib folder in the file system. This contains any reference DLL's needed to build the project. By keeping all resources needed for the project under a single folder, the development team can easily leverage advanced source control features like branching, merging and labeling. Additionally, this structure lends itself to setting up automated builds.

### TDS project property pages

The TDS project property pages are used to connect the TDS project to a Sitecore instance and to control how the TDS project interacts with other projects in the solution during the build. 

#### General

Contains settings that are common to all project configurations.

![](/Images/chapter4-general.png) 

* **Source Web Project** – This dropdown selects the web project to copy to Sitecore when the TDS project is built. This may be set to <None> if there is no need to copy files to Sitecore.
* **Source Web Physical Path** – For information only. This shows the path to the web project.
* **Source Web Virtual Path** – For information only. This shows the path within the solution to the web project.
* **Sitecore Database** – Configures the Sitecore database the TDS project will use.
* **Assemblies** – When deploying to Sitecore, TDS can skip the deployment of certain assemblies. These assemblies may be referenced by one or more projects in the solution. Excluding/including static assemblies from the build will reduce the size of the packages TDS generates and improve deployment time. By default, TDS excludes assemblies beginning with "Sitecore.". Selecting **Exclude** from the dropdown will cause TDS to skip these files and not add them to the deployment. Selecting **Include** from the dropdown will only include the files listed and cause TDS to skip all the files not listed.

#### Code Generation
 
Used to turn on and control TDS Code Generation. 
 
![](/Images/chapter4-codegeneration.png)

* **Target Project** – The target project in which the generated code file will be generated.
* **Code Generation Target File** – the name of the file that will contain the generated code. Remember to add the appropriate extension, e.g. “.cs” for c-sharp files.
* **Base Namespace** – The namespace that class will be generated in.
* **Header Transform File** – The TT file used to generate the header of the generated file.
* **Base Project Transform File** – The TT file used to generate output for each item in the generated file.
* **Sitecore Fields to Pass to Code Generation** – Standard Sitecore fields that should be passed to the code generation template. By default standard Sitecore fields are skipped but developer created fields are always passed to the code generator.

Please see the code generation section below for more information on the Code Generation property page.

#### Multi-Project Properties

The Multi-Project properties page allow you to setup dependencies between projects within the same solution.

![](/Images/chapter4-multiproject.png)

