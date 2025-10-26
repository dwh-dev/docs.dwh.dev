---
cover: .gitbook/assets/dwh-docs-cover-03.png
coverY: 0
---

# What is Dwh.dev?

## **Dwh.dev - next-gen data lineage for Snowflake**

We provide a unique data lineage solution built especially for Snowflake users.&#x20;

[**Dwh.dev**](https://dwh.dev) is designed to help data teams easily understand, document, and manage their data flow.

With [**Dwh.dev**](https://dwh.dev), you can search and visualize your data lineage, track data dependencies issues, and better understand your data pipelines.&#x20;

It's a perfect solution for data engineers, analysts, and scientists who want to boost their productivity and efficiency.

It's easy to start: any type of [**integration**](integrations/) takes about a few minutes!

## **How does it work?**

[**Dwh.dev**](https://dwh.dev) is based on a static analyzer.\
We parse SQL, then compile it into an internal representation and analyze it **automatically**.

We don't use information from Snowflake system tables, which allows us to provide features such as:

* [**Offline mode**](integrations/snowflake/offline-mode.md): building data lineage without a direct connection to your database.
* [**In-query lineage**:](features/column-level-lineage/in-query-lineage.md) visualizing the dependency graph within a query.
* [**Equals lineage**](features/column-level-lineage/equals-column-lineage.md): displaying a hidden dependency graph based on conditions in `JOIN` and `WHERE`.
* [**QUERY\_HISTORY analysis and schema change tracking**](integrations/snowflake/snowflake-marketplace/query_history-analysis-and-schema-change-tracking.md)
* [**CTAS cost management**](integrations/snowflake/snowflake-marketplace/ctas-cost-management.md)
* [**CTAS logic change tracking**](integrations/snowflake/snowflake-marketplace/ctas-logic-change-tracking.md)
* [**CTAS logic change alerting**](integrations/snowflake/snowflake-marketplace/ctas-logic-change-alerting.md)
* And much more.

You can access the parsing and compilation results through [**our API**](integrations/api.md).

