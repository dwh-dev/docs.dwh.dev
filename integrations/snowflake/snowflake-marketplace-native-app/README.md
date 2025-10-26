---
description: Always up-to-date lineage without external dependencies
---

# Snowflake Marketplace (Native App)

#### Overview

DWH.dev is available directly in the [Snowflake Marketplace](https://app.snowflake.com/marketplace/listing/GZTSZ1Y553M/dwh-dev-inc-dwh-dev-lineage) as a native application.

This allows you to deploy and run DWH.dev _**inside your own Snowflake account**_, without sharing data externally or managing any external infrastructure.

The Marketplace version of DWH.dev performs static SQL analysis and metadata lineage computation directly in your Snowflake environment - leveraging the same security, governance, and role-based access controls you already use.

***

#### Benefits of Marketplace Deployment

* **100% Snowflake-native** - no data leaves your account
* **Instant setup** - no servers or containers to manage
* **Secure** - fully isolated within your Snowflake account without external dependencies
* **Automatic updates** - always the latest version
* **Continuously up-to-date lineage** - DWH.dev refreshes lineage automatically based on schema change tracking
* **Integrated billing** - usage is billed through your existing Snowflake account balance (no separate contracts or credit cards)

#### Requirements & Resources

| **Snowflake Account** | Any account tier starting from **Standard**                                    | No dependency on [ACCESS\_HISTORY view](https://docs.snowflake.com/en/sql-reference/account-usage/access_history) — DWH.dev performs _static_ SQL analysis         |
| --------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Compute Pool**      | DWH.dev runs entirely inside a dedicated compute pool of size **CPU\_X64\_S**  | Adds credit utilization of \~0.11 credits/hour, as per [Snowflake Credit Consumption Table (1d)](https://www.snowflake.com/legal-files/CreditConsumptionTable.pdf) |
| **Warehouse**         | M size                                                                         | Used for query-history export                                                                                                                                      |
| **Permissions**       | Metadata read access on target databases and Read access to **QUERY\_HISTORY** | No SELECT access to data contents required.                                                                                                                        |
| **Network Access**    | None required                                                                  | fully in-account execution                                                                                                                                         |

#### Features

* [query\_history-analysis-and-schema-change-tracking.md](query_history-analysis-and-schema-change-tracking.md "mention")
* [ctas-cost-management.md](ctas-cost-management.md "mention")
* [ctas-logic-change-tracking.md](ctas-logic-change-tracking.md "mention")
* [ctas-logic-change-alerting.md](ctas-logic-change-alerting.md "mention")





