# Module 00 - Lab Environment Setup

**[Home](../README.md)** - [Next Module >](../modules/module01.md)

## :loudspeaker: Introduction

In order to follow along with the lab exercises, you need to provision a set of resources.

## :thinking: Prerequisites

* An [Azure account](https://azure.microsoft.com/free/) with an active subscription.
* Owner permissions within a Resource Group to create resources and manage role assignments.
* The subscription must have the following resource providers registered.
  * Microsoft.Authorization
  * Microsoft.DataFactory
  * Microsoft.EventHub
  * Microsoft.KeyVault
  * Microsoft.Storage
  * Microsoft.Sql
  * Microsoft.Synapse
  * Microsoft.Insights

    > :warning: If you are using an **Azure Pass promo code**, the following resource providers - `Microsoft.Storage`, `Microsoft.EventHub`, and `Microsoft.Synapse` are not registered by default. Follow the instructions on [how to register a resource provider](./providers.md) before proceeding with the lab environment deployment below.

## :test_tube: One Time Lab Environment Setup

1. Right-click or `Ctrl + click` the button below to open the Azure Portal in a new window.

    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fadhazel%2FAzure-Data-Factory-Mapping-Data-Flow-Workshop%2Fmain%2Fenvironment%2Fazuredeploy.json)

    This deployment will do the following:
    
    1. Deploy an Azure SQL Server and Database (with an open firewall for training purposes only)
    2. Deploy an Azure Storage account and container
    3. Create a Synapse workspace and Synapse Dedicated Pool 

    > **Warning**
    > Deployed assets will include allow Azure and allow all firewall rules for training purposes only


2. Beneath the **Resource group** field, click **Create new** and provide a unique name (e.g. `adfmdflab-rg`), select a [valid location](https://azure.microsoft.com/global-infrastructure/services/?products=purview&regions=all) (e.g. `West US 3`), and then click **Review + create**.

    ![Deploy Template](../images/module00/create_deployment.png)

3. Once the validation has passed, click **Create**.

    ![Create Resources](../images/module00/create_deployment_create.png)

4. The deployment may take up to 10 minutes to complete. Once you see the message **Your deployment is complete**, click **Go to resource group**.

    ![Deployment Complete](../images/module00/deployment_complete.png)

5. If successful, you should see the resource group resources, similar to the screenshot below.

    ![Resource Group](../images/module00/deployed_resources.png)

## :test_tube: Per Participant Lab Environment Setup

1. Right-click or `Ctrl + click` the button below to open the Azure Portal in a new window.

    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fadhazel%2FAzure-Data-Factory-Mapping-Data-Flow-Workshop%2Fmain%2Fenvironment%2Fazuredeploy.json)


## :tada: Summary

By successfully deploying the lab template, you have the Azure resources needed to follow along with the learning exercises.

[Continue >](../modules/module01.md)