# Module 09 - Medallion Architecture: Gold Layer

[< Previous Module](../modules/module08.md) - **[Home](../README.md)** - [Next Module >](../modules/module10.md)

## Introduction
This module shows what a gold layer within the medallion pattern might look like implemented in Azure Data Factory. The gold layer is often highly refined and aggregated, containing data that powers anlaytics, machine learning, and production applications. In this lab, the gold layer includes the following:
  - Calculated value(s)
  - Given that the source includes both general and confidential attributes, the data is sinked twice, once for consumption of general data and once for consumption of confidential data. 
    - *Sink for general sensitivity*: selected attributes that are confirmed to be available for general use are included using explicit column.
    - *Sink for confidential sensitivity*: all attributes are passed through using schema drift and auto-mapping.

Key capabilities of the gold layer are listed below:

- Represents a highly refined and/or enriched version of the data
- Acts as re-usable asset for self-service and enterprise applications and data integrations
- Reduces data duplication across consumption teams and personas when combined with row level security
- Has lower latency query performance because ...
    - Most transformations are handled before data is written to the gold layer
    - Data is read-optimized
    - Multiple variations of a dataset may be published in the gold layer to support diverse query patterns

## :bookmark_tabs: Table of Contents

If there are multiple sections to this page, add a Table of Contents with jump links.

| #  | Section |
| --- | --- |
| 1 | [Section 1 Header](#1section-1-header) |
| 2 | [Section 2 Header](#2section-2-header) |

<div align="right"><a href="#module-##---module-title">↥ back to top</a></div>

## 1. Section 1 Header

Section 1 content

<div align="right"><a href="#module-##---module-title">↥ back to top</a></div>

## 2. Section 2 Header

Section 2 content

## :tada: Summary

You have now completed this module. 

[Continue >](../modules/module##.md)