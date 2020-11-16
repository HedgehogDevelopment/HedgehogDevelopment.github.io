---
title: Sitecore Razl - Using Razl with Containers
layout: RazlLayout
---

## Using Razl with Containers
The growing populartiy of running Sitecore inside containers has introduced some potential issues for using Razl in a container environment. There are a number of ways to install the Razl connector in a container. These include:

- Install the connector as a package.
- Map a local folder to a folder in the container and use robocopy to move the files to the webroot.
- Build the connector into the container using a layered image.

The first two can work, but may have issues with scripts and permissions. This document will describe the steps needed to automatically build the connector into the container and use an environment variable to hold the Sitecore Access Guid.

### Creating the Razl Connection
When creating the Razl connection in the Razl Connection Manager, choose "Package Connection" as the type of connection, but don't download the connection .zip file and install it. Follow the instructions below to configure the container for Razl.

Once the container has been configured, click "Test Connection" and procede through the wizard to complete the connection.

### Building the Razl Connector into docker-compose containers
This document assumes you are using a docker-compose environment similar to the docker-compose templates provided by the **sitecore.aspnet.gettingstarted** dotnet template. Since each container environment is potentally different, you may not be able to follow this document exactly.

The Razl Connector is typically installed on the CM server, but can actually be installed on any ASP.Net web server in the container. This document will show how to update the docker configuration for the CM and to configure docker-compose to use the updated configuration to build the connector into the environment.

