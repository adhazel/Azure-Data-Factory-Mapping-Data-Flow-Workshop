# Module 00 - Lab Environment Setup

**[Home](../README.md)** - [Next Module >](../modules/module01.md)

## :loudspeaker: Introduction

In order to follow along with the lab exercises, you need to provision a set of common resources and then provision an Azure Data Factory for each resource. Finally, sample data needs to be staged.

## :thinking: Prerequisites

<details>

* An [Azure account](https://azure.microsoft.com/free/) with an active subscription.
* The subscription must have the following resource providers registered.
  * Microsoft.Authorization
  * Microsoft.DataFactory
  * Microsoft.EventHub
  * Microsoft.KeyVault
  * Microsoft.Storage
  * Microsoft.Sql
  * Microsoft.Synapse
  * Microsoft.Insights
    > **Warning**  If you are using an **Azure Pass promo code**, the following resource providers - `Microsoft.Storage`, `Microsoft.EventHub`, and `Microsoft.Synapse` are not registered by default. Follow the instructions on [how to register a resource provider](./providers.md) before proceeding with the lab environment deployment below.
* Owner permissions within a Resource Group to create resources and manage role assignments.

</details>

## :gear: One Time Lab Environment Setup

<details>

  > **Warning**  Deployed assets will include allow Azure and allow all firewall rules for training purposes only. Use a testing environment for training. Consult appropriate networking and security teams before production implementation.

1. Right-click or `Ctrl + click` the button below to open the Azure Portal in a new window.

    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fadhazel%2FAzure-Data-Factory-Mapping-Data-Flow-Workshop%2Fmain%2Fenvironment%2Fazuredeploy.json)

    The below Azure resources will be included in the deployment:
    - Azure SQL Server and Database
    - Azure Synapse workspace and Synapse Dedicated Pool
    - 2 Azure Storage accounts (1 for the Synapse workspace and 1 for data files)
    - Azure Key Vault
    - Role assignment granting the Synapse workspace permission to the Storage Account for data files

2. Beneath the **Resource group** field, click **Create new** and provide a unique name (e.g. `adfmdflab-rg`), select a [valid location](https://azure.microsoft.com/global-infrastructure/services/?products=purview&regions=all) (e.g. `West US 3`), and then click **Review + create**.

    ![Deploy Template](../images/module00/create_deployment.png)

3. Once the validation has passed, click **Create**.

    ![Create Resources](../images/module00/create_deployment_create.png)

4. The deployment may take up to 10 minutes to complete. Once you see the message **Your deployment is complete**, click **Go to resource group**.

    ![Deployment Complete](../images/module00/deployment_complete.png)

5. If successful, you should see the resource group resources, similar to the screenshot below.

    ![Resource Group](../images/module00/deployed_resources.png)

</details>

## :gear: Per Participant Lab Environment Setup

<details>

1. Right-click or `Ctrl + click` the button below to open the Azure Portal in a new window.

    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fadhazel%2FAzure-Data-Factory-Mapping-Data-Flow-Workshop%2Fmain%2Fenvironment%2Fazuredeploy.json)

</details>

## :gear: Stage Sample Data

<details>

Sample data is used throughout the modules. Sample data is listed by module below. Follow the instructions to stage it before the event.

1. [Create Integration Runtime](./modules/module01.md)

No sample data 

# [Create Linked Services](./modules/module02.md)

# [Two Ways to do a Basic Copy](./modules/module03.md)



4. [Join Placeholder](./modules/module04.md)
5. [Slowly Changing Dimensions](./modules/module05.md)
6. Change Data Capture Storage to SQL (coming soon)
7. [Medallion Architecture: Bronze Layer](./modules/module07.md)
8. [Medallion Architecture: Silver Layer](./modules/module08.md)
9. [Medallion Architecture: Gold Layer](./modules/module09.md)
10. [Medallion Architecture: Consumption Layer](./modules/module10.md)
11. [Troubleshooting](./modules/module11.md)
12. [Best Practices](./modules/module12.md)


</details>


## :tada: Summary

By successfully deploying the lab template, you have the Azure resources needed to follow along with the learning exercises.

[Continue >](../modules/module01.md)