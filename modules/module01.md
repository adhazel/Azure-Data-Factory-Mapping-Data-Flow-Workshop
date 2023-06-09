# Module 01 - Create Integration Runtime

[< Previous Module](../modules/module00.md) - **[Home](../README.md)** - [Next Module >](../modules/module02.md)

## :loudspeaker: Introduction
The Integration Runtime (IR) is the compute infrastructure used by Azure Data Factory and Azure Synapse pipelines. For more information about integration runtimes, see [Integration runtime in Azure Data Factory](https://learn.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime).

In this workshop, the default Azure Integration Runtime is used, along with Managed Virtual Network. Azure integration runtime provides a fully managed, serverless compute in Azure. You don't have to worry about infrastructure provision, software installation, patching, or capacity scaling. In addition, you only pay for the duration of the actual utilization. The enablement of Managed Virtual Network allows you to use the power of spark within mapping data flows.

<div align="right"><a href="#module-01---create-integration-runtimes-and-linked-services">↥ back to top</a></div>

## Create an Azure IR with Managed Virtual Network enabled

1. From the resources list in the resource group, find and click the Data factory (V2) resource to open Azure Data Factory.

   <kbd> <img src="../images/module01/open_datafactory.png" alt="Open Data Factory Studio" /> </kbd>

2. Click the **Launch studio** button.

   <kbd> <img src="../images/module01/launch_datafactory.png" alt="Launch Data Factory Studio" /> </kbd>

3. Within the Data Factory Studio, select the **Manage** tab from the leftmost pane. Select **Integration runtimes** on the left pane, and click the **+ New** button.

   <kbd> <img src="../images/module01/add_integration_runtime.png" alt="Open Data Factory" /> </kbd>

4. Click the **Azure, Self-Hosted** option and then click **Continue**.

   <kbd> <img src="../images/module01/create_ir_1.png" alt="Select Azure and Continue" /> </kbd>

5. Click the **Azure** option and then click **Continue**.

   <kbd> <img src="../images/module01/create_ir_2.png" alt="Select Azure and Continue" /> </kbd>

6. On the **Settings** tab, enter the following values.

    | Attribute  | Example Value |
    | --- | --- |
    | Name | `ir-vnetwork-medium-60min` |
    | Description | `An integration runtime with managed virtual network enabled and a 60 minute cluster time to live. Cluster size is set to medium.` |
    | Region | `Auto Resolve` |

   <kbd> <img src="../images/module01/create_ir_3.png" alt="Enter IR Settings" /> </kbd>

6. On the **Virtual network** tab, select **Enable** for **Virtual network configuration** and ensure the **Interactive authoring** box is checked with a **Time to live** of `60 minutes`.

   <kbd> <img src="../images/module01/create_ir_4.png" alt="Enter IR Virtual network settings" /> </kbd>

6. On the **Data flow runtime** tab, select a **Compute size** of `Medium` and click **Create**.

   <kbd> <img src="../images/module01/create_ir_5.png" alt="Enter IR Data Flow compute size" /> </kbd>

   The IR will be provisioned by Azure. Note that this can take up to 15 minutes.

   <kbd> <img src="../images/module01/create_ir_6.png" alt="IR Provisioning" /> </kbd>

   Once the IR is provisioned, the **Status** will be `Running` and you can proceed to the next section.

## :tada: Summary

You have now created an integration runtime with managed virtual network enabled, designed to be used with mapping data flow transformations.

[Continue >](../modules/module02.md)