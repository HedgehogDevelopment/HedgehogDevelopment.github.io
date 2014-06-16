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

