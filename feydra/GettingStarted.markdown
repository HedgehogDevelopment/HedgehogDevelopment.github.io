---
title: Sitecore Feydra - Getting Started
layout: FeydraLayout
---

# Sitecore Feydra Getting Started

## The Virtual Sandbox - How it works
Sitecore Feydra allows any MVC web application to host front-end development by creating virtual 
sandboxes for each front-end developer.  A virtual sandbox is a virtualized environment 
in which front-end assets (css, js, cshtml, etc.) can be selectively replaced without 
disturbing the back-end functionality of the web application. This virtualization allows 
back-end developers to create **stubs** for front-end functionality without having the actual 
front-end assets available at development time. The front-end developers can hook-up the 
components as they become available without impacting back-end development.

Sitecore Feydra also greatly improves front-end developers’ ability to maintain and update their 
portion of the web application. If there are issues with the front-end functionality of 
the site, a front-end developer can easily update the front-end assets in their virtual 
sandbox and test fixes against a working web application; all without the overhead of 
maintaining a full Sitecore development environment or MVC application.

Ultimately, Sitecore Feydra is designed to allow front-end developers to use their preferred 
development environment; make their changes in a virtual sandbox and test by pushing 
their changes to a shared location (File share, FTP, etc.) using standard tools.

## Installation with NuGet
Sitecore Feydra is distributed as a .zip of NuGet packages. These packages can be added to a local 
NuGet feed to make them accessible to developers and the build process.

To install Sitecore Feydra, simply add the NuGet package **Hedgehog.Feydra** to a web application 
and the Sitecore Feydra assembly is automatically installed. If the developer is using Sitecore, 
add the NuGet package **Hedgehog.Feydra.Sitecore** to the web application.

The MVC core of Sitecore Feydra consists of a single assembly called **Hedgehog.Feydra.dll**. If 
this file is present in the **/bin** folder of a website, Sitecore Feydra will be available on that 
server. Deleting this file will remove Sitecore Feydra.

The Sitecore components of Sitecore Feydra consist of two additional files. These are 
**Hedgehog.Feydra.SC.dll** and **Z_Feydra.config**. These are installed in the **/bin** and 
**/App_Config/Include** folders, respectively.

## Installation without NuGet
To install Sitecore Feydra without using NuGet, extract the files from the NuGet packages and place the 
files in the folders specified in the table below:

| File | Folder | 
| ---- | ------ | 
| Hedgehog.Feydra.dll Hedgehog.Feydra.SC.dll | \bin | 
| Z_Feydra.config | /App_Config/Include | 

## Deployment
Sitecore Feydra needs to be deployed on the servers where the front-end developers are going to 
be updating front-end assets. This can be any server capable of running the web 
application. We recommend using a server that is not used for CI builds, since the 
build/deployment process will interfere with the front-end developer testing.

Sitecore Feydra doesn’t support load balanced servers. Load balanced servers are typically not 
needed in a development environment, so this should not be a major problem.

The Sitecore Feydra assemblies and configuration files should not be deployed to a production 
server.

## Configuration

Sitecore Feydra needs to create a few folders on the web server for proper operation. In most cases, 
Sitecore Feydra can create these folders automatically. Sitecore Feydra will display an error message if it 
does not have permission to create the folders during the initialization process. Granting the 
permission to create/write to the folders specified in the Sitecore Feydra error messages will resolve 
the startup errors. If this is not possible because of infrastructure restrictions, you need 
to create the folders Sitecore Feydra requires as part of your deployment process.

The following is a list of the folders used by Sitecore Feydra:

| File/Folder | Comments| 
| ---- | ------ | 
| ~/App_Data/Feydra | This folder stores all Sitecore Feydra data (Users, Licenses, Logs, etc.). Sitecore Feydra must be able to write to this folder. Overwriting or removing this folder at deployment time will remove any users or licenses installed in Sitecore Feydra.  | 
| ~/Areas/Feydra | Sitecore Feydra uses this folder to store the **web.config** file needed for the Sitecore Feydra views. Sitecore Feydra creates the **web.config** file at initialization time, and therefore, Sitecore Feydra needs write access to this folder. | 
| ~/App_Data/Feydra/*.dat | Any data files (.dat extension) files in this folder must be writable for Sitecore Feydra to function correctly. |
| ~/FeydraRoot | This is the location of the users Virtual Sandboxes. This folder must be writable for Sitecore Feydra to function correctly. The front-end developers must also be able to write files to this folder using a file share or FTP protocol. <br/> <br/> Creating a new user will cause Sitecore Feydra to create a user’s Virtual Sandbox as a folder under the FeydraRoot folder. |

## Setup
Once Sitecore Feydra is installed on a server, Sitecore Feydra will verify the environment and display 
error messages indicating any problems found on the server that would prevent Sitecore Feydra 
from functioning correctly. The following is a list of requirements Feydra will check 
at startup:

- There is a folder called **FeydraRoot** in the root of the website. If the folder 
doesn’t exist, Sitecore Feydra will try to add it. Sitecore Feydra will report a problem if the folder 
cannot be created.
- The Web Server needs write rights to **FeydraRoot**.
- There must be a folder called **/App_Data/Feydra**.  If the folder doesn’t exist, 
Sitecore Feydra will try to add it. Sitecore Feydra will report an error if the folder cannot be created.
- The Web Server needs write rights to **/App_Data/Feydra** and all files in that folder.
- The Web Server needs write rights to a folder called **/Areas/Feydra**.
- The property **runAllManagedModulesForAllRequests** must be set on the 
**/configuration/modules** element in the **web.config**.
