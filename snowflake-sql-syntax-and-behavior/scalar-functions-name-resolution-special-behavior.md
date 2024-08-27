# Scalar functions name resolution special behavior

This topic is about the behavior of name resolution in Snowflake inside **CREATE VIEW**.

When you execute queries, Snowflake looks for the objects specified in the query in the schemas specified in **SEARCH\_PATH**. You can view them like this:

```sql
SELECT current_schemas();
```

But it seems like a good idea to make the creation of VIEWs independent of **SEARCH\_PATH**. Otherwise, we will get different results when we work with VIEWs at different **SEARCH\_PATH**.

The documentation says the following:

> The **SEARCH\_PATH** is not used inside views or UDFs. All unqualifed objects in a view or UDF definition will be resolved in the view’s or UDF’s schema only.

That's great! And it works!

```sql
CREATE OR REPLACE DATABASE db1;
CREATE SCHEMA sh1;

CREATE TABLE public.t1(c1 int);

CREATE VIEW sh1.v1 AS
SELECT * FROM t1;
```

will return

```sql
SQL compilation error:
Object 'DB1.SH1.T1' does not exist or not authorized.
```

And not only for tables. For any objects, except … **scalar functions**!

```sql
CREATE OR REPLACE DATABASE db1;
CREATE SCHEMA sh1;

CREATE TABLE sh1.t1(c1 int);
INSERT INTO sh1.t1(c1) VALUES (1);

CREATE FUNCTION public.test()
RETURNS NUMBER
LANGUAGE SQL
AS '1';

CREATE VIEW sh1.v1 AS
SELECT *, test() c2 FROM t1;

select * from sh1.v1;
```

will return

```sql
C1  C2
1   1
```

Strange behavior, don't you agree?

In PostgreSQL, for example, it works like this: when creating a VIEW, all objects without schema specification are searched in the public schema. If you want a different schema, specify it by hand.

But maybe I'm being picky? Let's add one more thing…

```sql
CREATE FUNCTION sh1.test()
RETURNS NUMBER
LANGUAGE SQL
AS '2';

select * from sh1.v1;
```

will return

```sql
C1  C2
1   2
```

Oops… i.e. if there is a scalar function in the scheme where **VIEW** is created, it will be used. If not, the function from **PUBLIC** will be used.

**I.e. if you didn't specify a schema for a scalar function from the PUBLIC schema while creating a VIEW, in a schema other than PUBLIC, then to corrupt the data in your database it is enough to create a function with the same name in the corresponding schema…**

At [**Dwh.dev**](https://dwh.dev/), we don't display downstream lineage for scalar functions right now, but if you click on that function in the source code ([**which we display in a very cool way**](../features/data-catalog/fancy-sql-highlight.md)), you will jump to the exact function used in that context.