#### Editing the Docker configuration for the CM
The docker-compose environment for the sitecore.aspnet.gettingstarted template has a Docker file for each server located in a folder called /docker/build/[server]. The Docker configuration file for the CM is located in the folder /docker/build/cm/Dockerfile and should look something like:

    # escape=`

    ARG PARENT_IMAGE
    ARG SOLUTION_IMAGE
    ARG TOOLS_IMAGE
    ARG MANAGEMENT_SERVICES_IMAGE
    ARG HEADLESS_SERVICES_IMAGE

    FROM ${SOLUTION_IMAGE} as solution
    FROM ${TOOLS_IMAGE} as tools
    FROM ${MANAGEMENT_SERVICES_IMAGE} AS management_services
    FROM ${HEADLESS_SERVICES_IMAGE} AS headless_services
    FROM ${PARENT_IMAGE}

    SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

    WORKDIR C:\inetpub\wwwroot

    # Copy developer tools and entrypoint
    COPY --from=tools C:\tools C:\tools

    # Copy the Sitecore Management Services Module
    COPY --from=management_services C:\module\cm\content C:\inetpub\wwwroot

    # Copy and init the JSS / Headless Services Module
    COPY --from=headless_services C:\module\cm\content C:\inetpub\wwwroot
    COPY --from=headless_services C:\module\tools C:\module\tools
    RUN C:\module\tools\Initialize-Content.ps1 -TargetPath C:\inetpub\wwwroot; `
        Remove-Item -Path C:\module -Recurse -Force;

    # Copy solution website files
    COPY --from=solution /artifacts/sitecore/ ./

There are three changes to the Dockerfile needed to install the Razl components from the Razl Connection Image:

1. Provide a parameter with the Razl component location
2. Add the image with the Razl components
3. Copy the components from the image into the CM

Having the Razl component location as a parameter allows the component location to be easily updated. This is accomplished by adding the line **ARG RAZL_CONNECTION_IMAGE** after the last argument:

    ARG PARENT_IMAGE
    ARG SOLUTION_IMAGE
    ARG TOOLS_IMAGE
    ARG MANAGEMENT_SERVICES_IMAGE
    ARG HEADLESS_SERVICES_IMAGE
    ARG RAZL_CONNECTION_IMAGE

Next, we need to include the image into the docker configuration using the command **FROM ${RAZL_CONNECTION_IMAGE} as razl**. This can be anywhere in the list of named images. In this example, it will be first, but if the user wishes to setup multiple configurations for the CM, it can be located elsewhere:

    ARG PARENT_IMAGE
    ARG SOLUTION_IMAGE
    ARG TOOLS_IMAGE
    ARG MANAGEMENT_SERVICES_IMAGE
    ARG HEADLESS_SERVICES_IMAGE
    ARG RAZL_CONNECTION_IMAGE

    FROM ${RAZL_CONNECTION_IMAGE} as razl
    FROM ${SOLUTION_IMAGE} as solution
    FROM ${TOOLS_IMAGE} as tools
    
The last step is to copy the Razl components from the Razl image into the container. This is done using the copy command **COPY --from=razl c:\RazlService c:\inetpub\wwwroot**. This copy command can be anywhere in the list of copy commands. This final Dockerfile should look something like:

    # escape=`

    ARG PARENT_IMAGE
    ARG SOLUTION_IMAGE
    ARG TOOLS_IMAGE
    ARG MANAGEMENT_SERVICES_IMAGE
    ARG HEADLESS_SERVICES_IMAGE
    ARG RAZL_CONNECTION_IMAGE

    FROM ${RAZL_CONNECTION_IMAGE} as razl
    FROM ${SOLUTION_IMAGE} as solution
    FROM ${TOOLS_IMAGE} as tools
    FROM ${MANAGEMENT_SERVICES_IMAGE} AS management_services
    FROM ${HEADLESS_SERVICES_IMAGE} AS headless_services
    FROM ${PARENT_IMAGE}

    SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

    WORKDIR C:\inetpub\wwwroot

    # Copy Razl connector files
    COPY --from=razl c:\RazlService c:\inetpub\wwwroot

    # Copy developer tools and entrypoint
    COPY --from=tools C:\tools C:\tools

    # Copy the Sitecore Management Services Module
    COPY --from=management_services C:\module\cm\content C:\inetpub\wwwroot

    # Copy and init the JSS / Headless Services Module
    COPY --from=headless_services C:\module\cm\content C:\inetpub\wwwroot
    COPY --from=headless_services C:\module\tools C:\module\tools
    RUN C:\module\tools\Initialize-Content.ps1 -TargetPath C:\inetpub\wwwroot; `
        Remove-Item -Path C:\module -Recurse -Force;

    # Copy solution website files
    COPY --from=solution /artifacts/sitecore/ ./

#### Configuring the docker-compose.override.yml to install the Razl Connector
Since the location of the connector is a parameter, the docker-compose file needs to be updated to pass the parameter. The typical CM configuration in the .override file looks something like this:

      # Use our custom CM (XP0 Standalone) image with added modules and solution code.
      # Folders are mounted below for code deployment and log output. See Dockerfile for details.
      # Configure for a mounted license file instead of using SITECORE_LICENSE.
      cm:
        image: ${REGISTRY}${COMPOSE_PROJECT_NAME}-xp0-cm:${VERSION:-latest}
        build:
          context: ./docker/build/cm
          args:
            PARENT_IMAGE: ${SITECORE_DOCKER_REGISTRY}sitecore-xp0-cm:${SITECORE_VERSION}
            SOLUTION_IMAGE: ${REGISTRY}${COMPOSE_PROJECT_NAME}-solution:${VERSION:-latest}
            TOOLS_IMAGE: ${TOOLS_IMAGE}
            MANAGEMENT_SERVICES_IMAGE: ${MANAGEMENT_SERVICES_IMAGE}
            HEADLESS_SERVICES_IMAGE: ${HEADLESS_SERVICES_IMAGE}
        depends_on:
          - solution
        volumes:
          - ${LOCAL_DEPLOY_PATH}\platform:C:\deploy
          - ${LOCAL_DATA_PATH}\cm:C:\inetpub\wwwroot\App_Data\logs
          - ${HOST_LICENSE_FOLDER}:c:\license
        environment:
          SITECORE_LICENSE_LOCATION: c:\license\license.xml
        entrypoint: powershell.exe -Command "& C:\tools\entrypoints\iis\Development.ps1"

There are two changes needed to support razl. The Razl connection image needs to be passed and the Razl Access Guid needs to be specified as an environment variable. The connect image arg is done by adding **RAZL_CONNECTION_IMAGE: ${RAZL_CONNECTION_IMAGE}** to cm/build/args. The Razl Access Guid is added to the environment variables by adding **RAZL_AccessGuid: ${RAZL_ACCESS_GUID}** to cm/environment. The final configuration of the CM in the docker-compose.override.yml looks something like:

      # Use our custom CM (XP0 Standalone) image with added modules and solution code.
      # Folders are mounted below for code deployment and log output. See Dockerfile for details.
      # Configure for a mounted license file instead of using SITECORE_LICENSE.
      cm:
        image: ${REGISTRY}${COMPOSE_PROJECT_NAME}-xp0-cm:${VERSION:-latest}
        build:
          context: ./docker/build/cm
          args:
            PARENT_IMAGE: ${SITECORE_DOCKER_REGISTRY}sitecore-xp0-cm:${SITECORE_VERSION}
            SOLUTION_IMAGE: ${REGISTRY}${COMPOSE_PROJECT_NAME}-solution:${VERSION:-latest}
            TOOLS_IMAGE: ${TOOLS_IMAGE}
            MANAGEMENT_SERVICES_IMAGE: ${MANAGEMENT_SERVICES_IMAGE}
            HEADLESS_SERVICES_IMAGE: ${HEADLESS_SERVICES_IMAGE}
            RAZL_CONNECTION_IMAGE: ${RAZL_CONNECTION_IMAGE}
        depends_on:
          - solution
        volumes:
          - ${LOCAL_DEPLOY_PATH}\platform:C:\deploy
          - ${LOCAL_DATA_PATH}\cm:C:\inetpub\wwwroot\App_Data\logs
          - ${HOST_LICENSE_FOLDER}:c:\license
        environment:
          SITECORE_LICENSE_LOCATION: c:\license\license.xml
          RAZL_AccessGuid: ${RAZL_ACCESS_GUID}
        entrypoint: powershell.exe -Command "& C:\tools\entrypoints\iis\Development.ps1"

Since the image location and access guid are also parameterized, the environment needs to be updated as well.

#### Updating the Environment variables for the Razl Connector
The .env file is used to configure environment variables for the docker-compose command. The following lines need to be added to the environment file to enable the Razl connector using the configuration settings specified above.

    RAZL_CONNECTION_IMAGE=scr.sitecore.com/tools/sitecore-razl-assets:[Razl Version]-1809
    RAZL_ACCESS_GUID=0000000-1111-2222-3333-444444444444

The **[Razl Version]** in the RAZL_CONNECTION_IMAGE should be replaced with the version of the connnector the developer wishes to install in the environment. The format of the version is typically *Major*.*Minor*.*Release*. e.g. 5.0.1
