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
6. Change Data Capture Storage to SQL (module planned)
7. [Medallion Architecture: Bronze Layer](./modules/module07.md)
8. [Medallion Architecture: Silver Layer](./modules/module08.md)
9. [Medallion Architecture: Gold Layer](./modules/module09.md)
10. [Medallion Architecture: Consumption Layer](./modules/module10.md)
11. [Troubleshooting](./modules/module11.md)
12. [Best Practices](./modules/module12.md)

## :books: Optional Learning Modules

13. [SAP Change Data Capture](./modules/module13.md)
14. [Working with pipeline templates](./modules/module14.md)

<div align="right"><a href="#azure-data-factory-mapping-data-flow-workshop">↥ back to top</a></div>

## :books: Medallion Architecture
In a [medallion architecture](https://learn.microsoft.com/en-us/azure/databricks/lakehouse/medallion), data is organized into layers: 

- **Bronze Layer**: Holds raw data.
- **Silver Layer**: Contains cleansed data.
- **Gold Layer**: Stores aggregated data that's useful for business analytics.
- **Consumption Layer**: Applications and data integrations read from the gold layer and may optionally create versions of the data that are purpose-built for their use case. This layer may reside within a transactional database used by the application, another analytical storage repository, or built as an API or another technology.

In this model, data is democratized so that all or most services that work with a dataset connect to a single underlying data source to ensure consistency. Integrated, row-level security is typically built in to allow for maxium data asset re-use.

In this lab, the following concepts by layer are present:
- **Bronze Layer**
  - Data Ingestion
  - Data Retention Policy
- **Silver Layer**
  - De-duplication
  - Data quality assertions
  - Cast data types
  - Joins
  - Reroute errors
  - Schema drift
- **Gold Layer**
  - Calculated value(s)
  - Given that the source includes both general and confidential attributes, the data is sinked twice, once for consumption of general data and once for consumption of confidential data. 
    - *Sink for general sensitivity*: selected attributes that are confirmed to be available for general use are included using explicit column.
    - *Sink for confidential sensitivity*: all attributes are passed through using schema drift and auto-mapping.
- **Consumption Layer**
  - Read gold layer, and sink aggregate dataset with a new calculated column

<div align="right"><a href="#azure-data-factory-mapping-data-flow-workshop">↥ back to top</a></div>

## :link: References

- [Microsoft Learn: Mapping data flows in Azure Data Factory](https://learn.microsoft.com/en-us/azure/data-factory/concepts-data-flow-overview)
- [Microsoft Learn: Mapping data flows performance and tuning guide](https://learn.microsoft.com/en-us/azure/data-factory/concepts-data-flow-performance)
- [Microsoft Learn: Mapping data flow transformation overview](https://learn.microsoft.com/en-us/azure/data-factory/data-flow-transformation-overview) 
- [Microsoft Learn: Data transformation expressions in mapping data flows](https://learn.microsoft.com/en-us/azure/data-factory/data-transformation-functions)
- [Microsoft Learn: Mapping data flow video tutorials](https://learn.microsoft.com/en-us/azure/data-factory/data-flow-tutorials)
- [Microsoft Learn: Integration Runtime Custom shuffle partition](https://learn.microsoft.com/en-us/azure/data-factory/concepts-integration-runtime-performance#custom-shuffle-partition)

<div align="right"><a href="#azure-data-factory-mapping-data-flow-workshop">↥ back to top</a></div>

## :link: Workshop URL

[https://github.com/adhazel/Azure-Data-Factory-Mapping-Data-Flow-Workshop](https://github.com/adhazel/Azure-Data-Factory-Mapping-Data-Flow-Workshop)
