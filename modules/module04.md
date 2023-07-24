# Module 04 - Joins

[< Previous Module](../modules/module03.md) - **[Home](../README.md)** - [Next Module >](../modules/module05.md)


## :bookmark_tabs: Table of Contents

| #  | Section |
| --- | --- |
| 1 | [Introduction to the different types of joins](#1-Introduction-to-the-different-types-of-joins) |
| 2 | [Prepare the dataset](#2-prepare-the-dataset) |
| 3 | [Join creation with MDF](#3-Join-creation-with-MDF) |
| 4 | [Aggregation with MDF](#4-Aggregation-with-MDF) |

<div align="right"><a href="## Module-04---Joins">↥ back to top</a></div>

## 1. Introduction to the different types of joins

Relational databases usually contain multiple tables that are linked by common key fields. This normalized design minimizes duplication of data, but means that you'll often need to write queries to retrieve related data from two or more tables. The most fundamental and common method of combining data from multiple tables is to use a JOIN transformation. 

### Join Tables: Introduction

Mapping data flows currently supports five different join types.

Inner Join

	Inner join only outputs rows that have matching values in both tables.

Left Outer

	Left outer join returns all rows from the left stream and matched records from the right stream. If a row from the left stream has no match, the output columns from the right stream are set to NULL. The output will be the rows returned by an inner join plus the unmatched rows from the left stream.

Right Outer

	Right outer join returns all rows from the right stream and matched records from the left stream. If a row from the right stream has no match, the output columns from the left stream are set to NULL. The output will be the rows returned by an inner join plus the unmatched rows from the right stream.

Full Outer

	Full outer join outputs all columns and rows from both sides with NULL values for columns that aren't matched.

Custom cross join

	Cross join outputs the cross product of the two streams based upon a condition. If you're using a condition that isn't equality, specify a custom expression as your cross join condition. The output stream will be all rows that meet the join condition.

Fuzzy join

    You can choose to join based on fuzzy join logic instead of exact column value matching by turning on the "Use fuzzy matching" checkbox option.


<div align="right"><a href="## Module-04---Joins">↥ back to top</a></div>

## 2. Prepare the dataset

Let's start creating three datasets.

We are going to use two tables from the existing SQL database to demonstrate the join operation:
  SalesLT.Product and 
  SalesLT.ProductCategory

First we need to get to the Author tab from ADF studio.
We can see here a Dataset entry and positioning on the right we will see three dots. Clicking on the dots it will provide us the option to choose a "New Dataset"

![Label](../images/module04/09_NewDataset_01.png)

Then we need to filter using the sql keyword and select Azure SQL database and Continue

![Label](../images/module04/09_NewDataset.png)

Now provide a name to the dataset: ds_sql_product

Select a Linked service: ls_azuresql_irvnetmedium

Select a table name: SalesLT.Product

![Label](../images/module04/10_NewDatasetProduct.png)

Now we repeate the same process for the table SalesLT.ProductCategory:

![Label](../images/module04/11_NewDatasetProductCategory.png)

For the third dataset we need first to connect to the SQL database and execute the following code to create a target table:

create table dbo.ProductByCategory 
     (CategoryName nvarchar(50), TotalProducts int);

After that we can create a new SQL dataset as done previously, this time for the table dbo.ProductByCategory

![Label](../images/module04/11b_NewDatasetProductsByCategory.png)


<div align="right"><a href="## Module-04---Joins">↥ back to top</a></div>

## 3. Join creation with MDF


Let's start creating a new Pipeline

![Label](../images/module04/01_CreatePipeline.png)

Provide a name to the pipeline. In this case we uses  "pipeline-Join"

![Label](../images/module04/02_NameIt.png)

We need to add a Data Flow activity. Name it "Data FLow Join"

![Label](../images/module04/03_MDF_Join.png)

From settings tab for Data Flow click on new

![04_NewDataFlow](../images/module04/04_NewDataFlow.png)

You will see a data source box. Click on the arrow and select Add Source

![Label](../images/module04/12_AddSource1.png)

For source type select dataset and for dataset select the newly created ds_sql_product

![Label](../images/module04/12_AddSource1_Product.png)

Click on the second box Add source.

For source type select dataset and for dataset select the newly created ds_sql_productCategory

![Label](../images/module04/12_AddSource2_ProductCategory.png)

Now ad the base right of the Source1 box click on the plus sign to add an activity and select Join

![Label](../images/module04/13_AddJoin.png)

For Left stream select source1 and for right stream select source2.

![Label](../images/module04/14_AddJoinSource2.png)

For the join condition left source column once the cursor is inside the cell you will see an option to launch expression builder. select it.

![Label](../images/module04/13b_AddJoin.png)

From expression values select source1@ProductCategoryID
Press save and finish

![Label](../images/module04/14c_ExpBuilder1.png)

Perform the same for the right source column opening the expression builder

![Label](../images/module04/14d_ExpBuilder2.png)

From the expression value list select source2ProductCategoryID
Save and finish

![Label](../images/module04/14e_ExpBuilder3.png)

Provide the name TotalProducts for the column

![Label](../images/module04/14f_ExpBuilder4.png)

Now enable the Data flow debug
This will provide the ability to preview the data while building the pipeline.
Select AutoresolveIntegrationRuntime for faster response time.

![Label](../images/module04/15_EnableDebug.png)

We are now going to select only few columns from the previous join operation.

To make this click on the plus sign on the right of join box and choose "Select" from the schema modifier group.

![Label](../images/module04/16_AddSelect.png)

Select the source2@name and rename it on the right cell from Name to CategoryName

![Label](../images/module04/18_Select2.png)

Select as well the ProductID and delete all the other columns (trash symbol on the right of each lines)

![Label](../images/module04/19_Select3.png)

Now we can preview the output of this Select activity.

Just click on "Data preview" tab and Refresh in case of need.

You should see only two columns: ProductID and CategoryName.

![Label](../images/module04/20_SelectPreview.png)


<div align="right"><a href="## Module-04---Joins">↥ back to top</a></div>

## 4. Aggregation with MDF

During this part we are going to create an aggregation and send the results to a SQL table.

![Label](../images/module04/21_AddAggregate.png)

Let's start adding an aggregate activity:
Click on the plus sign on the right of select box and choose aggregate.

Select GroupBy and choose CategoryName as column. You can leave Name as the same.

![Label](../images/module04/22_GroupBy.png)

For the Aggregate instead select "Open expression builder"

![Label](../images/module04/23_OpenExBuilder.png)

In the expression builder type count and select the first option provided by the list.

![Label](../images/module04/24_Count.png)

Click inside the parentesis and from the expression value list choose ProductID.
You should have an expression like that one shown in th ebelow image.
Click save

![Label](../images/module04/25_TotalProducts.png)

We can now check the Data preview to verify the result of our operation.

You should see the columns CategoryName and TotalProducts

![Label](../images/module04/26_Preview.png)

As a final step we are adding a Sink operation to write output data to a SQL table.

Click on plus sign on the right side of the Aggregate operation and type sink.
Choose sink.

![Label](../images/module04/27_AddSink.png)

In the Sink detail page ensure the Sink type is set to dataset.

Then set the dataset to the previosly created ds_sql_ProductCategory and test connection.


![Label](../images/module04/28_AddSinkDetails.png)

Now that we completed outr pipeline you can Publish all the changes.

From the top bar, close to Validate all there is the Publish all button. Select it and ensure no errors are raised.

![Label](../images/module04/29_PublishAll.png)

In case of any error please review the message and provide the correction.

Now from the left menu, in the Pipelines list select the newly created pipeline named pipeline-Join

![Label](../images/module04/29b_FinalPipeline.png)

From the top menu select Add trigger and then Trigger now.
This will execute immediately the pipeline.
Instead with New/Edit you can set a specific schedule.

![Label](../images/module04/30_Execute.png)





