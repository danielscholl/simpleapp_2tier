# Simple Demo Code Base for a 2 Tier Deployment

[![Build Status](https://cloudcodeit.visualstudio.com/DemoStuff/_apis/build/status/danielscholl.simpleapp_2tier)](https://cloudcodeit.visualstudio.com/DemoStuff/_build/latest?definitionId=25)

This is a simple 2 Tier Code Sample that connects to a SQL Database and retrieves some records, then displays them on a web page.  The purpose of this code sample is to workload options for running a 2 Tier App.

- Web Tier  (DotNet Core MVC Website)
- DB Tier   (SQL Datatbase with a single table)

 ## Infrastructure Architecture (2 Tier PaaS)

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdanielscholl%2Fsimpleapp_2tier%2Fmaster%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

![[0]][0]

```powershell
# Manually Deploy via CLI
$ResourceGroup = "simpleapp"
az group create --location eastus --name $ResourceGroup
az group deployment create --name simpleapp_2tier `
 --template-file azuredeploy.json `
 --resource-group $ResourceGroup
```

## Instructions to run locally on a Developer Workstation as code.

__Requirements:__

1. [DotNet Core](https://docs.microsoft.com/en-us/dotnet/core/about)

    ```powershell
    dotnet --version

    ## Result
    2.1.400
    ```

2. [LocalDB](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017)  

    ```powershell
    SQLLocalDB

    ## Result   
    Microsoft (R) SQL Server Express LocalDB Command Line Tool
    Version 13.0.1601.5
    ...
    ```

> Note: SQL can be run in a Container if desired see README.md in Database Folder for Directions

__Installation:__

To install or run the app locally simply clone the repo locally and follow the instructions.

```powershell
# Restore and Build
dotnet restore
dotnet build

# Initiate a LocalDB Database
cd SimpleApp
dotnet ef database update
cd ..

# Execute Test Cases
cd SimpleApp.Tests
dotnet test
cd ..

# Run the App
dotnet run --project SimpleApp
```

## Instructions to run locally on a Developer Workstation using docker.

__Requirements:__

1. [Docker](https://www.docker.com/get-started)

```powershell
docker --version
docker-compose --version


## Result
Docker version 18.06.1-ce, build e68fc7a
docker-compose version 1.22.0, build f46880fe
```

__Installation:__

To install or run the app under docker simply clone the repo locally and follow the instructions.

```powershell
# Build the Containers
docker-compose build

# Launch the Containers
docker-compose up

# Halt the Containers
docker-compose down
```

>Note: Set the Environment Variable for Registry Support ${DOCKER_REGISTRY}

[0]: ./diagrams/architecture.png "Architecture Diagram"