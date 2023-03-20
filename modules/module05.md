
[< Previous Module](../modules/module04.md) - **[Home](../README.md)** - [Next Module >](../modules/module05.md)

## :loudspeaker: Introduction

according to Wikipedia (#https://en.wikipedia.org/wiki/Slowly_changing_dimension): a slowly changing dimension (SCD) in data management and data warehousing is a dimension which contains relatively static data which can change slowly but unpredictably, rather than according to a regular schedule. A typical example is the change of address of a customer (which happens unpredictably).

Based on how to deal with a slowly dimensional data change in different scenarios, there are 7 SCD Types. The most frequently used are SCD Type 1 and SCD Type 2, which will be introduced in this module together with the implementation pattern in Azure Data Factory Mapping Data Flow. 


* Slowly Changing Dimensions Type 1 (overwrite without tracking history)
* Slowly Changing Dimensions Type 2 (track history by adding new row)
