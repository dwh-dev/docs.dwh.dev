# Identifiers

## Basic Syntax ([Youtube](https://youtu.be/RIfgdpIOA3Q))

**Snowflake** provides an extensive toolkit for working with object and column identifiers. Let's start with the basics: identifiers with and without quotes ([documentation](https://docs.snowflake.com/en/sql-reference/identifiers-syntax))

Even at this stage, we won't achieve full compatibility with the syntax of other databases. However, two nuances deserve special attention:

* Identifiers without quotes are converted to uppercase.
* Identifiers within backticks behave similarly.

```sql
CREATE TABLE `Myidentifier` (
  f5 INT
);

CREATE TABLE "quote""andunquote""" (
  f6 INT
);
```

We collected all the varieties of the basic syntax [in 1.identifiers.1.sql](https://github.com/dwh-dev/data-lineage-challenge/blob/main/snowflake/1.identifiers/sql/1.identifiers.1.sql)

Here is the [**Dwh.dev**](https://dwh.dev/) result:

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

## Special syntax ([Youtube](https://youtu.be/hGf2VtBxzHU))

In addition to the basic syntax, **Snowflake** has special functionality:

* [Literals and Variables as Identifiers](https://docs.snowflake.com/en/sql-reference/identifier-literal). A special **IDENTIFIER()** function to get a reference to an object or column from a session variable or string.
* [Table Literals](https://docs.snowflake.com/en/sql-reference/literals-table) Special function **TABLE()** to get a reference to an object from a session variable or string.
* [Double-Dot Notation](https://docs.snowflake.com/en/sql-reference/name-resolution#resolution-when-schema-omitted-double-dot-notation) A special syntax that allows the **PUBLIC** scheme to be omitted when addressing an object.

```sql
CREATE VIEW V1 AS
  SELECT * 
  FROM
    identifier($table_var1)
;

-- Column Identifier
CREATE VIEW V4 AS
  SELECT identifier('DEMO_DB.SCH1.T1.V1'):json_prop as prop 
  FROM 
    DEMO_DB.SCH1.T1
;

-- Double-Dot Notation
CREATE VIEW V8 AS
  SELECT * 
  FROM
    DEMO_DB..T3
;
```

This syntax is often found in the description of transformations because it helps to use the same source code with different object names.

We have collected all kinds of special syntax [in 1.identifiers.2.sql](https://github.com/dwh-dev/data-lineage-challenge/blob/main/snowflake/1.identifiers/sql/1.identifiers.2.sql).

Here is the [**Dwh.dev**](https://dwh.dev/) result:

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>
