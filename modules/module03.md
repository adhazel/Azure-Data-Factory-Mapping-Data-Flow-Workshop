# Module 03 - Two Ways to do a Basic Copy

[< Previous Module](../modules/module02.md) - **[Home](../README.md)** - [Next Module >](../modules/module04.md)

## :loudspeaker: Introduction

A basic data movement can be accomplished two ways in Azure Data Factory. This module will demonstrate both:

* Pipeline copy
* Mapping data flows copy

## :bookmark_tabs: Table of Contents

| #  | Section |
| --- | --- |
| 1 | [Stage data in the data lake](#1stage-data-in-the-data-lake) |
| 2 | [Pipeline copy](#2pipeline-copy) |
| 3 | [Mapping data flows copy](#3mapping-data-flows-copy) |

<div align="right"><a href="#module-03---two-ways-to-do-a-basic-copy">↥ back to top</a></div>

## 1. Stage data in the data lake

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

<div align="right"><a href="#module-03---two-ways-to-do-a-basic-copy">↥ back to top</a></div>

## 2. Pipeline Copy

1. Within the Data Factory Studio, select the **Author** tab from the leftmost pane. Open the **Pipeline Actions** elipsis menu, and click the **New pipeline** menu item.

   <kbd> <img src="../images/module03/create_new_pipeline.png" alt="new pipeline" /> </kbd>

2. In the **Properties** pane of the new pipeline, add a **Name** and **Description**.

    | Attribute  | Example Value |
    | --- | --- |
    | Name | `pl_simple_copy` |
    | Description | `Use the copy activity to copy data from one location to another.` |

2. From the **Activities** pane, under **Move & transform**, click and drag the **Copy data** activity into the pipeline area. Then, on the **Source** tab of the activity properties, click the **+ New** button.

   <kbd> <img src="../images/module03/new_dataset.png" alt="New dataset" /> </kbd>

3. In the **New dataset** pane, find **Azure Data Lake Storage Gen 2** and click the **Continue** button.

4. Click the **Binary** option and click the **Continue** button.

5. Enter the properties and click the **OK** button.

    | Attribute  | Value |
    | --- | --- |
    | Name | `ds_irazure_adls_binary` |
    | Linked Service | `ls_adls_irazure` |

6. Click the **Open** button from the **Source** tab of the activity properties.

   <kbd> <img src="../images/module03/open_dataset_adls.png" alt="New dataset adls 2" /> </kbd>

7. On the **Parameters** tab of the new dataset, click the **+ New** button and add three parameters.

    | Name  | Type | Default value |
    | --- | --- | --- |
    | `container` | `String` | leave blank |
    | `directory` | `String` | leave blank |
    | `filename` | `String` | leave blank |

   <kbd> <img src="../images/module03/new_dataset_params.png" alt="New dataset adls 3" /> </kbd>

8. On the **Connection** tab of the new dataset, for all 3 attributes of the **File path**, roll over the attribute fields and click the **Add dynamic content** link that appears under each field. Then, add the parameters to the appropriate fields, the first field being for the `container` parameter, then `directory`, then `filename`.

   <kbd> <img src="../images/module03/new_dataset_adls_connection.png" alt="New dataset adls 4" /> </kbd>
   <kbd> <img src="../images/module03/new_dataset_adls_connection2.png" alt="New dataset adls 5" /> </kbd>

9. Click the `ds_ir_azure_adls_binary` dataset elipsis menu item and select **Clone**.

   <kbd> <img src="../images/module03/clone_adls_dataset.png" alt="Clone dataset" /> </kbd>

10. On the **Properties** pane of the cloned dataset, replace the text "copy1" in the **Name** with `directory`. Then, roll over the file name part of the **File path** and click the gargage bin icon. On the **Parameters** tab, check the filename parameter and click the **Delete** button. 

   <kbd> <img src="../images/module03/clone_adls_dataset2.png" alt="New dataset adls 6" /> </kbd>
   <kbd> <img src="../images/module03/clone_adls_dataset3.png" alt="New dataset adls 7" /> </kbd>

11. Click the `pl_simple_copy` pipeline tab in the working pane. On the **Source** tab of the **Copy data** activity, enter the following values. 

    | Attribute  | Value |
    | --- | --- |
    | Source dataset | `ds_irazure_adls_binary` |
    | Dataset properties / container | `inbound` |
    | Dataset properties / directory | `x` (This is a placeholder only; the value will be overwritten due to the **Wildcard file path** option selected in the **File path type** radio option.)|
    | Dataset properties / filename | `x` (This is a placeholder only; the value will be overwritten due to the **Wildcard file path** option selected in the **File path type** radio option.)|
    | File path type | `Wildcard file path` |
    | Wildcard paths / directory | `nyx_taxi_sample` |
    | Wildcard paths / filename | `*.parquet*` |

   <kbd> <img src="../images/module03/create_new_pipeline_copy_source.png" alt="Create new pipeline copy source" /> </kbd>

12. On the **Sink** tab of the **Copy data** activity, enter the following values. 

    | Attribute  | Value |
    | --- | --- |
    | Sink dataset | `ds_irazure_adls_binary_directory` |
    | Dataset properties / container | `publish` |
    | Dataset properties / directory | `nyx_taxi_sample_pipeline` |

   <kbd> <img src="../images/module03/create_new_pipeline_copy_sink.png" alt="Create new pipeline copy sink" /> </kbd>

13. Click the **Debug** button and ensure your copy succeeds!

adfadfadfadfadf
<div align="right"><a href="#module-03---two-ways-to-do-a-basic-copy">↥ back to top</a></div>

## 3. Mapping Data Flows Copy

mapping data flow copy

## :tada: Summary

You have now completed this module. 

[Continue >](../modules/module04.md)

