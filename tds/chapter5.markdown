---
title: Chapter 5 - TDS Documentation
layout: TdsLayout
---
# Team Development for Sitecore

## Chapter 5 – TDS Builds and Deployment

In addition to giving developers the ability to track their Sitecore item changes with source control, TDS allows Sitecore items to be deployed through standard build automation tools. This allows Sitecore implementations to benefit from the ease and reproducibility offered by automated builds much the same as other web implementations.

### Solution Configurations and Project Configurations

TDS uses project configurations to represent different environments. Example environments could be Dev, QA, UAT and Prod. Each of these environments use different Sitecore instances installed in different locations. The project configurations can be set to deploy the Sitecore items and code to each of these environments or even to generate packages that can be deployed at a later date.

Project configurations are created and managed using the Visual Studio solution Configuration Manager. This is the standard way of managing configurations within Visual Studio. There are many articles available on the web that describe how solution configurations and project configurations are managed within Visual Studio. An in-depth explanation of these features is outside the scope of this document.

### Configuration File Transforms

Visual Studio 2010 introduced a new feature called configuration transforms. These transforms allow developers to specify small changes that convert the configuration file for one environment into a file appropriate for another environment. The assumption is that most of the configuration file is common to all environments and only minor changes are needed to the files between environments. A good example of the type of changes that are usually in a configuration transform are connection strings, folder paths or locations of external resources.

By default, Visual Studio only supports configuration transforms on the web.config file in the root folder. There are a number of add-on packages to Visual Studio that support configuration transforms on other configuration files. At Hedgehog Development, we use the Slow Cheetah add-on to allow configuration transforms on all configuration files in a project.

TDS is aware of all of the configuration transforms in a project when it is being built. If TDS sees a configuration file with a transformation for the current configuration during a build, TDS will automatically apply the configuration transformation before deploying the file or adding it to a package.

<div class="panel">
  <div class="panel-header bg-lightBlue fg-white">
    NOTE
  </div>
  <div class="panel-content">
    TDS uses the name of the configuration for the TDS project to determine the configuration transform to apply, not the name of the configuration in the Web Project. It is a good practice to make sure the names of the configurations in the web project match the names of the configurations in the TDS project.
  </div>
</div>

### Building Packages

Building and deploying Sitecore items directly to a server is a very good practice for internal test servers. It allows developers to quickly and easily integrate their changes with other developers and also gives the QA team faster access to application updates.

<div class="panel">
  <div class="panel-header bg-lightBlue fg-white">
    NOTE
  </div>
  <div class="panel-content">
    Although it is possible to setup a build with TDS that allows one click deployment to a production server careful thought is required before implementing such a solution. Production deployments often require multiple steps to be performed ( e.g. taking backups, removing servers from load, content freezes) which can’t be accounted for in a single click deployment.
  </div>
</div>

TDS can be configured to automatically build a Sitecore update package during the build. These packages can be deployed through automated scripts or by a separate deployment team, offering additional control over the deployment process. For more information on about how to configure a build to generate a package please see the **Update Package** property tab in the TDS project property pages section.
