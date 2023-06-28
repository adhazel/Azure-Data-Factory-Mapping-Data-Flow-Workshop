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

<div align="right"><a href="##module-3-two-ways-to-do-a-basic-copy-sample-data">↥ back to top</a></div>

## 1. Stage data in the data lake

Data was staged as part of the setup for this lab. See <a href="../modules/module00.md/###module-3-two-ways-to-do-a-basic-copy">↥ staging instructions</a>.

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

11. Click the `pl_simple_copy` pipeline from the list of Pipelines. On the **Source** tab of the **Copy data** activity, enter the following values. 

    | Attribute  | Value |
    | --- | --- |
    | Source dataset | `ds_irazure_adls_binary` |
    | Dataset properties / container | `inbound` |
    | Dataset properties / directory | `x` (This is a placeholder only; the value will be overwritten due to the **Wildcard file path** option selected in the **File path type** radio option.)|
    | Dataset properties / filename | `x` (This is a placeholder only; the value will be overwritten due to the **Wildcard file path** option selected in the **File path type** radio option.)|
    | File path type | `Wildcard file path` |
    | Wildcard paths / directory | `nyx_taxi_sample` |
    | Wildcard paths / filename | `*.parquet` |

   <kbd> <img src="../images/module03/create_new_pipeline_copy_source.png" alt="Create new pipeline copy source" /> </kbd>

12. On the **Sink** tab of the **Copy data** activity, enter the following values. 

    | Attribute  | Value |
    | --- | --- |
    | Sink dataset | `ds_irazure_adls_binary_directory` |
    | Dataset properties / container | `publish` |
    | Dataset properties / directory | `nyx_taxi_sample_pipeline` |

   <kbd> <img src="../images/module03/create_new_pipeline_copy_sink.png" alt="Create new pipeline copy sink" /> </kbd>

13. Click the **Debug** button and ensure your copy succeeds!

   <kbd> <img src="../images/module03/pipeline_succeeded.png" alt="Pipeline succeeded" /> </kbd>

14. Click the **Publish all** button, then click the **Publish** button.

   <kbd> <img src="../images/module03/publish_new_pipeline.png" alt="Publish all" /> </kbd>

<div align="right"><a href="#module-03---two-ways-to-do-a-basic-copy">↥ back to top</a></div>

## 3. Mapping Data Flows Copy

1. Within the Data Factory Studio, select the **Author** tab from the leftmost pane. Open the **Pipeline Actions** elipsis menu, and click the **New pipeline** menu item. In the **Properties** pane of the new pipeline, add a **Name** and **Description**.

    | Attribute  | Value |
    | --- | --- |
    | Name | `pl_simple_copy_df` |
    | Description | `Use the copy activity to copy data from one location to another using mapping data flows.` |

2. From the **Activities** pane, under **Move & transform**, click and drag the **Data flow** activity into the pipeline area. Then, on the **Settings** tab, click the **+ New** button.

   <kbd> <img src="../images/module03/create_pipeline_df.png" alt="Create pipeline with data flows" /> </kbd>
   <kbd> <img src="../images/module03/create_dataflow.png" alt="Create data flow" /> </kbd>

3. On the Properties pane, enter the following values.

    | Attribute  | Value |
    | --- | --- |
    | Name | `df_simple_copy` |
    | Description | `Data flow that performs a simple copy.` |

4. Click the **Data flow debug** radio toggle from within the data flows working area. Select the **Integration runtime** `ir-vnetwork-medium-60min`. Select `4 hours` from the **Debug time to live** option so that your debug Apache cluster will be available during the next 4 hours of the lab. Click **OK**. 

   <kbd> <img src="../images/module03/df_debug_start.png" alt="Create data flow debug cluster" /> </kbd>

5. Click the **Add Source** option from the down caret menu as shown below.

   <kbd> <img src="../images/module03/df_add_source.png" alt="DF Add Source" /> </kbd>

