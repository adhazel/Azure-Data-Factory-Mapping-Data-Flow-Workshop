# Module 05 - Slowly Changing Dimensions

[< Previous Module](../modules/module04.md) - **[Home](../README.md)** - [Next Module >](../modules/module05.md)

## :loudspeaker: Introduction

according to [Wikipedia](https://en.wikipedia.org/wiki/Slowly_changing_dimension): a slowly changing dimension (SCD) in data management and data warehousing is a dimension which contains relatively static data which can change slowly but unpredictably, rather than according to a regular schedule. Typical examples are the family name change of an employee after marrige and address change of a customer, which all happens unpredictably.

Based on how to deal with a slowly dimensional data change in different scenarios, there are several SCD Types. The most frequently used are SCD Type 1 and SCD Type 2, which will be introduced in this module together with the implementation pattern in Azure Data Factory Mapping Data Flow. 


* Slowly Changing Dimensions Type 1 (overwrite without tracking history)
* Slowly Changing Dimensions Type 2 (track history by adding new row)

## :bookmark_tabs: Table of Contents

| #  | Section |
| --- | --- |
| 1 | [Introduction SCD Type 1 and SCD Type 2](#1-introduction-scd-type-1-and-scd-type-2) |
| 2 | [Set up the linked service and dataset](#2-set-up-the-linked-service-and-dataset) |
| 3 | [Implement SCD Type 1 transformation with MDF](#3-implement-sdc-type-1-transformation-with-MDF) |
| 4 | [Implement SCD Type 2 transformation with MDF](#4-implement-sdc-type-2-transformation-with-MDF) |

<div align="right"><a href="#module-05---slowly-changing-dimensions">↥ back to top</a></div>

## 1. Introduction SCD Type 1 and SCD Type 2

### SCD Type 1
A **SCD Type 1** always reflects the latest values, and when changes in source data are detected, the dimension table data is overwritten. This design approach is common for columns that store supplementary values, like the email address or phone number of a customer. When a customer email address or phone number changes, the dimension table updates the customer row with the new values. It's as if the customer always had this contact information. The key field, such as CustomerID, would stay the same so the records in the fact table automatically link to the updated customer record.

<kbd> <img src="../images/module05/slowly-changing-dimensions-type-1-change.png" alt="example of SCD Type 1" /> </kbd>

### SCD Type 2
A **SCD Type 2** supports versioning of dimension members. Often the source system doesn't store versions, so the data warehouse load process detects and manages changes in a dimension table. In this case, the dimension table must use a surrogate key to provide a unique reference to a version of the dimension member. It also includes columns that define the date range validity of the version (for example, StartDate and EndDate) and possibly a flag column (for example, IsCurrent) to easily filter by current dimension members.

For example, Adventure Works assigns salespeople to a sales region. When a salesperson relocates region, a new version of the salesperson must be created to ensure that historical facts remain associated with the former region. To support accurate historic analysis of sales by salesperson, the dimension table must store versions of salespeople and their associated region(s). The table should also include start and end date values to define the time validity. Current versions may define an empty end date (or 12/31/9999), which indicates that the row is the current version. The table must also define a surrogate key because the business key (in this instance, employee ID) won't be unique.

<kbd> <img src="../images/module05/slowly-changing-dimensions-type-2-change.png" alt="example of SCD Type 2" /> </kbd>

