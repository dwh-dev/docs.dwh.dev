# CTE as an expression alias

We all like to use **CTEs (Common Table Expression)**. It makes our code cleaner and sometimes helps to speed up queries.

But somehow, Snowflake documentation hides from us one beautiful behavior of CTE that will make your life even more convenient.

What does the [documentation say](https://docs.snowflake.com/en/user-guide/queries-cte)?

> A CTE (common table expression) is a named subquery defined in a WITH clause. You can think of the CTE as a temporary view for use in the statement that defines the CTE

In other words:

* we can only use SELECT in the CTE
* the result of the CTE is a view-like object

Surely many of you have used the CTE to define some constants that are used further in the query. For example:

```sql
WITH
  var_cte AS (
    SELECT 'Snowflake' AS vendor
  )
SELECT *
FROM t
WHERE
  vendor = (SELECT vendor FROM var_cte)
```

Tolerable, but not perfect. Especially scalar sub-queries. Scalar sub-queries are bad practice. Avoid using them!

Can this be done more elegantly? Yes! Look at this:

```sql
WITH
  var_cte AS ('Snowflake')
SELECT *
FROM t
WHERE
  vendor = var_cte;
```

Wow! The code became easier to read, and we got rid of scalar sub-queries at the same time!

What if we want to use several values at once? We can make an object:

```sql
WITH
  var_cte AS ({'vendor': 'Snowflake'})
SELECT * FROM t WHERE
  vendor = var_cte:vendor;
```

Or here's the IN analog:

```sql
WITH
  var_cte AS (['Snowflake', 'Bigquery'])
SELECT * FROM t WHERE
  ARRAY_CONTAINS(vendor::VARIANT, var_cte)
```

Although it's not so beautiful anymore…

It turns out that CTE can be not only a view-like object but also a scalar value!

Very cool, but even this is not a final:

```sql
CREATE TABLE t AS SELECT 1 AS a, 2 AS b;

WITH
  var_cte AS (a+b)
SELECT
  var_cte
FROM t;
```

As a result, we will get a table with a var\_cte column and a value of 3.

**I.e. CTE is not only a view-like object, and not only a scalar value but also an alias to any expression!**

Here's another example:

```sql
WITH
  var_cte AS (SUM(a))
SELECT
  var_cte
FROM t;
```

Yes, you can use any function calls there, including aggregate function calls.

And even that works too:

```sql
WITH
  var_cte1 AS (a),
  var_cte2 AS (var_cte1+b)
SELECT
  var_cte2
FROM t;
```

And like a function's argument:

```sql
WITH
  var_cte AS (a + b)
SELECT
  ROUND(var_cte/2, 0)
FROM t;
```

Are there any downsides? Unfortunately, yes… First of all, CTE macros refuse to work when you use them in UNION and inline FROM queries:

```sql
-- doesn't work!

WITH
  var_cte AS (a+b)
SELECT var_cte FROM t1
UNION
SELECT var_cte FROM t2
;

-- and here

WITH
  var_cte AS (a)
SELECT * FROM (
  SELECT var_cte FROM t
);
```

Maybe Snowflake engineers will finish this functionality and CTE macros will become possible to use everywhere. Let's hope they know about it themselves :)

And second, none of the data lineage tools will tell you that.

But the good news is that in [dwh.dev](https://dwh.dev/) we take CTE macros into account at compile time and display all relevant connections in lineage!

PS: I found out about it quite by accident from the last example in the [documentation of the ENCRYPT\_RAW function](https://docs.snowflake.com/en/sql-reference/functions/encrypt\_raw#examples)