6. Complete the **Source settings**.

    | Attribute  | Value |
    | --- | --- |
    | Name | `source` |
    | Source type | `Inline` |
    | Inline dataset type | `Parquet` |
    | Linked service | `ls_adls_irvnetmedium` |
    | Sampling | `Enable` |

   <kbd> <img src="../images/module03/df_source_settings.png" alt="DF Source Settings" /> </kbd>

7. On the **Source options** tab, click the `Wildcard` **File mode** option and click the **Browse** button. An error may appear indicating that interactive authoring is disabled. This is a debug condition, whereby the . Click the **Edit interactive authoring** link.

   <kbd> <img src="../images/module03/edit_interactive_authoring.png" alt="DF Interactive authoring" /> </kbd>

8. On the **Edit integration runtime** pane, on the **Virtual network** tab, click **Enable** under **Interactive authoring**. Then, click **Apply**.

   <kbd> <img src="../images/module03/edit_interactive_authoring2.png" alt="DF Interactive authoring" /> </kbd>

9. When the runtime is edited to allow interactive authoring, the **Browse** pane will indicate `Interactive authoring enabled`. Click **Retry**.

   <kbd> <img src="../images/module03/edit_interactive_authoring3.png" alt="DF Interactive authoring" /> </kbd>

10. Use the **Browse** pane to navigate to `inbound` and click **OK**. The **File system** and **Wildcard paths** container values will show `inbound`.

   <kbd> <img src="../images/module03/df_source_browse.png" alt="DF Source browse" /> </kbd>

11. Enter `nyx_taxi_sample/*.parquet` in the **Wildcard paths** field as shown below.

   <kbd> <img src="../images/module03/df_source_settings2.png" alt="DF Source options path" /> </kbd>

12. On the **Projection** tab, click **Import schema**.

   <kbd> <img src="../images/module03/df_projection.png" alt="DF Source options path" /> </kbd>

13. On the **Data preview** tab, click **Refresh** to see a preview of the data. Data flow activity data previews are used in conjunction with sampling of the source data to allow for ease of development and to ensure the Azure Data Factory user interface is able to pre-populate the data mid-transformation.

   <kbd> <img src="../images/module03/df_source_preview.png" alt="DF Source preview" /> </kbd>

14. Click the **+** button on the bottom right corner of the `source` activity and then select the **Sink** option.

   <kbd> <img src="../images/module03/df_add_sink.png" alt="DF Sink Add" /> </kbd>

15. Enter the following values in the **Sink** tab.

    | Attribute  | Value |
    | --- | --- |
    | Name | `sink` |
    | Sink type | `Inline` |
    | Inline dataset type | `Parquet` |
    | Linked service | `ls_adls_irvnetmedium` |

16. On the **Settings** tab, click the **Browse** button, browse to `publish/nyx_taxi_sample_dataflow` and click **OK**.

   <kbd> <img src="../images/module03/df_sink_settings.png" alt="DF Sink Settings" /> </kbd>

17. Set the unmask settings as shown below.

    | Attribute  | Value |
    | --- | --- |
    | Owner | `R` + ` W` + `X` |
    | Group | `R` + ` W` + `X` |
    | Others | `X` |

18. On the **Data preview** tab, click **Refresh** to see a preview of the data.

   <kbd> <img src="../images/module03/df_sink_refresh.png" alt="DF Sink Refresh" /> </kbd>

19. Click the `pl_simple_copy_df` pipeline from the list of **Pipelines**.  Click the **Debug** button and ensure your copy succeeds!

   <kbd> <img src="../images/module03/df_debug.png" alt="DF Debug" /> </kbd>

20. Click the **Publish all** button, then click the **Publish** button.

   <kbd> <img src="../images/module03/df_publish_all.png" alt="Publish all" /> </kbd>

<div align="right"><a href="#module-03---two-ways-to-do-a-basic-copy">↥ back to top</a></div>

## :tada: Summary

You have now completed this module. You have performed a simple copy using both the **Pipelines** and the **Data flows** features. The pipelines copy used the Azure IR compute that does not use spark while the data flows pipeline you created utilized an IR with managed virtual network enabled with a medium sized Apache spark cluster.

[Continue >](../modules/module04.md)

