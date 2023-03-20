# Azure-Data-Factory-Mapping-Data-Flow-Workshop

Use this repository for hands-on training of Azure Data Factory Mapping Data Flows capabilities.

## What is Azure Data Factory?

Azure Data Factory is Azure's cloud ETL service for scale-out serverless data integration and data transformation. It offers a code-free UI for intuitive authoring and single-pane-of-glass monitoring and management.

:grey_exclamation: Another product within Azure, Azure Synapse Pipelines, is mostly synonomous with Azure Data Factory. While this repository uses Azure Data Factory for demonstration purposes, the lessons and concepts can be applied to Azure Synapse Pipelines as well.

## What are Azure Data Factory mapping data flows?

This repository focuses on the mapping data flows feature within Azure Data Factory. Mapping data flows allow data engineers to develop data transformation logic without writing code (visual ETL). The resulting data flows are executed as activities within Azure Data Factory pipelines that use scaled-out Apache Spark clusters. Data flow activities can be operationalized using existing Azure Data Factory scheduling, control, flow, and monitoring capabilities.

Mapping data flows provide an entirely visual experience with no coding required. Your data flows run on ADF-managed execution clusters for scaled-out data processing. Azure Data Factory handles all the code translation, path optimization, and execution of your data flow jobs.

## :thinking: Prerequisites

* An [Azure account](https://azure.microsoft.com/free/) with an active subscription. Note: If you don't have access to an Azure subscription, you may be able to start with a [free account](https://www.azure.com/free).
* You must have the necessary privileges within your Azure subscription to create resources, perform role assignments, register resource providers (if required), etc.

## :test_tube: Lab Environment Setup

* [Lab Environment](./modules/module00.md)

## :books: Learning Modules

1. [Create Integration Runtime](./modules/module01.md)
2. [Create Linked Services](./modules/module02.md)
3. [Two Ways to do a Basic Copy](./modules/module03.md)
4. [Join Placeholder](./modules/module04.md)
5. [Slowly Changing Dimensions](./modules/module05.md)

## :books: Optional Learning Modules

3. Other modules here

<div align="right"><a href="#azure-data-factory-mapping-data-flow-workshop">↥ back to top</a></div>

## :link: Workshop URL

[https://github.com/adhazel/Azure-Data-Factory-Mapping-Data-Flow-Workshop](https://github.com/adhazel/Azure-Data-Factory-Mapping-Data-Flow-Workshop)