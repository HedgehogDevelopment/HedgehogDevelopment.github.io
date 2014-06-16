---
title: Chapter 1
layout: TdsLayout
---

# Chapter 1 – Introduction

## Team Development for Sitecore (TDS)

Team Development for Sitecore (TDS) is a Sitecore developer productivity tool created by Hedgehog Development (http://www.hhogdev.com), a company that designs and develops customized applications and Web sites, and provides technology consulting services.  TDS is used by Hedgehog Development internally and by development teams around the globe.
TDS is a Visual Studio add-in that supports 2010, 2012 and 2013 versions.  Sitecore developers use Team Development for Sitecore to increase the productivity of the Sitecore software development process. TDS allows you to treat your Sitecore Items as you would .Net code, allowing you to bring your Sitecore items into your development lifecycle.

## How It Works

Team Development for Sitecore gives the Sitecore development team members the ability to use source control to keep track of all Sitecore items in a project. This provides the same tracking and accountability for changes to Sitecore items as you have with .NET code.  This solves the problem of having code in Visual Studio but the Sitecore items that represent this code elsewhere.  
TDS allows teams to put all Sitecore items and .Net code in a Source Control Management System (SCMS), providing one master repository of Sitecore changes and .Net code changes for a project.  The SCMS becomes the central integration point for teams allowing automation of deployment and additional control over releases.  Team members using TDS can work remotely or disconnected from the network and then sync and merge changes at a later date due to the shift in reliance on the SCMS and not a shared Sitecore database.
TDS works with all known SCMS that integrate with Visual Studio including Team Foundation Server, SVN, CVS, GIT, and Perforce. Since TDS stores Sitecore items in the file system as a project, TDS is also compatible with version control systems such as GIT that work directly with the file system. 
Having everything in a SCMS gives you one master repository for the project. The SCMS becomes the master and central integration point for all the code and Sitecore items. Even if you are a team of one, using a SCMS is the smart way to work, and provides many benefits, including:

* Complete accountability and audit trail for all changes to all Sitecore items and .NET code in a project – Without TDS the development team loses all accountability and audit trails for changes to Sitecore items.
* Easy, secure backups – All of your Sitecore items and code are stored in a single repository, meaning backups are easy to do, making your work safe. Without TDS, your backup and recovery procedures have to accommodate multiple developer databases.
* Option to work remotely or disconnected from the network – Developers can sync and merge changes at a later date to the SCMS.  This allows the developer to work independently without worrying about the conflicts than can be cause by sharing a single Sitecore database with other developers.
* Easily compare item changes from other developers – Without TDS you cannot view changes made by other members of the development team before integrating them into your local development environment.
* Ability to easily rollback to prior versions if there is a problem – Without an audit trail and item accountability, narrowing down a problematic item change is extremely time consuming.  With TDS, Sitecore items are brought into your SCMS, giving you a full history of each change to an item. This makes a rollback significantly easier to execute. 
* Faster, easier automatic merge of changes items – Without TDS the merging of item changes is an extremely labor intensive process. With TDS, your SCMS can do this automatically for you.
* Ability to leverage branching and other advanced source code management techniques on Sitecore items – Without TDS this is impossible.
* Helps get new developers up to speed quickly – TDS helps new developers on a team get up to speed quickly. The developer can install a clean Sitecore environment, get the latest code and Sitecore items from the SCMS and then easily deploy the entire project to the new Sitecore instance. With TDS, developers have the ability to easily see what other team members have been doing by reviewing the check-in comments. (Without TDS, each developer is dependent on coordinating and then packaging up changes with the entire team. We have even seen partners go so far as designing their projects so that developers each work in separate areas of a project to reduce the risk of collision. This is not the optimal way to work.)

## Why TDS works

Over the course of a project's life, the amount of time spent performing code deployments can be significant, and thus, the time savings of TDS can also be significant. Based on Hedgehog’s experience developing many small, medium and large Sitecore projects, we have compiled extensive statistics on the life cycle of Sitecore projects. From these statistics, we have created graphs detailing a hypothetical Sitecore project that runs for 30 weeks.
When development on a project starts, there is an immediate need to begin creating Sitecore items. As development progresses, the number of new items tends to taper off. Changes to existing items continue and eventually tapers off as well.
 
As more templates are added, the cost (time) to deploy the items rises. The cost of deployment is also influenced by the number of changes to the existing items. Since each environment (development, Quality Assurance (QA), User Acceptance (UAT) sometimes also called Integration, and Production) is different, the costs associated with creating a QA build doesn’t completely offset the cost of building a UAT or Production build. In addition, since each deployment is a manual process, the risk of differences being introduced between each environment rises.
 

Setting up an automated TDS build at the start of a project incurs a small cost in developer time, but once the initial project and build are created, there is minimal costs associated with maintaining them. Having an automated process also resolves the issue of differences between deployments and environments.
 
We have found TDS easily affords an 8%-15% decrease in costs (time) to develop a Sitecore solution regardless of the size of the project. A 10% savings over 30 weeks for a 3 person team is 9 weeks of gained productivity. If the average team member salary is $75k per year this represents approximately $13k in savings.

## Work Environments

While developing Sitecore solutions for our clients, Hedgehog Development reviewed a number of published Sitecore development methods. We decided that none of these addressed the real problem, which was tracking and deploying Sitecore items. We decided to develop our own development methodology. TDS is the result of that effort.

### Development Environment Before TDS

Before we developed TDS, we realized there were many manual steps our developers needed to perform to deploy their work to a server.
 
* First they must move their Sitecore items directly to the Sitecore Development database while simultaneously checking in their .NET code to the SCMS.
* Next, the developer has to communicate to the team that Sitecore items must be deployed to the target environment. They then have to package the Sitecore items, which involves:
	* The developer logging into the Sitecore Desktop
	* Running the Sitecore Package Designer
	* Selecting the items to include in the package
	* Building the package
* Now the .NET code must be dealt with (assuming that code deployment is not part of the Sitecore packaging process)
	* The developer performs a build
	* The code in the Build Output folder is zipped up and copied to the target server.
	* Zip file is extracted
* Finally the developer or release manager runs the Sitecore Installation wizard on target to install the Sitecore package.

These steps, while simple, became tedious and occasionally error prone.

### Development Environment Using TDS

One of the driving principals of building TDS was to allow developers to work with their Sitecore items much the same way they work with code. Developers have been working with SCMS and automated builds for years using code. We wanted to leverage these same tools when dealing with Sitecore items.

When a developer is using TDS, deploying their work to a server is much simpler.

* The developer checks their code and Sitecore items into the SMCM.
* The developer (or other team member) starts an automated build for the environment they wish to deploy to.