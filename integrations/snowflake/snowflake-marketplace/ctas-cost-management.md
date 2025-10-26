# CTAS cost management

{% embed url="https://youtu.be/l36dOAFYASg" %}

DWH.dev automatically identifies all `CREATE TABLE AS SELECT` (CTAS) operations and links them to their corresponding compute cost using data from Snowflake’s `QUERY_HISTORY`.\
Each CTAS execution is associated with its target object, warehouse, and runtime metadata — allowing DWH.dev to estimate and attribute the credit consumption of transformation pipelines.

Costs are calculated based on the warehouse type used during execution (e.g., `XSMALL`, `MEDIUM`) and the runtime duration recorded in `QUERY_HISTORY`.\
In native Marketplace deployments, this data is enriched with compute-pool utilization metrics, providing a unified view of both **warehouse** and **pool-level** resource usage.

#### Used for

* Identifying the most expensive CTAS transformations across your pipelines.
* Tracking warehouse utilization and compute-pool credit consumption.
* Optimizing task schedules and warehouse configurations to reduce recurring costs.
* Highlighting redundant or rarely used CTAS operations.
