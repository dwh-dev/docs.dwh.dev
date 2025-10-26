# Snowflake

#### Operation Modes

| [**Snowflake Marketplace (Native App)**](snowflake-marketplace/) | Runs fully inside your Snowflake account as a native application. All parsing, lineage analysis, and metadata storage happen within your Snowflake environment using Snowflake-managed compute. Supports live schema change tracking and logic change alerting | ✅ Recommended — provides the richest feature set, automatic updates, and integrated billing. |
| ---------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| [**Offline Mode**](offline-mode.md)                              | Runs as a service in our cloud. Only static SQL files are analyzed; no connection to Snowflake is required. Ideal for isolated environments or CI/CD validation pipelines.                                                                                     | For restricted environments or local development.                                            |

> 💡 We recommend using the Snowflake Marketplace deployment, as it provides the most complete functionality — including live lineage synchronization, compute-pool execution, governance integration, and seamless billing via your Snowflake account balance.
