---
title: TDS Documentation
layout: TdsLayout
---
 
# Team Development for Sitecore 

## About TDS

TDS (Team Development for Sitecore), a Microsoft Visual Studio Plugin, brings Sitecore items into Visual Studio while reducing developer’s deployment time to almost zero.  
By using TDS, developers can improve control and overall team performance by integrating Source Code Control into Sitecore and Visual Studio projects.  
TDS allows new developers to be easily added to a project. New developers can get the most recent updates from the Source Code Control and begin making 
updates to the project almost immediately.  TDS eliminates the need for manually tracking item changes for deployment, since all changes are automatically 
tracked by source control.  TDS features continuous builds and fully automated deployment releases.  TDS allows Sitecore items to be moved in and out of a 
Sitecore instance within Microsoft Visual Studio.  TDS helps keep track of changes by allowing the developer to quickly compare their project items to their developer 
instance of Sitecore.  Because of all this, TDS significantly increases the ability for developers to work in teams, and saves time, money, and a good deal of 
frustration in the long run. 

### Acknowledgements

Development team: Charlie Turano, Sean Kearney, Matt Friedlander, Elena Zlateva, Petko Kamburov, Steven Striga, Mike Edwards 

## Contents

* [Chapter 1 – Introduction](./chapter1.html)
	* Team Development for Sitecore (TDS)	6
	* How It Works	6
	* Why TDS works	7
	* Work Environments	9
		* Development environment before TDS	9
		* Development environment using TDS	10
* Chapter 2 – Getting started with TDS	10
	* System Requirements	10
	* Installation	10
		* Step-by-Step Instructions	12
		* Updating the TDS License	15
	* Initial Configuration	15
		* Create the TDS Project	16
		* Connect the TDS Project to Sitecore	17
		* Adding Sitecore items to the TDS Project	18
		* Choosing which items to bring into a TDS project	19
	* TDS Project Types	20
		* TDS Project	21
		* TDS Project with Wizard	21
* Chapter 3 – TDS Architecture	22
	* TDS Add-in	22
	* TDS Web Service	22
* Chapter 4 – Using TDS for Sitecore Development	23
	* The Sitecore database(s)	24
	* Working outside the web root	24
	* Solution Structure	24
	* TDS project property pages	26
		* General	26
		* Code Generation	28
		* Multi-project Properties	29
		* Build	31
		* Update Package	34
		* File Replacement	36
		* Nuget Package	37
		* Validations	41
	* Deployment Properties	42
	* Visual Studio Property Window	42
	* TDS Options Window	45
		* General Options	46
		* Sync Window	47
	* Deployment Property Manager	47
	* Adding Sitecore items to a project	49
	* Updating Sitecore Items in a project	50
		* The Sync Window	50
		* The Merge Window	53
		* Renaming items	54
		* Moving items	54
	* Global Config	54
	* Sitecore Rocks	56
		* Setting up Rocks and TDS	56
		* Getting items using Rocks	57
		* TDS and Sitecore upgrades	57
* Chapter 5 – TDS Builds and Deployment	58
	* Solution Configurations and Project Configurations	58
	* Configuration File Transforms	58
	* Building Packages	59
* Chapter 6 – Code Generation	59
	* vData Models	60
		* ProjectHeader	60
		* SitecoreItem	60
		* SitecoreTemplate	60
		* SitecoreField	61
	* Transformation Templates	61
		* Header Transformation File	61
		* Item Transformation File	61
	* Sample Transformation Templates	61
	* Setup	62
		* Project Level Setup	62
		* Creating Header and Base Project Transform Files	62
	* Item Level Properties	63
	* Namespaces	64
