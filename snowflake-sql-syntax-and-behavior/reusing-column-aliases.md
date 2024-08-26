# Reusing column aliases

In any database, you can use aliases for both columns and expressions within queries:

```sql
SELECT
    id AS user_id,
    name AS user_name,
    age AS user_age,
    age * 2 AS user_age_doubled
FROM users;
```

But what can we do with these aliases? Database vendors allow different things. For example, in MySQL and PostgreSQL, aliases can only be used in **GROUP BY** and **ORDER BY**. In Clickhouse and **Snowflake**, however, aliases can be used everywhere. But, as usual, there are nuances :)

Let's create syntactically identical VIEWs:

```sql
CREATE TABLE abc AS SELECT 1 AS a, 100 AS b, 1000 AS c;

CREATE VIEW v13 AS 
SELECT 
    a+1 AS b,
    b+1 AS c
FROM abc;

CREATE VIEW v14 AS 
SELECT 
    a+1 AS d,
    d+1 AS e
FROM abc;
```

At first glance, the lineage for these views should be the same. But let's see what happened:

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Why in **V13** the column **C** not reuse the alias **B**? Because in **Snowflake** when using an alias equivalent to the original column name from the source, the original column takes precedence!

By the way, in Clickhouse, it works differently...

What was meant by saying that aliases work everywhere?

Aliases can be reused in JOIN and WHERE clauses:

```sql
CREATE TABLE t12 AS SELECT 1 AS a, 100 AS b;
CREATE TABLE t13 AS SELECT 1 AS c, 100 AS d;

CREATE VIEW v15 AS
SELECT 
 a + b AS e,
 c + d AS f
FROM 
  t12 
  JOIN t13 ON e = f;
```

or even like this:

```sql
CREATE VIEW v16 AS
SELECT 
  a1 + b1 AS e,
  c1 + d1 AS f,
  ROUND(e, f) AS g,
  ROUND(f, e) AS h 
FROM 
  t12 AS t121(a1, b1) 
  JOIN t13 AS t131(c1, d1) ON e = f
WHERE 
  g = h;
```

Since in [**Dwh.dev**](https://dwh.dev/) we display not only the data flows but also the [**columns used in JOIN and WHERE**](../features/join-and-where.md), you will also see the original column sources in the corresponding section.
