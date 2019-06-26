---
title: Chapter 5 - Sitecore TDS Documentation
layout: TdsLayout
---
# Sitecore TDS

## Chapter 5 – Sitecore TDS Builds and Deployment

In addition to giving developers the ability to track their Sitecore item changes with source control, Sitecore TDS allows Sitecore items to be deployed through standard build automation tools. This allows Sitecore implementations to benefit from the ease and reproducibility offered by automated builds much the same as other web implementations.

### Solution Configurations and Project Configurations

Sitecore TDS uses project configurations to represent different environments. Example environments could be Dev, QA, UAT and Prod. Each of these environments use different Sitecore instances installed in different locations. The project configurations can be set to deploy the Sitecore items and code to each of these environments or even to generate packages that can be deployed at a later date.

Project configurations are created and managed using the Visual Studio solution Configuration Manager. This is the standard way of managing configurations within Visual Studio. There are many articles available on the web that describe how solution configurations and project configurations are managed within Visual Studio. An in-depth explanation of these features is outside the scope of this document.

### Configuration File Transforms

Visual Studio 2010 introduced a new feature called configuration transforms. These transforms allow developers to specify small changes that convert the configuration file for one environment into a file appropriate for another environment. The assumption is that most of the configuration file is common to all environments and only minor changes are needed to the files between environments. A good example of the type of changes that are usually in a configuration transform are connection strings, folder paths or locations of external resources.

By default, Visual Studio only supports configuration transforms on the web.config file in the root folder. There are a number of add-on packages to Visual Studio that support configuration transforms on other configuration files. At Hedgehog Development, we use the Slow Cheetah add-on to allow configuration transforms on all configuration files in a project.

Sitecore TDS is aware of all of the configuration transforms in a project when it is being built. If Sitecore TDS sees a configuration file with a transformation for the current configuration during a build, Sitecore TDS will automatically apply the configuration transformation before deploying the file or adding it to a package.

<div class="panel">
  <div class="panel-header bg-lightBlue fg-white">
    NOTE
  </div>
  <div class="panel-content">
    Sitecore TDS uses the name of the configuration for the Sitecore TDS project to determine the configuration transform to apply, not the name of the configuration in the Web Project. It is a good practice to make sure the names of the configurations in the web project match the names of the configurations in the Sitecore TDS project.
  </div>
</div>

### Building Packages

Building and deploying Sitecore items directly to a server is a very good practice for internal test servers. It allows developers to quickly and easily integrate their changes with other developers and also gives the QA team faster access to application updates.

<div class="panel">
  <div class="panel-header bg-lightBlue fg-white">
    NOTE
  </div>
  <div class="panel-content">
    Although it is possible to setup a build with Sitecore TDS that allows one click deployment to a production server careful thought is required before implementing such a solution. Production deployments often require multiple steps to be performed ( e.g. taking backups, removing servers from load, content freezes) which can’t be accounted for in a single click deployment.
  </div>
</div>

Sitecore TDS can be configured to automatically build a Sitecore update package during the build. These packages can be deployed through automated scripts or by a separate deployment team, offering additional control over the deployment process. For more information on about how to configure a build to generate a package please see the **Update Package** property tab in the Sitecore TDS project property pages section.

### Sitecore TDS builds using cloud servers

Before Sitecore TDS version 5.5, the build server needed to have Sitecore TDS installed on it to build Sitecore TDS projects. This is no longer necessary. The Sitecore TDS build components can now be added to a project as a NuGet package. The NuGet package is available in the .zip that contains the Sitecore TDS install. 

#### Installing the NuGet build components package

If you wish to use the build components in the NuGet package on your build server, the TDS Nuget packages are available as private NuGet packages on the public **nuget.org** feed. You may add these components to your project using the following command in the NuGet command prompt:

    PM> Install-Package HedgehogDevelopment.TDS

To install a specific version please add the switch **-Version x.x.x.x ** where x.x.x.x represents the version of TDS you have installed.

**Please Note:** The TDS package is unlisted on the NuGet feed. You must explicitly add it using the above command, or place it in your own private feed. Once added to your projects, NuGet will recognize the package and check it for updates. 

When using the TDS NuGet packages, it is important that you keep the version of the NuGet package the same as the version of TDS you are running. This is needed because the TDS Add-in in visual studio works closely with the NuGet package. 

#### Licensing Sitecore TDS on the build server ###

The Sitecore TDS components need to validate your license at build time. The recommended way to pass the license information to the build server is through environment variables. The names and values for the environment variables are: 

-  **TDS_Owner** - The owner of the license. This value must exactly match the value you use to install Sitecore TDS.
-  **TDS_Key** - The license key supplied by Hedgehog Development.

Please do not include quotes or leading/trailing spaces in these values.

Adding these environment variables to your build process varies depending on the build server you are using.

<div class="panel">
 <div class="panel-header bg-lightBlue fg-white">
 NOTE
 </div>
 <div class="panel-content">

To ensure all Sitecore TDS features work correctly, it is important that the installed version of Sitecore TDS is the same version as the build components. Since the build component version is tied to the project, it is important that all team members use the same version of Sitecore TDS.