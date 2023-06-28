# Module 00 - Lab Environment Setup

**[Home](../README.md)** - [Next Module >](../modules/module01.md)

## :loudspeaker: Introduction

In order to follow along with the lab exercises, you need to provision a set of common resources and then provision an Azure Data Factory for each resource. Finally, sample data needs to be staged. 

| #  | Jump To |
| --- | --- |
| 1 | [Prerequisites](#thinking-prerequisites) |
| 2 | [One Time Lab Environment Setup](#gear-one-time-lab-environment-setup) |
| 3 | [Per Participant Lab Environment Setup](#gear-per-participant-lab-environment-setup) |
| 4 | [Stage Sample Data](#gear-stage-sample-data) |

## :thinking: Prerequisites

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

<div align="right"><a href="#module-00---lab-environment-setup">↥ back to top</a></div>

## :gear: One Time Lab Environment Setup

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

<div align="right"><a href="#module-00---lab-environment-setup">↥ back to top</a></div>

## :gear: Per Participant Lab Environment Setup

1. Right-click or `Ctrl + click` the button below to open the Azure Portal in a new window.

    [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fadhazel%2FAzure-Data-Factory-Mapping-Data-Flow-Workshop%2Fmain%2Fenvironment%2Fazuredeployadf.json)

    The below Azure resources will be included in the deployment:
    - Azure Data Factory
    - Role assignment granting the participant resource group contributor access
    - Role assignment granting the participant Storage Blob Data Contributor access to the Storage Accont for data files
    - Role assignment granting the Azure Data Factory permission to the Storage Account for data files

<div align="right"><a href="#module-00---lab-environment-setup">↥ back to top</a></div>

## :gear: Stage Sample Data

<div align="right"><a href="#module-00---lab-environment-setup">↥ back to top</a></div>

Sample data is used throughout the modules. Sample data is listed by module below. Follow the instructions to stage it before the event.

### Module 3 [Two Ways to do a Basic Copy](./modules/module03.md) Sample Data 

The pipelines in this module use a 5 MB file named *NYCTripSmall.parquet*. This file needs to be in the Azure Storage Account created for this lab.

1. Download this file from [../data_to_be_staged/adls/inbound/nyx_taxi_sample/NYCTripSmall.parquet](../data_to_be_staged/adls/inbound/nyx_taxi_sample/NYCTripSmall.parquet).

2. From the Azure Resource Group overview page, find and click the Azure Storage Account lab resource named `dfmdf< Random string for your lab environment resources >adls` to open the storage account.

   <kbd> <img src="../images/module03/open_storage_account.png" alt="Open ADLS" /> </kbd>

3. Within the Azure Storage Account, open the **Containers** page from within the **Data storage** section of the left pane. Then, click the **+ Container** button and add an `inbound` container.

   <kbd> <img src="../images/module03/create_inbound_container.png" alt="Create inbound Container" /> </kbd>

4. Click the container name to open the container. Then, click **+ Add Directory**. Add a directory Name `nyx_taxi_sample' and click **Save** to create the directory.

   <kbd> <img src="../images/module03/create_nyx_taxi_sample_dir.png" alt="Create nyx tax dir" /> </kbd>

5. Click the directory name to open the directoy. Then, click the **Upload** button and drag and drop the `NYCTripSmall.parquet` file you downloaded in step 1 into the **Upload blob** drag and drop area. Finally, click **Upload**.

   <kbd> <img src="../images/module03/uploadNYCTripSmall.png" alt="Upload nyx taxi data" /> </kbd>

6. Within the Azure Storage Account, open the **Containers** page from within the **Data storage** section of the left pane. Then, click the **+ Container** button and add an `publish` container.

   <kbd> <img src="../images/module03/create_publish_container.png" alt="Create publish Container" /> </kbd>

7. Click the `publish` container name to open the container. Then, click **+ Add Directory**. Add a directory named `nyx_taxi_sample_pipeline` and click **Save** and add a second directory named `nyx_taxi_sample_dataflow` and click **Save**.

   <kbd> <img src="../images/module03/create_publish_directories.png" alt="Create publish directories" /> </kbd>

### Module 4 [Join Placeholder](./modules/module04.md) Sample Data 

Instructions here


### Module 5 [Slowly Changing Dimensions](./modules/module05.md) Sample Data 

Instructions here

### Module 7 [Medallion Architecture: Bronze Layer](./modules/module07.md) Sample Data 

Instructions here

<div align="right"><a href="#module-00---lab-environment-setup">↥ back to top</a></div>

## :tada: Summary

By successfully deploying the lab template, you have the Azure resources and data needed to follow along with the learning exercises.

[Continue >](../modules/module01.md)

<div align="right"><a href="#module-00---lab-environment-setup">↥ back to top</a></div>