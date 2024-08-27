# ASOF Join

Perhaps not everyone knows, but Snowflake now has a new type of connection with an additional condition - [**ASOF JOIN**](https://docs.snowflake.com/en/sql-reference/constructs/asof-join).

> An ASOF JOIN operation combines rows from two tables based on timestamp values that follow each other, precede each other, or match exactly. For each row in the first (or left) table, the join finds a single row in the second (or right) table that has the closest timestamp value. The qualifying row on the right side is the closest match, which could be equal in time, earlier in time, or later in time, depending on the specified comparison operator.

```sql
SELECT l.c1 as a, l.c4 as b, r.c4 as c
  FROM left_table l ASOF JOIN right_table r
    MATCH_CONDITION(l.c3>=r.c3)
    ON(l.c1=r.c1 and l.c2=r.c2)
  ORDER BY l.c1, l.c2
```

The **MATCH\_CONDITION** is now displayed next to the **ON** condition in the [**in-query lineage**](../features/data-lineage/in-query-lineage.md). All columnar relationships are highlighted on click:

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>
